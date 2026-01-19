# Orchestrator - Workflow Coordinator

## Objective
Coordinates data flow between agents, monitors triggers, and manages the end-to-end job application workflow using n8n.

---

## Trigger Points

### 1. Orchestrator → Matcher Flow
**Trigger**: Scheduled job search (periodic, e.g., every 6 hours or daily)

**Workflow**:
1. **Trigger**: n8n cron schedule (configurable, default: every 6 hours)
2. **Action**: Orchestrator triggers Matcher Agent via webhook
3. **Matcher workflow**:
   - Searches for new jobs across configured sources
   - Evaluates fit score for each job
   - Stores jobs via `ApplicationManagement` MCP tool
4. **Result**: New job matches stored and ready for next flow

---

### 2. Orchestrator → Composer Flow (Asynchronous)
**Trigger**: New job(s) with fit_band = "High" (score ≥85) AND dealbreakers = null detected

**Workflow**:
1. **Monitor**: Orchestrator polls `ApplicationManagement` tool every 15 minutes
2. **Query**: Uses `ApplicationManagement.get_applications_by_status(user_id, "new_match", limit)` to find new applications
3. **Filter**: From results, process only applications where:
   - `fit_band` = "High" (score ≥85)
   - `dealbreakers` = null (no blocking issues)
4. **For each filtered high-quality match** (one call per application):
   - Orchestrator makes **ONE individual call** to Composer per application
   - Each call is independent and asynchronous
   - If there are 5 new matches, Orchestrator makes 5 separate calls to Composer
   - Composer can process these in parallel

5. **Composer webhook call** (per application):
   - HTTP POST to Composer endpoint
   - Request payload (single application):
     ```json
     {
       "application_id": "uuid-app-123",
       "user_id": "uuid-user-456",
       "callback_url": "https://orchestrator.careeragent.io/webhooks/composition-complete"
     }
     ```
   - **Orchestrator does NOT wait** - immediately continues to next application or other tasks

6. **Composer workflow** (runs asynchronously per application):
   - Retrieves job data via `ApplicationManagement.get_application_data(application_id)`
   - Retrieves user data via `ProfileManagement.get_user_profile(user_id)`
   - Generates CV + Cover Letter
   - Stores draft via `ApplicationManagement.store_draft()`
   - Updates status via `ApplicationManagement.update_status(application_id, "draft_ready")`
   - **Calls the callback URL** with application_id (see Section 3)

---

### 3. Composer → Orchestrator Callback Flow
**Trigger**: Composer completes generation (success or failure)

**Workflow**:
1. **Composer calls callback URL**: POST to `callback_url` provided in original request
2. **Callback payload** (on success):
   ```json
   {
     "event": "composition_complete",
     "status": "success",
     "application_id": "uuid-app-123",
     "user_id": "uuid-user-456",
     "job_title": "Product Owner",
     "company": "Manor AG",
     "timestamp": "2026-01-19T14:30:00Z"
   }
   ```
   Or (on failure):
   ```json
   {
     "event": "composition_failed",
     "status": "error",
     "application_id": "uuid-app-123",
     "user_id": "uuid-user-456",
     "error_code": "insufficient_profile_data",
     "message": "User profile has <3 work experiences",
     "timestamp": "2026-01-19T14:30:00Z"
   }
   ```

3. **Orchestrator receives callback**:
   - Uses `application_id` to identify which application completed
   - If success: Send email notification to user ("New CV/Cover Letter ready for [Job Title] at [Company]")
   - If error: Log error and send alert to admin

**Benefits of async + callback pattern**:
- Orchestrator can trigger multiple compositions in parallel (different job applications)
- No timeout issues for long-running compositions
- Composer can process at its own pace
- Orchestrator remains responsive

---

### 4. User → Composer Iteration Flow (Also Asynchronous)
**Trigger**: User requests regeneration or approval

**Workflow**:
- **Regenerate**:
  - User provides feedback reasons via UI
  - Orchestrator calls Composer (async): POST /composer/regenerate
  - Payload: `{application_id, user_id, feedback_reasons[], callback_url}`
  - Composer regenerates and calls callback when done

- **Edit**:
  - User makes inline edits in UI
  - UI directly calls `ApplicationManagement.store_edited_draft()`; this is the mechanism that transitions the application to `edited`
  - No Composer or Orchestrator involvement

- **Approve**:
  - Orchestrator calls Composer (async): POST /composer/approve
  - Payload: `{application_id, user_id, callback_url}`
  - Composer generates PDFs, updates status to "approved", calls callback
  - Orchestrator receives callback and sends confirmation email with PDF download links

---

### 5. Orchestrator → AdapterAgent Flow
**Trigger**: Nightly cron (2am UTC)

**Workflow**:
1. Cron triggers AdapterAgent
2. AdapterAgent retrieves approved applications via `ApplicationManagement.get_application_history(user_id, {status: "approved", approved_after: last_run_timestamp})`
3. AdapterAgent analyzes patterns and updates style preferences via `ProfileManagement.update_style_preferences(user_id, preferences)`
4. Next Composer generation uses updated preferences

---

## Technology Stack
- **n8n workflows**: Scheduling, polling, webhook triggers
- **MCP Tools**: All data access abstracted through ProfileManagement and ApplicationManagement tools
- **Webhooks**: Agent-to-agent communication

---

## Notes
- All agents access data exclusively through MCP tools (no direct storage access)
- Storage backend (database, Google Sheets, etc.) is abstracted within MCP tool implementations
- Orchestrator is stateless - relies on MCP tools for state management
