# Composer Agent

1. #### Objective

##### Problem Statement

Job seekers face a time-quality tradeoff: either spend 30-45 minutes tailoring each application (high quality, low volume) or submit generic CVs (low quality, high volume). This results in application fatigue and missed opportunities.

##### Agent Purpose

Composer Agent generates job-specific, ATS-optimized CV and Cover Letters that maintain 100% factuality while achieving 80%+ relevance match to the target job description, saving precious time to the job hunters while increasing chances of interviews.

##### Agent Identity:

- **Role Identity**: CV and Career expert Writer  
- **Cognitive Tone**: Professional, factual, articulate, user-aligned (writes in user's voice), European Business tone.  
- **Base Temperature**: 0.3 (lower \= more factual, less creative).

High Level User Workflow:

1. A new matching opportunity arrives for the user.  
2. Composer Agent generates drafts (Markdown format for easy editing).  
3. User reviews side-by-side with job description.  
4. User iterates:  
   1. **Regenerate**  
   2. **Edit inline**  
      Both options above optionally with feedback reasons:  
      \- “Not factual”;  
      \- “Not matching / tailored to job enough”;  
      \- “Not my voice”;  
      \- “I just did not like it”.  
   3. **Approve**.  
5. If Regenerate → Generate new draft CV and Cover Letter, considering the feedback from the user.  
6. In case of Edit → Feed the AdapterAgent with original draft and user-edited version.  
7. In case of Regenerate or Edit inline: Save new draft in database.  
8. User keeps iterating on the CV / Cover Letter until **approval**.  
9. Upon approval: Generate final PDFs (CV \+ Cover Letter)  
10. PDFs stored with application data and available to the user  
11. User downloads and manually submits

2. #### Desired Outcomes

**System Outcomes**

- CV and Cover Letter generated in PDF format  
- Documents stored with application details in database  
- Available to user for download

**Quality Outcomes**

- Factuality: 100% claims supported by user profile (0% fabrication)  
- Relevance: ≥80% match score (CV/Cover Letter aligned to job description)  
- ATS Optimization: Key skills and requirements from job description naturally integrated  
- Usability: ≤5 minutes of user editing required  
- Voice alignment: "Sounds like me" feedback \>90%

**User Outcomes**

- User confirms satisfaction with generated content  
- User successfully downloads PDFs  
- User proceeds to application submission

3. #### Health Metrics

**Quality Metrics** (output evaluation):

- **Factuality Score**: 100% claims supported by user profile.  
  - Measured via: Automated fact-checking against profile data.  
- **Match Score**: ≥80% CV/Cover Letter relevance to job description.  
  - Measured via: LLM-as-judge (simulating ATS scoring).  
  - Evaluation: Via both, a test set (offline) and live generation (online monitoring).  
- **Voice Authenticity**: \<10% "doesn't sound like me" reports (after first 3 applications)  
  - Measured via: User feedback for each generation

**Performance Metrics** (operational):

- **Generation Latency**: \<10s per document (p95)  
- **First-Approval Rate**: ≥70% users approve without regeneration  
- **Edit Changes**: User edits represent \<10% of the generated CV / Cover Letter.  
- **Regeneration Rate**: \<30% of generations require regeneration

**Reliability Metrics** (system health):

- **LLM API Success Rate**: ≥99% successful calls  
- **Fallback Rate**: \<1% fallback to template-based generation  
- **Fact-Check Pass Rate**: ≥95% generations pass first validation

**Cost Metrics**:

- **Cost per Generation**: \<€0.10 per CV+Cover Letter pair (at 0.3 temperature, GPT-4o-mini; For the buildathon demo, we will use gemini-2.5-flash(-lite?) on the free tier).

**Monitoring Strategy**:

- Real-time: Match score and Factuality score calculated on each generation  
- Async: LLM-as-judge evaluation runs on sample (10% of generations) for quality audit

4. #### Strategic Context

##### System Context

**Upstream Dependencies** (what Composer receives):

- **From Matcher Agent** (automatic trigger):  
  - New high-quality match found (score ≥80)  
  - Match score (0-100)  
  - Match explanation (why job fits user)  
  - Skills gap analysis (matched vs. missing skills)  
  - Job description (company, title, location, full description, salary)  
- **From Database**:  
  - User profile (structured format with parsed experience, achievements, skills)  
  - **Baseline CV**: Original CV stored during onboarding (parsed into structured format, constant reference)  
  - Previous draft iterations for this specific job (if user requested regeneration), with:  
    - Draft CV / Cover Letter  
    - Factuality score  
    - Match score of CV / Cover Letter \- Job  
    - Reasons from the user for edit / regeneration (to better adapt in next iteration)  
- **From AdapterAgent** (cross-job learning):  
  - User style profile (tone, formality)  
  - Document generation preferences learned from past edits  
    - Past edits and reasons for the edits

**AdapterAgent Integration (Shared Database Architecture)**:

- **Composer → AdapterAgent** (writes on user approval):  
  - Table: `composer_feedback`  
  - Stores per USER \+ JOB (specific application):  
    - Original draft (CV \+ Cover Letter in Markdown)  
    - User-edited final version (Markdown, if user made edits; NULL otherwise)  
    - User feedback reasons (if provided): \["not my voice", "not matching enough", etc.\]  
    - Factuality score (0-100%)  
    - Match score (CV/Cover Letter \- Job, 0-100%)  
    - Timestamp of approval  
  - Purpose: Raw feedback data for AdapterAgent to learn from

- **AdapterAgent → Composer** (writes nightly batch):  
  - Table: `user_style_profiles`  
  - Stores per USER:  
    - Learned style preferences:  
      - Tone (e.g., "analytical", "narrative", "conversational")  
      - Formality (0.0-1.0 scale)  
      - Metrics density (preference for quantified achievements)  
      - Leadership emphasis (0.0-1.0 scale)  
      - Generic skills usage (0.0 \= specific, 1.0 \= generic)  
    - Last updated timestamp  
    - Sample size (number of approved documents analyzed)  
    - Confidence level (statistical confidence in this profile)  
  - Purpose: Style preferences used by Composer for next job generation


- **Data Flow**:  
  1. **Initial Generation**:  
     - Composer reads `user_style_profiles` WHERE user\_id \= X (if exists) → injects into LLM prompt  
     - Composer generates draft (CV \+ Cover Letter)  
     - Composer calculates factuality score \+ match score  
     - Composer writes to `draft_iterations` table: draft, scores, status \= "draft\_ready", version \= 1  
     - User notified via email

     

  2. **User Review \- Regenerate Loop** (if user requests):  
     - User provides feedback reasons: \["not my voice", "not matching enough"\]  
     - Composer reads previous iteration from `draft_iterations` (version N)  
     - Composer writes feedback reasons to `draft_iterations` (version N)  
     - Composer generates NEW draft using feedback \+ previous iteration context  
     - Composer calculates new scores  
     - Composer writes to `draft_iterations`: new draft, new scores, status \= "draft\_ready", version \= N+1  
     - User reviews new version (can loop back to step 2\)

     

  3. **User Review \- Edit Loop** (if user edits inline):  
     - User makes text edits directly in Markdown editor  
     - User optionally provides reasons: \["not factual", "didn't like wording"\]  
     - Composer reads current draft from `draft_iterations` (version N)  
     - Composer writes to `draft_iterations`: original draft (unchanged), edited version, edit reasons, version \= N (updated)  
     - User can still regenerate (go to step 2\) or approve (go to step 4\)

     

  4. **User Approval**:  
     - User clicks "Approve"  
     - Composer reads final version from `draft_iterations` (latest version)  
     - Composer generates PDFs  
     - Composer writes to `composer_feedback` table:  
       - Original draft (first generated version)  
       - User-edited final version (if edited; NULL if not)  
       - All user feedback reasons (aggregated from all iterations)  
       - Final factuality \+ match scores  
       - Timestamp of approval  
     - Composer updates status \= "approved" in `draft_iterations`

     

     

  5. **AdapterAgent Learning** (nightly batch, 2am UTC):  
     - AdapterAgent reads `composer_feedback` WHERE approved\_at \> last\_run\_timestamp  
     - For each user with ≥3 approved documents:  
       - AdapterAgent analyzes: original vs edited versions, feedback reasons  
       - AdapterAgent extracts style patterns (tone, formality, metrics density)  
     - AdapterAgent updates `user_style_profiles` with learned preferences

     

  6. **Next Job Generation**:  
     - Matcher finds new match  
     - Composer reads updated `user_style_profiles` → improved style alignment  
     - Go to step 1 (but now with learned preferences)


- **Ownership Rules**:  
  - AdapterAgent is **sole writer** to `user_style_profiles` (Composer read-only)  
  - Composer is **sole writer** to `composer_feedback` (AdapterAgent read-only)  
  - Clear boundaries prevent data conflicts

**Core Tools & Access**:

- **LLM API**: GPT-4o-mini (production) / Gemini 2.5 Flash (buildathon demo)  
  - Temperature: 0.3 (factuality prioritized)  
- **Fact-Check Module**: Internal validation (claims vs. profile data)  
  - Runs automatically before exposing draft to user  
- **Match Scorer**: LLM-as-judge (ATS simulation scoring)  
  - Runs automatically before exposing draft to user  
- **PDF Generator**: Markdown → PDF conversion (on user approval)  
- **Database**: Read/Write access  
  - **Read**: (See Upstream above)  
  - **Write**: (See Downstream here below)

**Automatic Generation Workflow**:

1. **Trigger**: Matcher Agent finds high-quality match (score ≥80)  
2. Composer generates CV \+ Cover Letter draft (Markdown) automatically  
3. Calculate factuality score (automated fact-check against profile)  
4. Calculate match score (LLM-as-judge ATS simulation)  
5. **IF scores fail (factuality \<99% OR match \<80%)**:  
   - Regenerate with adjusted prompt (loop max 2-3 times)  
   - If still failing → escalate (see Stop Rules)  
6. **IF scores pass**: Store draft in database with status \= "draft\_ready"  
7. Notify user via:  
   - Email for first draft version ("New CV/Cover Letter ready for Job X at Company Y").  
   - Via n8n webhook on subsequent iterations

**User Review & Iteration Loop** (when user has time):

1. User opens draft (side-by-side with job description)  
2. User provides action \+ optional feedback:  
   - **Regenerate** with optional reasons:  
     - "Not factual"  
     - "Not matching / tailored to job enough"  
     - "Not my voice"  
     - "I just did not like it"  
   - **Edit inline** (Markdown editor) with optional reasons (same as above):  
     - User makes direct text edits  
     - User can specify WHY they edited (helps AdapterAgent learn)  
   - **Approve**: Lock draft, generate PDFs  
3. If Regenerate: Return to step 2 of Automatic Generation (inner loop)  
4. If Edit: Save edited version \+ feedback reasons, user can approve or regenerate again  
5. If Approve: Generate PDFs, update status \= "approved", store with application data

**Downstream Outputs**:

- **To User (via n8n webhook)**:  
  - Draft completion notification (automatic, after generation, via email)  
  - Approval confirmation (with download link for the PDFs)  
- **To Database**:  
  - Application status updates: "draft\_ready" → "approved" → "downloaded" → "applied"  
  - Store drafts (Markdown), metadata (scores, timestamp, version), final PDFs, application status  
  - This draft iteration for this specific job with:  
    - CV / Cover Letter (in internal format)  
    - Factuality score  
    - Match score of CV / Cover Letter \- Job  
    - Timestamp  
    - Version  
    - If this version was from a user edit / regeneration: Reasons from the user  
- **To AdapterAgent** (post-approval, cross-job learning):  
  - Original draft and user-edited final version  
  - User feedback reasons (if provided during regeneration or editing)  
  - Factuality \+ Match scores  
- **To Health Monitoring System**:  
  - Factuality score, match score, generation latency, cost per generation  
  - Regeneration attempts, approval rate, edit distance

**Data Flow Summary**:  
Matcher (Finds a Match) → Composer (auto-generates) → User (reviews later, iterates with Composer in a loop) → User (edits/approves) → Composer (generates PDF) → AdapterAgent (learns) → Feeds User Profile for Composer to better adapt on the next job generation

**Important Notes**:

- **Automatic generation**: User does NOT trigger generation. Composer generates automatically when Matcher finds a good match.  
- **Baseline CV**: Constant CV reference from the onboarding, available in User Profile

**Excluded from MVP** (Post-MVP features):

- **Company research tool**: External data (Glassdoor, LinkedIn, company news) to personalize cover letter intro  
- **RAG system for user voice**: Store/query approved past documents as reference examples.

##### Organizational Context

**Business Model**: B2C SaaS for EU job seekers  
**Brand Promise**: Quality-first automation

- "Your authentic voice, AI-enhanced" (not generic templates)  
- "Factual, tailored to the job and ATS-optimized CV and Cover Letter, to increase the chances of an interview"

##### Trade-off Priorities

**Priority Order**: Factuality (Trust) \> Matching/Tailoring \> Speed \> Cost  
**Rationale**:

1. **Factuality \> Matching**:  
   - Fabricated claims \= user reputation damage, potential job loss (HIGH blast radius)  
   - Poor tailoring \= lower interview rate but user can edit (MEDIUM impact, recoverable)  
   - **Decision**: If forced to choose, generate less tailored but 100% factual document  
2. **Matching \> Speed**:  
   - 80%+ match score \= higher ATS pass rate and interview likelihood  
   - Slow generation \= user friction (acceptable since it's automatic/background)  
   - **Decision**: Invest 2-3s extra for match scoring before output (validate before showing)  
3. **Speed \> Cost**:  
   - Background generation: User doesn't wait, so \<10s is comfortable  
   - Cost: €0.10 per generation is sustainable  
   - **Decision**: Use GPT-4o-mini (faster \+ cheaper) vs. GPT-4o (slower \+ expensive)  
     Gemini-2.5-flash-(lite) will be used during the demo at the Buildthaton.

**Edge Case \- Factuality vs. Matching Conflict**:

- If inner loop fails both (factuality \<99% AND match \<80% after 3 attempts) → Escalate (see Stop Rules)

5. #### Constraints

##### Steering Constraints (LLM-level):

- Do NOT fabricate facts from the user (Experience, Skills, Achievements, etc.)  
- Do NOT make unsupported claims (e.g., "led team of 50" if profile says "team of 5")  
- Do NOT use clichés ("rockstar", "ninja", "guru", "10x engineer", "passionate self-starter")  
- MUST include ≥2 quantified achievements from user profile  
- MUST use British English spelling (optimise, organisation, analyse, etc.)  
- MUST use European business tone (formal but warm, not American colloquial)  
- MUST optimize for ATS systems (naturally integrate keywords from job description)  
- MUST stay within desired length by user (Default: 2 pages total for CV \+ Cover Letter)

##### Hard Guardrails (System-enforced):

**Quality Guardrails**:

- If CV/Cover Letter fact-check validation not passed (\>1% unsupported claims) → Regenerate with:  
  - Reduce temperature by 10% (do not go lower than 0.2)  
  - Stricter prompt emphasizing factuality  
- If CV/Cover Letter \- Job Description match \<80% → Regenerate with:  
  - Enhanced prompt focusing on keyword alignment and tailoring  
- After 3 consecutive attempts failing both factuality AND match quality → STOP (see Section 7 Stop Rules)

**Dependency Guardrails** (graceful degradation only \- critical failures in Section 7):

- Cannot access baseline CV → Use profile text only (graceful degradation, log warning)  
- Cannot access previous iterations (if regenerating) → Start fresh from version 1 (graceful degradation)  
- Cannot access AdapterAgent style profile → Skip style preferences, use baseline only (graceful degradation)

**Data Integrity Guardrails**:

- Ensure CV is not empty (minimum 100 words) → If fails, STOP (see Section 7\)  
- Ensure Cover Letter is not empty (minimum 150 words) → If fails, STOP (see Section 7\)  
- Ensure both factuality score AND match score are calculated before exposing draft → If fails, STOP (see Section 7\)  
- Ensure version numbering is sequential (no gaps) → If fails, STOP (see Section 7\)

6. #### Decision Types and Autonomy:

**Risk**: Generate user-facing content representing professional identity. Risks of not being factually correct, or not tailored enough for the job description.  
**Reversibility**: YES (drafts never auto-used, user can edit/discard)  
**Blast Radius**: HIGH if unchecked and actually sent (fabricated claims damage credibility, could lead to job loss post-hire)  
**Autonomy Decision**: Proposal-First: Human-In-The-Loop Required (Generate Bucket): The agent generates autonomously, humans need to approve and send it.

7. #### Stop Rules:

**Critical Data Access Failures** (cannot recover):

- STOP if cannot access user profile → Escalate error: "Critical dependency unavailable \- user profile required for generation"  
- STOP if cannot write to database (draft\_iterations table) → Escalate error: "Data loss risk \- unable to persist drafts. Check database connection."

**Generation Quality Failures** (exhausted all attempts):

- STOP if user profile has \<3 work experiences/achievements → Escalate to user: "Insufficient profile data for quality generation. Please add at least 3 work experiences with achievements to your profile."  
- STOP if after 3 consecutive regeneration attempts, both conditions fail:  
  - Factuality \<99% (\>1% unsupported claims) AND  
  - Match score \<80% → Escalate to user: "Unable to generate document that is both factual and well-matched to the job. Possible causes: incomplete profile, job requirements too specific, or mismatch between your background and role. Please review your profile or manually edit."

**System Failures** (core functionality unavailable):

- STOP if LLM API fails after 3 retries → Fallback to template-based generation \+ Escalate error to admin: "LLM service unavailable \- using basic template fallback"  
- STOP if Fact-Check Module fails → Escalate error to admin: "Cannot validate factuality \- safety mechanism unavailable. Generation blocked."  
- STOP if Match Scorer (LLM-as-judge) fails → Escalate error to admin: "Cannot score relevance \- quality check unavailable. Generation blocked."

**Data Integrity Failures** (output validation failed):

- STOP if generated CV is empty (CV \<100 words) → Escalate error: "Generation produced empty CV output"  
- STOP if generated Cover Letter is empty (Cover Letter \<150 words) → Escalate error: "Generation produced empty Cover Letter output"  
- STOP if version numbering breaks (non-sequential or duplicate) → Escalate error: "Data consistency issue detected \- version conflict in draft\_iterations table"

**Note**: Graceful degradation scenarios (e.g., cannot access baseline CV, cannot access AdapterAgent style profile, cannot access previous iterations) do NOT trigger STOP \- see Section 5 Dependency Guardrails for fallback behavior.  
