# MCP Tools - CareerAgent System

## Overview
Common tools accessible via MCP (Model Context Protocol) for all agents in the CareerAgent system. These tools abstract data storage and retrieval, allowing agents to remain agnostic to the underlying storage backend (PostgreSQL, Google Sheets, etc.).

---

## 1. ProfileManagement

**Purpose**: Centralized access to user profile data.

**Capabilities**:
- Read user profile (structured experience, achievements, skills)
- Read baseline CV (original CV from onboarding, parsed format)
- Read user style preferences (learned by AdapterAgent)
- Update user profile fields
- Update style preferences

**Operations**:

### `get_user_profile(user_id)`
**Returns**: Structured user profile data
```json
{
  "user_id": "uuid",
  "personal_info": {
    "name": "John Doe",
    "email": "john@example.com",
    "location": "Basel, Switzerland"
  },
  "experiences": [
    {
      "company": "Manor AG",
      "title": "Product Owner",
      "duration": "2020-2023",
      "achievements": [
        "Led team of 5 developers",
        "Increased conversion by 25%"
      ]
    }
  ],
  "skills": ["Product Management", "Agile", "Jira", "SAP Commerce"],
  "education": [...],
  "certifications": [...]
}
```

### `get_baseline_cv(user_id)`
**Returns**: Original CV from onboarding (parsed into structured format, constant reference)
```json
{
  "user_id": "uuid",
  "cv_markdown": "# John Doe\n\n## Experience\n...",
  "parsed_sections": {
    "header": "...",
    "experience": "...",
    "skills": "..."
  }
}
```

### `get_style_preferences(user_id)`
**Returns**: Learned style preferences from AdapterAgent
```json
{
  "user_id": "uuid",
  "tone": "analytical",  // or "narrative", "conversational"
  "formality": 0.75,  // 0.0-1.0 scale
  "metrics_density": 0.80,  // preference for quantified achievements
  "leadership_emphasis": 0.65,  // 0.0-1.0 scale
  "generic_skills_usage": 0.20,  // 0.0 = specific, 1.0 = generic
  "sample_size": 8,  // number of documents analyzed
  "confidence": 0.85,  // statistical confidence 0.0-1.0
  "last_updated": "2026-01-18T02:15:00Z"
}
```
**Note**: Returns `null` if user hasn't approved ≥3 documents yet (insufficient data for learning).

### `update_user_profile(user_id, fields)`
**Purpose**: Update specific profile fields
**Access**: Restricted (typically only via UI or onboarding flow)

### `update_style_preferences(user_id, preferences)`
**Purpose**: Update learned style preferences
**Access**: Restricted to AdapterAgent only

**Data Storage**: Abstracted (tool handles storage backend internally)

---

## 2. ApplicationManagement

**Purpose**: Manages individual user-job applications and tracks application status throughout the workflow.

**Application Statuses**:
- `new_match` - New high-quality match found by Matcher, not yet processed by Composer
- `draft_ready` - Initial generation complete, awaiting user review
- `regenerating` - User requested regeneration with feedback
- `edited` - User made inline edits
- `approved` - User approved, PDFs generated
- `downloaded` - User downloaded PDFs
- `applied` - User submitted application externally

**Operations**:

### `create_application(user_id, job_id, match_data)`
**Purpose**: Initialize application record when Matcher finds new high-quality match
**Parameters**:
```json
{
  "user_id": "uuid",
  "job_id": "string",  // from Matcher's Google Sheet
  "match_data": {
    "company": "Manor AG",
    "job_title": "Product Owner",
    "location": "Basel, Switzerland",
    "job_url": "https://...",
    "job_description": "Full job description text...",
    "match_score": 88,
    "match_summary": "Strong fit based on product management experience and Swiss market knowledge",
    "skills_keywords": "Product Management, Agile, Scrum, Jira, Stakeholder Management",
    "salary_text": "CHF 100k-120k"
  }
}
```
**Returns**: `application_id` (UUID)

### `get_application_data(application_id)`
**Purpose**: Retrieve job and match data for a specific application
**Returns**:
```json
{
  "application_id": "uuid",
  "user_id": "uuid",
  "job_id": "string",
  "company": "Manor AG",
  "job_title": "Product Owner",
  "location": "Basel, Switzerland",
  "job_url": "https://...",
  "job_description": "Full text...",
  "match_score": 88,
  "match_summary": "Strong fit based on...",
  "skills_keywords": "Product Management, Agile, Scrum, Jira",
  "salary_text": "CHF 100k-120k",
  "status": "new_match",
  "created_at": "2026-01-19T10:00:00Z"
}
```

### `store_draft(application_id, draft_data)`
**Purpose**: Store draft iteration (CV/Cover Letter version)
**Parameters**:
```json
{
  "application_id": "uuid",
  "version": 1,
  "cv_markdown": "# John Doe\n\n...",
  "cover_letter_markdown": "Dear Hiring Manager...",
  "factuality_score": 99.5,
  "match_score": 87.0,
  "feedback_reasons": null  // or ["not my voice", "not matching enough"] if regeneration
}
```

### `get_draft_iterations(application_id)`
**Purpose**: Retrieve all draft versions for an application (for regeneration context)
**Returns**: Array of draft versions (latest first)

### `store_feedback(application_id, version, feedback_reasons)`
**Purpose**: Store user feedback reasons when regenerating or editing
**Parameters**:
```json
{
  "application_id": "uuid",
  "version": 2,
  "feedback_reasons": ["not my voice", "not matching enough"]
}
```

### `update_status(application_id, new_status)`
**Purpose**: Update application status
**Parameters**: `application_id`, `new_status` (from status enum above)

### `store_final_pdfs(application_id, cv_pdf, cover_letter_pdf)`
**Purpose**: Store approved PDFs (on user approval)
**Parameters**: Binary PDF data or file paths

### `get_application_history(user_id, filters)`
**Purpose**: Retrieve application history for learning (used by AdapterAgent)
**Parameters**:
```json
{
  "user_id": "uuid",
  "status": "approved",  // optional filter
  "approved_after": "2026-01-10T00:00:00Z"  // optional
}
```
**Returns**: Array of applications with all iterations, edits, and feedback

**Data Storage**: Abstracted (tool handles storage backend internally)

---

## Future Tools (Placeholder)

### 3. CompanyResearchTool (Post-MVP)
- TBD: Glassdoor, LinkedIn, news APIs for company insights
