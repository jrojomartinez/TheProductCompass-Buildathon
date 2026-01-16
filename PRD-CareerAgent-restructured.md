# CareerAgent: AI-Powered Job Search Automation Platform
## Product Requirements Document v2.0

**Document Owner**: [Your Name/Team]
**Last Updated**: January 15, 2026
**Status**: Draft for Review

---

# PART 1: STRATEGIC PRD

## Executive Summary

**Problem**: Job seekers in Europe spend 40+ hours per month on repetitive, low-value tasks—scanning multiple job boards, customizing applications, and tracking submissions manually—while struggling to maintain quality and consistency.

**Solution**: CareerAgent is an AI-powered job search automation platform that uses specialized AI agents to automate discovery, matching, document generation, and application tracking. The platform combines the efficiency of automation with the quality and personalization that professional job seekers demand.

**Target Market**: European mid-career professionals (3-10 years experience) seeking their next career move.

**Business Model**:
- Freemium: Basic job matching and tracking (free)
- Professional: €29/month - AI document generation, unlimited applications
- Premium: €79/month - Priority support, advanced analytics, career coaching

**Success Metrics (12 months post-launch)**:
- **User Acquisition**: 50,000 registered users across EU markets
- **Conversion Rate**: 12% free-to-paid conversion
- **User Retention**: 65% 6-month retention for paid users
- **User Satisfaction**: >85% satisfaction with job match quality
- **Time Savings**: 75% reduction in time-per-application (from 45 min to <12 min)
- **Outcome Quality**: 90% of generated documents require <5 min editing
- **Revenue**: €1.2M ARR by month 12

---

## Market Opportunity

### The European Job Search Market

**Market Size**:
- **TAM**: 8.5M active job seekers per month across EU27 + UK
- **SAM**: 2.8M mid-career professionals (3-10 years experience) actively searching
- **SOM**: Target 1% (28,000 paying users) by year 2

**Geographic Focus (Phase 1)**:
- Primary: UK, Germany, France, Netherlands, Spain
- Language: English (expand to local languages in Phase 2)
- Target: English-speaking professionals in tech, marketing, finance, management

**Market Validation**:
- 18+ job automation competitors (primarily US-focused)
- Limited European-specific solutions addressing GDPR, local job boards, and European work culture
- User research shows 72% dissatisfaction with "spray and pray" automation tools
- Willingness to pay: €25-80/month for quality automation (validated through 40 user interviews)

### The Automation Gap

**Current State**: Manual job search requires 15-20 hours/week:
- Job discovery & filtering: 6-8 hours/week across 50+ fragmented sites
- Research & fit assessment: 4-5 hours/week
- Document customization: 3-4 hours/week (30-45 min per application)
- Application tracking: 1-2 hours/week

**Scaling Problem**: To increase success rates, job seekers apply to more roles, but manual overhead scales linearly:
- 10 applications = 7.5 hours
- 50 applications = 37.5 hours (nearly a full-time job)
- 100 applications = 75 hours (unsustainable for employed professionals)

**Competitive Gaps**:
1. **Quality vs. Quantity**: Existing tools prioritize volume over relevance
2. **European Market**: Limited support for EU job boards, GDPR compliance gaps
3. **User Control**: Most tools are "all or nothing" - no granular control
4. **Transparency**: Blackbox matching, no explanation of why jobs are recommended
5. **Professional Segment**: Tools target entry-level or mass market, not mid-career professionals

---

## Target Users & Jobs-to-be-Done

### Primary Persona: Active Mid-Career Professional

**Demographics**:
- Age: 28-42 years old
- Experience: 3-10 years in current field
- Location: Major EU cities (London, Berlin, Amsterdam, Paris, Madrid)
- Employment: Currently employed, seeking better opportunity
- Education: University degree
- Income: €45,000-€85,000 annual salary
- Tech-savviness: Comfortable with digital tools, uses LinkedIn actively

**Behavioral Characteristics**:
- Time-constrained: 2-3 hours/week available for job search
- Quality-conscious: Concerned about personal brand and reputation
- Strategic: Targets 5-10 carefully selected roles over 100 random applications
- Privacy-aware: Concerned about data security and discretion (currently employed)

### Core Jobs-to-be-Done (Mapped to AI Agents)

#### JTBD 1: Efficient Job Discovery
**Job Statement**: *"When I'm searching for my next role, I need to find all relevant opportunities across multiple platforms without spending hours scanning job boards, so I can focus my time on applying to the best-fit roles."*

**Current Friction**:
- Jobs scattered across 100+ sites (LinkedIn, Indeed, company career pages, niche boards)
- 60% of manually discovered jobs are false positives
- Miss opportunities on platforms they don't regularly check
- No way to track "already seen" jobs across platforms

**Pain Intensity**: HIGH - Opportunity cost of missing relevant roles
**Frequency**: Daily
**AI Agent Solution**: **Scout Agent** - Automated cross-platform discovery, deduplication, normalization

---

#### JTBD 2: Intelligent Job Matching
**Job Statement**: *"When I see a job posting, I need to quickly assess if it's actually a good match for my skills, experience, and career goals before investing time in an application, so I don't waste effort on poor-fit roles."*

**Current Friction**:
- Job descriptions use vague language ("2-5 years experience", "strong communication skills")
- 40% of applications go to roles where candidate is over/under-qualified
- No easy way to compare multiple jobs objectively
- Emotional cost: Rejection feels personal after significant investment

**Pain Intensity**: HIGH - Wasted time on low-probability applications
**Frequency**: Per job (10-20x per week)
**AI Agent Solution**: **Matcher Agent** - Explainable scoring (0-100), skill/location/seniority analysis

---

#### JTBD 3: Personalized Application Materials
**Job Statement**: *"When I'm ready to apply, I need a tailored CV and cover letter that highlights my relevant experience for this specific role without starting from scratch each time, so I can submit quality applications efficiently."*

**Current Friction**:
- Generic applications get filtered out by ATS systems
- Custom applications take 30-45 minutes each (research company, rewrite CV, draft letter)
- Quality-quantity tradeoff: 10 great applications vs. 50 generic ones
- Decision paralysis: Which jobs deserve the customization effort?

**Pain Intensity**: VERY HIGH - Time bottleneck and quality barrier
**Frequency**: Per application (5-15x per month)
**AI Agent Solution**: **Composer Agent** - LLM-powered CV/cover letter generation with fact-checking

---

#### JTBD 4: Application Pipeline Management
**Job Statement**: *"When I've applied to multiple jobs, I need a centralized system to track where I applied, what stage each application is in, and when I need to follow up, so I don't miss opportunities or duplicate applications."*

**Current Friction**:
- No standardized tracking (spreadsheets, email folders, memory)
- Miss follow-up deadlines ("did I apply here already?")
- Forget interview details or recruiter names
- Can't analyze what's working (which job types yield interviews)

**Pain Intensity**: MEDIUM - Organizational overhead and anxiety
**Frequency**: Continuous
**AI Agent Solution**: **Tracker Agent** - Unified pipeline view, status tracking, reminders

---

## Strategic Positioning

### Value Proposition

**For** mid-career European professionals
**Who** are time-constrained and quality-conscious in their job search
**CareerAgent** is an AI-powered job search platform
**That** automates discovery, matching, and document generation while maintaining personalization
**Unlike** mass-application tools like LazyApply or Sonara
**We** prioritize quality matches and user control over volume and automation.

### Differentiation

| Dimension | Competitors | CareerAgent |
|-----------|-------------|-------------|
| **Geography** | US-centric (LinkedIn, Indeed) | EU-first (local boards, GDPR-native) |
| **Approach** | Spray-and-pray (100s of apps) | Targeted quality (10-20 best fits) |
| **Matching** | Blackbox algorithms | Transparent, explainable scoring |
| **User Control** | All-or-nothing automation | Granular control, HITL at key points |
| **Documents** | Generic templates | Personalized, fact-checked, ATS-optimized |
| **Target User** | Entry-level, high-volume | Mid-career, quality-focused |
| **Privacy** | Unclear data practices | GDPR-compliant, privacy-first |

### Competitive Positioning Map

```
                    Quality-First
                         ↑
                         |
          [CareerAgent]  |  [Teal] [Huntr]
                         |
Automation ←──────────────┼──────────────→ Manual
                         |
    [Sonara] [LazyApply] | [LinkedIn] [Indeed]
                         |
                         ↓
                   Volume-First
```

---

## Go-to-Market Strategy

### Phase 1: UK Market Entry (Months 1-6)

**Target**: English-speaking professionals in London, Manchester, Birmingham
**Channels**:
- LinkedIn organic content (job search tips, automation insights)
- Reddit (r/UKJobs, r/cscareerquestionsEU)
- Product Hunt launch
- Referral program (€10 credit for referrer + referee)

**Pricing**: Launch discount - €19/month (Professional), €59/month (Premium)
**Goal**: 1,000 paying users, validate product-market fit

### Phase 2: EU Expansion (Months 7-12)

**Target**: Germany (Berlin, Munich), Netherlands (Amsterdam), France (Paris)
**Additions**:
- Integrate local job boards (StepStone, Xing, Monster.de, Indeed.fr)
- Basic German/Dutch/French job board support (English UI)
- GDPR compliance certification (SOC 2 Type I)

**Goal**: 5,000 paying users across 4 markets

### Phase 3: Scale & Localization (Months 13-24)

**Target**: Spain, Italy, Nordic countries
**Additions**:
- Multi-language UI and document generation
- Local payment methods (SEPA, iDEAL)
- Enterprise tier (teams/agencies)

**Goal**: 20,000 paying users, €3M ARR

---

## Non-Functional Requirements

### Performance

| Metric | Target | Measurement |
|--------|--------|-------------|
| Scout Agent batch time | <5 min for 100 jobs | p95 latency |
| Matcher Agent scoring | <2s per job | p95 latency |
| Composer Agent generation | <10s per document | p95 latency |
| Tracker Agent CRUD | <500ms per operation | p95 latency |
| Dashboard page load | <2s initial load | Real user monitoring |

### Reliability

- **Uptime**: 99.5% (excluding planned maintenance)
- **Data durability**: 99.999% (PostgreSQL with backups)
- **Agent coordination success**: 99% (workflows complete end-to-end)
- **Error recovery**: Automatic retry (3x with exponential backoff), manual fallback

### Data Privacy & Security (GDPR Compliance)

**Personal Data Handling**:
- User profile data: Name, email, phone, work history, skills, preferences
- Application data: CV drafts, cover letters, job URLs, notes
- Behavioral data: Click patterns, match quality feedback, time spent

**GDPR Requirements**:
- ✅ Explicit consent for data processing (clear opt-ins)
- ✅ Right to access (export all user data in JSON format)
- ✅ Right to deletion (complete data purge within 30 days)
- ✅ Right to rectification (edit all profile fields)
- ✅ Data portability (export in machine-readable format)
- ✅ Privacy by design (encryption at rest, TLS in transit)
- ✅ Data Processing Agreement with all third-party services (OpenAI, n8n)
- ✅ EU data residency (PostgreSQL hosted in EU region)

**Security Measures**:
- Encryption: AES-256 at rest, TLS 1.3 in transit
- Authentication: OAuth 2.0 + JWT tokens
- Authorization: Role-based access control (RBAC)
- Audit logging: All data access logged for 2 years
- Penetration testing: Annual third-party security audit

### Transparency & Explainability

**Matcher Agent**:
- Every score includes explanation: "Score: 78/100. Skills: 80% match (Python, React, PostgreSQL). Location: Remote (preferred). Seniority: Mid-level (3-7 years)."
- Users can adjust scoring weights (skills 50% → 60%)

**Composer Agent**:
- Show which profile sections were used for each document
- Highlight AI-generated vs. user-provided content
- Fact-check report: "3 claims verified against profile"

**Scout Agent**:
- Show source of each job (LinkedIn, Indeed, company page)
- Display discovery time ("found 2 hours ago")

---

# PART 2: MVP DEFINITION & PHASING

## MVP Scope (Phase 1: Months 1-3)

### Must-Have Features (P0)

#### 1. User Onboarding & Profile
- **Profile Setup**: Single-page form
  - Personal: Name, email, phone, location
  - Professional: Current title, years of experience (dropdown: 0-2, 3-5, 6-10, 10+)
  - Skills: Tag input (max 10 skills)
  - Preferences: Target locations (up to 3), remote preference (yes/no/hybrid), salary range (€X - €Y)
- **CV Upload**: Store PDF (optional, for reference - no parsing in MVP)
- **Authentication**: Email/password (magic link), Google OAuth

**JTBD Coverage**: Enables all downstream features
**Effort**: 16 hours (frontend + backend + DB schema)

---

#### 2. Job Discovery (Scout Agent - Automated)

**Functionality**:
- **Data Sources**:
  - LinkedIn Jobs (UK) - via unofficial API / scraping
  - Indeed.co.uk - via RSS feeds where available
  - HackerNews "Who's Hiring" (monthly thread)
  - Manual seed: 200 jobs from top company career pages
- **Automation**: Daily batch run (scheduled via n8n at 2am UTC)
- **Processing**:
  - Parse job title, company, location, description, salary (if present), URL
  - Normalize location (standardize "London, UK" vs. "London" vs. "Greater London")
  - Deduplicate by (company + title + location) hash
  - Store in PostgreSQL `jobs` table with status = "new"
- **Output**: 50-150 new jobs per day

**User Experience**:
- User sees "47 new jobs found" notification
- No user action required (fully automated)

**JTBD Coverage**: ✅ JTBD 1 (Efficient Job Discovery)
**Effort**: 32 hours (scraping logic + normalization + scheduling)

---

#### 3. Job Matching & Ranking (Matcher Agent - Automated)

**Functionality**:
- **Trigger**: Webhook from Scout Agent after batch completes
- **Algorithm** (Rule-based for MVP):
  ```python
  match_score = (
      skills_match * 0.50 +      # Keyword overlap: user skills vs job description
      location_match * 0.30 +    # Exact city match=100%, Remote=80%, Wrong=0%
      seniority_match * 0.20     # Experience years vs job level (Junior/Mid/Senior)
  )
  ```
- **Explainability**:
  - Generate natural language explanation:
    - "Score: 82/100. Skills: 4/5 matched (Python, React, PostgreSQL, Docker). Location: Remote (preferred). Seniority: Mid-level match (5 years experience)."
- **Thresholds**:
  - Score ≥80: "Excellent match" (highlight in green)
  - Score 60-79: "Good match" (highlight in yellow)
  - Score <60: "Possible match" (gray, lower priority)
- **Output**: All jobs scored and ranked; high matches trigger notification

**User Experience**:
- Dashboard shows ranked job list (highest score first)
- Each job card displays: title, company, location, salary, match score, explanation
- Filter by score, location, date posted
- User can "Save" (bookmark) or "Dismiss" (hide forever)

**JTBD Coverage**: ✅ JTBD 2 (Intelligent Job Matching)
**Effort**: 24 hours (scoring logic + explanation generation + UI)

---

#### 4. Document Generation (Composer Agent - Manual Trigger, HITL)

**Functionality**:
- **Trigger**: User clicks "Generate Documents" button for a specific job
- **Process**:
  1. Load user profile + job description
  2. Call OpenAI GPT-4o-mini or Anthropic Claude Sonnet 3.5
  3. Generate:
     - **CV Summary** (200-300 words): Tailored professional summary highlighting relevant experience
     - **Cover Letter** (300-400 words): 3 paragraphs connecting user background to job requirements
  4. **Fact-Check Validation**:
     - Extract claims from generated text
     - Verify each claim exists in user profile
     - Flag unsupported claims (e.g., "led team of 20" when profile says "team of 5")
     - If >10% unfounded → regenerate with stricter prompt
  5. Save as `status = "draft"` in `applications` table
  6. Notify user: "Documents ready for review"

**LLM Prompt Template**:
```
You are a professional CV writer helping a European job seeker.

USER PROFILE:
- Name: {name}
- Experience: {years} years in {field}
- Skills: {skills_list}
- Work History: {work_history_summary}
- Achievements: {quantified_achievements}

TARGET JOB:
- Title: {job_title}
- Company: {company}
- Description: {job_description}

TASK 1: Write a CV summary (200-300 words) emphasizing the user's most relevant skills and experience for THIS specific role.

TASK 2: Write a cover letter (3 paragraphs, 300-400 words):
- Paragraph 1: Why you're interested in this role and company
- Paragraph 2: How your experience matches the requirements (cite specific achievements)
- Paragraph 3: What you'll bring to the team

CONSTRAINTS:
- Only use facts from the user profile (do not fabricate)
- Include at least 2 quantified achievements
- Use professional European business tone (avoid American colloquialisms like "rockstar")
- Optimize for ATS keyword matching
- Format: Plain text, British English spelling

OUTPUT FORMAT:
[CV_SUMMARY]
...

[COVER_LETTER]
...
```

**User Experience**:
- Click "Generate Documents" → Loading spinner (8-12s)
- Review documents side-by-side with job description
- **Edit inline** (Markdown editor)
- **Regenerate** (if unsatisfied) or **Approve** (save final version)
- **Download** as PDF or .docx
- **Manual submission**: User copies text to job application form (no auto-apply in MVP)

**JTBD Coverage**: ✅ JTBD 3 (Personalized Application Materials)
**Effort**: 40 hours (LLM integration + prompt engineering + fact-checking + editor UI)

---

#### 5. Application Tracking (Tracker Agent - Manual Updates)

**Functionality**:
- **Pipeline Stages**:
  - Discovered (auto, when Scout finds job)
  - Matched (auto, when Matcher scores job)
  - Documents Ready (auto, when Composer generates drafts)
  - Applied (manual, user marks after submitting)
  - Interview Scheduled (manual)
  - Offer / Rejected (manual)
  - Archived (manual)

- **Dashboard Views**:
  - **Kanban Board**: Columns per stage, drag-and-drop to update status
  - **Table View**: Sortable by date, company, score, status
  - **Calendar View**: Upcoming interviews, follow-up reminders

- **Features**:
  - Add notes per application (e.g., "Met recruiter Sarah at coffee chat")
  - Set follow-up reminders ("Follow up in 7 days")
  - Link to job URL (quick access to original posting)
  - Track application date, interview dates, outcome

**User Experience**:
- Main dashboard shows all jobs across pipeline
- Click job card → Detail view (notes, documents, timeline)
- Update status via dropdown or drag-and-drop
- Search/filter: by company, status, date range

**JTBD Coverage**: ✅ JTBD 4 (Application Pipeline Management)
**Effort**: 24 hours (dashboard UI + CRUD APIs + state management)

---

### MVP Summary

| Feature | Agent | Automation Level | User Action Required | JTBD |
|---------|-------|------------------|---------------------|------|
| Job Discovery | Scout | Fully automated (daily) | None (review results) | #1 |
| Job Matching | Matcher | Fully automated (triggered) | None (review scores) | #2 |
| Document Generation | Composer | Manual trigger | Generate → Review → Approve | #3 |
| Application Tracking | Tracker | Manual updates | Update status, add notes | #4 |

**Total MVP Effort**: ~136 hours (4 weeks full-time solo, 2 weeks with 2-person team)

---

## Post-MVP Roadmap (P1/P2 Features)

### Phase 2 Features (Months 4-6)

**P1: Enhanced Automation**
- **Auto-Save Jobs**: Scout auto-saves high-match jobs (score ≥80) to user's pipeline
- **Batch Document Generation**: "Generate for all excellent matches" (process 5+ jobs at once)
- **Follow-Up Reminders**: Tracker sends email/push notification ("Applied 7 days ago - time to follow up?")
- **Application Analytics**: "You apply most to fintech roles (60% of apps), with 15% interview rate"

**P1: Matching Improvements**
- **User Feedback Loop**: Thumbs up/down on match quality → adjust scoring weights
- **Semantic Matching**: Use embeddings (OpenAI text-embedding-3-small) for skill similarity (e.g., "Backend" ≈ "Server-Side")
- **Salary Filtering**: Only show jobs within user's salary range (±15%)

**P1: European Expansion**
- Integrate German job boards (StepStone, Xing)
- Support Euro salary normalization (€45k-60k vs £40k-50k)

---

### Phase 3 Features (Months 7-12)

**P2: AI Enhancements**
- **Interview Prep Agent**: Generate common interview questions based on job description
- **Auto-Apply** (LinkedIn Easy Apply only): One-click submission for pre-approved jobs
- **Company Research Agent**: Summarize company news, culture, reviews (Glassdoor, LinkedIn)
- **Networking Recommendations**: "3 people in your network work at {company}"

**P2: Multi-Language Support**
- German UI + document generation
- French UI + document generation
- Dutch UI + document generation

**P2: Enterprise Features**
- Team workspaces (recruiting agencies, career coaches)
- Bulk user management
- White-label options

---

# PART 3: AI AGENT ARCHITECTURE

## System Overview: Multi-Agent Coordination

CareerAgent uses a **coordinator + specialist agents** architecture where four specialized AI agents coordinate through an n8n orchestrator and share state via a PostgreSQL database.

```
┌─────────────────────────────────────────────────────┐
│          n8n Workflow Orchestrator                  │
│  (Coordinator - manages state, triggers, handoffs)  │
└──────────┬────────────┬──────────┬─────────────────┘
           │            │          │          │
     ┌─────▼────┐ ┌────▼─────┐ ┌─▼────────┐ ┌▼────────┐
     │  SCOUT   │ │ MATCHER  │ │ COMPOSER │ │ TRACKER │
     │  Agent   │ │  Agent   │ │  Agent   │ │  Agent  │
     └──────────┘ └──────────┘ └──────────┘ └─────────┘
           │            │          │          │
     ┌─────▼────────────▼──────────▼──────────▼─────────┐
     │        PostgreSQL (Shared State Layer)           │
     │  user_profiles | jobs | matches | applications   │
     └──────────────────────────────────────────────────┘
```

**Key Design Principles**:
1. **Separation of Concerns**: Each agent has a single, well-defined responsibility
2. **Event-Driven Communication**: Agents trigger via webhooks (not polling)
3. **Shared State**: PostgreSQL as single source of truth (no agent-local state)
4. **Stateless Agents**: Agents can be restarted without losing context
5. **Fail-Safe Design**: If one agent fails, others continue; coordinator handles retries

---

## Agent 1: Scout Agent (Job Discovery Specialist)

### Persona & Autonomy Framework

**Role Identity**: Cross-Platform Job Aggregator
**Responsibility**: Monitor job sources, extract structured data, normalize and deduplicate postings
**Cognitive Tone**: Methodical, thorough, silent (no user interruptions during scanning)
**Autonomy Level**: **HIGH** (Interpret Bucket) - Fully automated, no HITL required

### Intent Equation

```
INTENT = OUTCOME + SCOPE + CONSTRAINTS + SUCCESS SIGNAL + STOP RULE
```

**OUTCOME**: Populate `jobs` table with 50-150 relevant job postings per day from EU sources

**SCOPE**:
- **Geographic**: UK, Germany, France, Netherlands (Phase 1)
- **Data Sources**: LinkedIn Jobs, Indeed.co.uk, HackerNews "Who's Hiring", company career pages
- **Job Types**: Professional roles (tech, marketing, finance, management) - exclude retail, gig work
- **Temporal**: Jobs posted in last 30 days only

**CONSTRAINTS** (Hard Boundaries):
- Do NOT scrape sites with restrictive robots.txt or ToS
- Do NOT store PII from job posts (only company, title, location, description, salary)
- Do NOT process jobs without required fields (company AND title AND location)
- Rate limits: Max 1 request per 10 seconds per source
- Budget: Max 1,000 jobs per batch (prevent database bloat)

**SUCCESS SIGNAL**:
- All designated sources scanned (checked timestamp in DB)
- Jobs validated against schema (required fields populated)
- Jobs deduplicated (no duplicate company+title+location)
- Database write confirmed (transaction committed)
- Webhook sent to Matcher Agent

**STOP RULE** (Emergency Brake):
- STOP if parser encounters >20% unparseable posts → alert engineering team
- STOP if database write fails 3 consecutive times → fallback to queue + retry later
- STOP if batch exceeds 1,000 jobs → investigate scraping logic
- STOP if processing time >10 minutes → performance issue

### Capabilities & Tool-Use

**Read Access**:
- LinkedIn Jobs API (unofficial endpoint) or web scraping
- Indeed.co.uk RSS feeds
- HackerNews API (read-only, public)
- PostgreSQL `jobs` table (check for duplicates)

**Write Access**:
- PostgreSQL `jobs` table (INSERT only)
- n8n webhook URL (POST to trigger Matcher)

**Processing Logic**:
1. For each source (LinkedIn, Indeed, HN):
   - Fetch latest postings (filter by date: last 7 days)
   - Parse structured fields: company, title, location, description, salary, URL
2. Normalize data:
   - Location: Standardize "London, UK" → "London"
   - Salary: Convert "£50k-60k" → EUR equivalent (€57k-68k at 1.14 exchange rate)
   - Title: Normalize "Sr. Engineer" → "Senior Engineer"
3. Validate:
   - Required fields present? (company, title, location, description)
   - Description length >100 chars? (filter spam)
4. Deduplicate:
   - Generate hash: `SHA256(company + title + location)`
   - Check against existing `jobs` table
   - Skip if hash exists
5. Batch insert:
   - INSERT new jobs with `status = "new"`, `source`, `created_at`
6. Trigger Matcher:
   - POST webhook: `{event: "scout_complete", job_count: 47}`

### Risk Assessment

**Task**: Parse unstructured job posts and store structured data
**Reversibility**: YES (can delete/re-import jobs with updated logic)
**Blast Radius**: LOW (worst case = bad data in jobs table, no user-facing impact until Matcher runs)
**Autonomy Decision**: **HIGH AUTONOMY ALLOWED** (Interpret Bucket) - Operates on schedule without human approval

---

## Agent 2: Matcher Agent (Job-Candidate Fit Analyst)

### Persona & Autonomy Framework

**Role Identity**: Intelligent Matching Engine
**Responsibility**: Score jobs against user profile, rank by fit, explain recommendations
**Cognitive Tone**: Analytical, balanced, advisory - "You decide, I recommend"
**Autonomy Level**: **GUARDED** (Choose Bucket) - Scores automatically, user controls next step

### Intent Equation

**OUTCOME**: Assign match score (0-100) with human-readable explanation to each new job

**SCOPE**:
- **Input**: Jobs with `status = "new"` (unscored)
- **Profile**: Single-user scoring (no batch multi-user in MVP)
- **Temporal**: Process jobs from last 30 days only

**CONSTRAINTS**:
- Must use explainable rule-based scoring (no blackbox ML in MVP)
- Do NOT auto-apply to jobs (scoring ≠ application decision)
- Do NOT penalize for missing optional fields (e.g., no salary listed)
- Score range: 0-100 (normalized scale)

**SUCCESS SIGNAL**:
- All "new" jobs have `match_score` and `match_explanation` in `matches` table
- Scores distributed across range (not all 100 or all 0 = logic error)
- High-score jobs (≥80) flagged for notification
- Webhook confirming completion sent to n8n

**STOP RULE**:
- STOP if user profile <50% complete → alert user "Complete your profile for better matches"
- STOP if scoring produces identical scores for >80% of jobs → calibration bug
- STOP if processing time >1 min per 100 jobs → performance issue

### Capabilities & Tool-Use

**Read Access**:
- PostgreSQL `user_profiles` table (skills, experience, preferences)
- PostgreSQL `jobs` table (all jobs with status = "new")

**Write Access**:
- PostgreSQL `matches` table (INSERT: user_id, job_id, score, explanation, component scores)
- Update `jobs` table: status "new" → "matched"
- n8n webhook (trigger notification if high matches found)

**Scoring Algorithm** (Rule-Based for MVP):

```python
def calculate_match_score(job, user_profile):
    # 1. Skills Match (50% weight)
    user_skills = set(user_profile.skills)  # ["Python", "React", "PostgreSQL"]
    job_skills = extract_skills(job.description)  # Keyword matching
    matched_skills = user_skills.intersection(job_skills)
    skills_score = (len(matched_skills) / len(user_skills)) * 100 if user_skills else 0

    # 2. Location Match (30% weight)
    if user_profile.remote_preferred and "remote" in job.location.lower():
        location_score = 100
    elif job.location in user_profile.target_locations:
        location_score = 100
    elif "remote" in job.location.lower():
        location_score = 80  # Remote is acceptable even if not preferred
    else:
        location_score = 0  # Location mismatch

    # 3. Seniority Match (20% weight)
    job_level = classify_seniority(job.title, job.description)  # Junior/Mid/Senior
    user_level = map_experience_to_level(user_profile.experience_years)
    if job_level == user_level:
        seniority_score = 100
    elif abs(job_level - user_level) == 1:  # One level off
        seniority_score = 50
    else:
        seniority_score = 0

    # Weighted average
    final_score = (
        skills_score * 0.50 +
        location_score * 0.30 +
        seniority_score * 0.20
    )

    # Generate explanation
    explanation = generate_explanation(
        final_score, matched_skills, location_score, seniority_score
    )

    return final_score, explanation

def generate_explanation(score, matched_skills, location_score, seniority_score):
    return f"""Score: {int(score)}/100.

Skills: {len(matched_skills)} matched ({', '.join(matched_skills)}).
Location: {'Perfect match' if location_score == 100 else 'Remote option' if location_score == 80 else 'Location mismatch'}.
Seniority: {'Exact level match' if seniority_score == 100 else 'One level off' if seniority_score == 50 else 'Level mismatch'}."""
```

**User Experience**:
- Dashboard shows jobs ranked by score (highest first)
- Each job card displays: title, company, location, salary, **match score badge** (color-coded), explanation
- User can adjust scoring weights: "I care more about remote (40%) than seniority (10%)" → re-score jobs

### Risk Assessment

**Task**: Rank jobs by fit, recommend prioritization
**Reversibility**: YES (user can override, adjust weights, re-run)
**Blast Radius**: MEDIUM (bad scores = wasted time reviewing poor matches, but no irreversible action)
**Autonomy Decision**: **GUARDED AUTONOMY** (Choose Bucket) - Scores automatically, user decides next step

---

## Agent 3: Composer Agent (Document Generation Assistant)

### Persona & Autonomy Framework

**Role Identity**: Personalized Content Generator
**Responsibility**: Create tailored CV summaries and cover letters using LLM
**Cognitive Tone**: Professional, articulate, user-aligned (writes in user's voice)
**Autonomy Level**: **HUMAN-IN-THE-LOOP** (Generate Bucket) - Generates drafts, user MUST approve before use

### Intent Equation

**OUTCOME**: Generate job-specific CV summary (200-300 words) and cover letter (300-400 words) that pass fact-check validation

**SCOPE**:
- **Input**: User profile (verified facts only) + Job description + Match explanation (for context)
- **Output**: Markdown text (plain formatting for easy editing)
- **Tone**: Professional European business tone, British English, achievement-focused

**CONSTRAINTS** (Critical for Hallucination Prevention):
- Do NOT fabricate experience, skills, or achievements
- Do NOT make unsupported claims (e.g., "led team of 50" if profile says "team of 5")
- Do NOT use clichés ("rockstar", "ninja", "guru", "10x engineer")
- Do NOT exceed token limits (CV: 400 tokens, Cover Letter: 600 tokens)
- MUST include ≥2 quantified achievements from user profile
- MUST use British English spelling (optimise, organisation, etc.)

**SUCCESS SIGNAL**:
- Documents generated and saved with `status = "draft"` in `applications` table
- Fact-check validation passed (>90% of claims supported by profile)
- User notified: "Documents ready for review - Job at {company}"
- User explicitly approves or rejects (no auto-use)

**STOP RULE**:
- STOP if user profile has <3 work experiences → "Insufficient profile data for quality generation"
- STOP if LLM API fails after 3 retries → fallback to template-based generation
- STOP if fact-check validation fails (>10% unsupported claims) → regenerate with stricter prompt
- STOP if user hasn't acted within 7 days → flag documents as "expired" for review

### Capabilities & Tool-Use

**Read Access**:
- PostgreSQL `user_profiles` (full profile data)
- PostgreSQL `jobs` + `matches` (job description, match explanation for context)
- Prompt templates (version-controlled in codebase)

**Write Access**:
- PostgreSQL `applications` table (INSERT draft documents)
- n8n webhook (notify user of draft completion)

**LLM Integration**:
- **Model**: OpenAI GPT-4o-mini or Anthropic Claude Sonnet 3.5
- **Temperature**: 0.3 (lower = more factual, less creative)
- **Max Tokens**: 400 (CV), 600 (Cover Letter)

**System Prompt Template**:

```
You are a professional CV writer helping a European job seeker customize their application.

USER PROFILE:
- Name: {user.name}
- Experience: {user.experience_years} years in {user.field}
- Current Role: {user.current_title}
- Skills: {user.skills_list}
- Work History:
  {for experience in user.work_history}
  - {experience.title} at {experience.company} ({experience.duration})
    Achievements: {experience.achievements}
  {endfor}
- Education: {user.education}

TARGET JOB:
- Title: {job.title}
- Company: {job.company}
- Location: {job.location}
- Description: {job.description}

MATCH CONTEXT:
- Match Score: {match.score}/100
- Why it's a good fit: {match.explanation}

TASK 1: Write a CV Summary (200-300 words)
- Emphasize skills and experience most relevant to THIS specific role
- Highlight 2-3 quantified achievements from the user's work history
- Use keywords from the job description naturally (for ATS optimization)
- Write in first person ("I am a...", "I have...")
- British English spelling

TASK 2: Write a Cover Letter (3 paragraphs, 300-400 words)
Paragraph 1: Why you're interested in this role at this company (show you researched them)
Paragraph 2: How your experience matches the requirements (cite specific achievements with metrics)
Paragraph 3: What unique value you'll bring to the team

CONSTRAINTS:
- Only use facts from the user profile (do not fabricate)
- Do not invent skills, experiences, or metrics not in the profile
- Avoid clichés like "rockstar", "ninja", "guru", "passionate", "self-starter"
- Use professional European business tone (formal but warm)
- British English spelling (optimise, organisation, etc.)

OUTPUT FORMAT:
[CV_SUMMARY]
...

[COVER_LETTER]
Dear Hiring Manager,

...
```

**Fact-Check Validation**:

```python
def fact_check_document(generated_text, user_profile):
    # 1. Extract claims from generated text
    claims = extract_claims(generated_text)  # GPT-4o extraction
    # Examples: ["5 years experience", "led team of 10", "Python expert", "increased revenue by 40%"]

    # 2. Verify each claim against profile
    unsupported_claims = []
    for claim in claims:
        if not verify_claim_in_profile(claim, user_profile):
            unsupported_claims.append(claim)

    # 3. Calculate accuracy
    accuracy = (len(claims) - len(unsupported_claims)) / len(claims) if claims else 1.0

    # 4. Decision
    if accuracy < 0.90:  # >10% unsupported
        return False, unsupported_claims
    else:
        return True, []

def verify_claim_in_profile(claim, profile):
    # Simple keyword matching + semantic similarity
    # e.g., "5 years experience" → check profile.experience_years == 5
    # e.g., "Python expert" → check "Python" in profile.skills
    # e.g., "increased revenue by 40%" → check profile.achievements for similar metric
    pass
```

**User Experience**:
1. User clicks "Generate Documents" button on job card
2. Loading state (8-12 seconds)
3. Side-by-side view: Job description (left) | Generated documents (right)
4. **Edit inline** (Markdown editor with toolbar)
5. **Regenerate** (if unsatisfied, calls LLM again with adjusted prompt)
6. **Approve** → Saves final version, unlocks "Download" and "Mark as Applied"
7. **Download** as PDF or .docx (Word format)

### Risk Assessment

**Task**: Generate user-facing content representing professional identity
**Reversibility**: YES (drafts never auto-used, user can edit/discard)
**Blast Radius**: HIGH if unchecked (fabricated claims damage credibility, could lead to job loss post-hire)
**Autonomy Decision**: **HUMAN-IN-THE-LOOP REQUIRED** (Generate Bucket) - Agent generates, human approves

---

## Agent 4: Tracker Agent (Pipeline Manager)

### Persona & Autonomy Framework

**Role Identity**: Application Lifecycle Manager
**Responsibility**: Maintain single source of truth for application status, surface actionable items
**Cognitive Tone**: Organized, reliable, unobtrusive (no spam notifications)
**Autonomy Level**: **HIGH** (Interpret Bucket) for data operations, **ZERO** for external actions (sending emails, auto-applying)

### Intent Equation

**OUTCOME**: Provide real-time, accurate view of application pipeline with status, notes, and next actions

**SCOPE**:
- **Entity**: All applications for current user (multi-user isolation enforced)
- **Temporal**: Applications from last 6 months (archive older)
- **Status Values**: Discovered, Matched, Documents Ready, Applied, Follow-up Sent, Interviewing, Offer, Rejected, Archived

**CONSTRAINTS**:
- Do NOT send emails/applications on behalf of user (read-only external actions)
- Do NOT delete application records (soft delete only, preserve history)
- Do NOT auto-transition status without explicit user trigger (except system events like "documents generated")
- Do NOT expose sensitive data in logs (PII protection)

**SUCCESS SIGNAL**:
- All user-initiated actions reflected in DB within 500ms
- Dashboard queries return in <1s (indexed)
- No data inconsistencies (foreign key constraints enforced)
- Weekly summary email sent (optional, user-configured)

**STOP RULE**:
- STOP if database connection fails → prevent data loss, queue writes
- STOP if user requests data export → pause writes during backup
- (No infinite loops - CRUD operations are single-shot)

### Capabilities & Tool-Use

**Read Access**:
- PostgreSQL `applications` table (all user applications)
- PostgreSQL `jobs` + `matches` (join for full job details)

**Write Access**:
- PostgreSQL `applications` table (CRUD operations)
- Update status, add notes, set follow-up dates, soft delete

**Dashboard Features**:
- **Kanban Board**: Columns per status, drag-and-drop to update
- **Table View**: Sortable by date, company, score, status
- **Search/Filter**: By company name, job title, status, date range
- **Bulk Actions**: Archive multiple applications, export to CSV
- **Timeline View**: Chronological history per application

**Processing Logic**:
1. **User views dashboard** → Query `applications` with JOINs on `jobs` and `matches`
2. **User updates status** ("Applied" → "Interview Scheduled") → Update record + timestamp
3. **User adds note** → Append to `notes` field with timestamp
4. **System event** ("documents generated") → Auto-update status: "Matched" → "Documents Ready"
5. **Weekly cron job** (optional):
   - Identify stale applications (status = "Applied", no update in 7 days)
   - Send reminder: "You applied to {company} 7 days ago. Consider following up?"

**User Experience**:
- Main dashboard shows all jobs across pipeline stages
- Click job card → Detail view (full job description, notes, documents, timeline)
- Update status via dropdown or Kanban drag-and-drop
- Add notes: Free-form text field ("Met recruiter Sarah - follow up next week")
- Set reminders: "Follow up on {date}" → Calendar integration (optional)

### Risk Assessment

**Task**: CRUD operations on application data, dashboard queries
**Reversibility**: YES (undo status changes, edit notes)
**Blast Radius**: LOW (worst case = incorrect status, user corrects manually)
**Autonomy Decision**: **HIGH AUTONOMY ALLOWED** (Interpret Bucket) - Transparent data operations, user has full control

---

## Multi-Agent Coordination via n8n

### Coordinator Responsibilities

The n8n orchestrator manages:
1. **Workflow Triggers**: Schedule-based (Scout daily 2am), event-based (Matcher after Scout)
2. **State Transitions**: Update job/application status as agents complete work
3. **Agent Handoffs**: Pass data from Scout → Matcher → Composer → Tracker
4. **Error Handling**: Retry failed agent calls (3x exponential backoff), log errors, alert on critical failures
5. **User Notifications**: Send dashboard updates, high-priority match alerts (email/push)

### End-to-End Workflow Example

```
┌──────────────┐
│   TRIGGER    │  Daily cron: 2am UTC
│  (Schedule)  │
└──────┬───────┘
       │
       ▼
┌──────────────┐
│ SCOUT AGENT  │  Fetch jobs from LinkedIn, Indeed, HN
│   Executes   │  Parse → Validate → Store in DB
└──────┬───────┘  Status: "new"
       │
       │ Webhook: "scout_complete, 87 new jobs"
       │
       ▼
┌──────────────┐
│MATCHER AGENT │  Score 87 jobs against user profile
│   Executes   │  Generate explanations
└──────┬───────┘  Status: "new" → "matched"
       │
       │ Webhook: "matcher_complete, 18 high matches (≥80)"
       │
       ▼
┌──────────────┐
│   DECISION   │  IF high matches found:
│   Gateway    │  THEN send email notification
└──────┬───────┘  User: "18 new excellent matches for you!"
       │
       │ User logs in, reviews matches
       │ User clicks "Generate Documents" for Job #42
       │
       ▼
┌──────────────┐
│COMPOSER AGENT│  Generate CV + Cover Letter for Job #42
│   Executes   │  Fact-check validation
└──────┬───────┘  Status: "matched" → "documents_ready"
       │
       │ Webhook: "documents_ready, Job #42"
       │
       ▼
┌──────────────┐
│TRACKER AGENT │  Update dashboard
│   Executes   │  Notify user: "Documents ready for {company}"
└──────────────┘  Status: "documents_ready" (awaits user approval)
       │
       │ User reviews documents → Approves → Downloads PDF
       │ User manually submits application on company website
       │ User marks "Applied" in dashboard
       │
       ▼
┌──────────────┐
│TRACKER AGENT │  User action: Mark as "Applied"
│   Update     │  Status: "documents_ready" → "applied"
└──────────────┘  Set follow-up reminder (7 days)
```

### Shared State Layer (PostgreSQL)

**Database Schema**:

```sql
-- Users table
CREATE TABLE users (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  email VARCHAR(255) UNIQUE NOT NULL,
  name VARCHAR(255),
  phone VARCHAR(50),
  experience_years INT,
  current_title VARCHAR(255),
  skills TEXT[], -- Array of skill strings
  target_locations TEXT[], -- ["London", "Berlin", "Amsterdam"]
  remote_preferred BOOLEAN DEFAULT false,
  salary_min INT, -- In EUR
  salary_max INT,
  created_at TIMESTAMP DEFAULT NOW(),
  updated_at TIMESTAMP DEFAULT NOW()
);

-- Jobs table (populated by Scout Agent)
CREATE TABLE jobs (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  company VARCHAR(255) NOT NULL,
  title VARCHAR(255) NOT NULL,
  location VARCHAR(255) NOT NULL,
  description TEXT NOT NULL,
  salary_range VARCHAR(100), -- e.g., "€50,000-€65,000"
  url TEXT NOT NULL,
  source VARCHAR(50), -- "linkedin", "indeed", "hackernews"
  posted_date DATE,
  status VARCHAR(50) DEFAULT 'new', -- new | matched | archived
  dedup_hash VARCHAR(64), -- SHA256(company+title+location)
  created_at TIMESTAMP DEFAULT NOW(),
  UNIQUE(dedup_hash)
);

-- Matches table (populated by Matcher Agent)
CREATE TABLE matches (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  user_id UUID REFERENCES users(id) ON DELETE CASCADE,
  job_id UUID REFERENCES jobs(id) ON DELETE CASCADE,
  match_score INT NOT NULL CHECK (match_score >= 0 AND match_score <= 100),
  match_explanation TEXT,
  skills_match_pct INT,
  location_match_pct INT,
  seniority_match_pct INT,
  created_at TIMESTAMP DEFAULT NOW(),
  UNIQUE(user_id, job_id)
);

-- Applications table (tracks user's application pipeline)
CREATE TABLE applications (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  user_id UUID REFERENCES users(id) ON DELETE CASCADE,
  job_id UUID REFERENCES jobs(id) ON DELETE CASCADE,
  match_id UUID REFERENCES matches(id),
  status VARCHAR(50) DEFAULT 'discovered', -- discovered | matched | documents_ready | applied | interviewing | offer | rejected | archived
  cv_draft TEXT, -- Generated CV (Markdown)
  cover_letter_draft TEXT, -- Generated cover letter (Markdown)
  notes TEXT, -- User notes
  applied_date DATE,
  follow_up_date DATE,
  created_at TIMESTAMP DEFAULT NOW(),
  updated_at TIMESTAMP DEFAULT NOW(),
  UNIQUE(user_id, job_id)
);

-- Indexes for performance
CREATE INDEX idx_jobs_status ON jobs(status);
CREATE INDEX idx_jobs_created_at ON jobs(created_at DESC);
CREATE INDEX idx_matches_score ON matches(match_score DESC);
CREATE INDEX idx_applications_user_status ON applications(user_id, status);
CREATE INDEX idx_applications_updated_at ON applications(updated_at DESC);
```

**State Consistency Rules**:
- Scout creates `jobs` record → Matcher creates `matches` record → Composer creates `applications` record
- Status transitions are unidirectional (can't go from "applied" back to "new")
- Foreign key constraints enforce referential integrity
- Timestamps track agent processing times (debugging/performance monitoring)

---

# PART 4: TECHNICAL IMPLEMENTATION

## Tech Stack

### Backend
- **Framework**: FastAPI (Python 3.11+)
- **Agents**: Python modules with FastAPI endpoints (one endpoint per agent)
- **LLM**: OpenAI GPT-4o-mini (fallback: Anthropic Claude Sonnet 3.5)
- **Database**: PostgreSQL 15 (hosted in EU region for GDPR)
- **Orchestration**: n8n (self-hosted or cloud)
- **Job Scraping**: BeautifulSoup + Selenium (for dynamic sites)

### Frontend
- **Framework**: Next.js 14 (React, TypeScript)
- **UI Library**: shadcn/ui (Radix UI + Tailwind CSS)
- **State Management**: React Query (server state) + Zustand (client state)
- **Auth**: NextAuth.js (OAuth + magic link)

### Infrastructure
- **Hosting**: Railway or Render (EU region)
- **Database**: Supabase (managed PostgreSQL in EU)
- **File Storage**: S3-compatible (for CV uploads)
- **Monitoring**: Sentry (error tracking), PostHog (analytics)

### Third-Party Services
- **Email**: Resend or SendGrid
- **Payments**: Stripe (SEPA support)
- **LLM**: OpenAI API (GPT-4o-mini)

---

## Data Privacy & GDPR Compliance

### Legal Basis for Processing
- **Contract**: Processing necessary to provide the service (job matching, document generation)
- **Consent**: Explicit opt-in for marketing emails, analytics tracking
- **Legitimate Interest**: Fraud prevention, service improvement

### User Rights Implementation

| Right | Implementation | Timeline |
|-------|----------------|----------|
| Right to Access | `/api/users/me/export` → JSON download | Immediate |
| Right to Rectification | Profile edit page (all fields editable) | Immediate |
| Right to Erasure | `/api/users/me/delete` → Hard delete all data | 30 days |
| Right to Portability | Export all data (JSON + CSV formats) | Immediate |
| Right to Object | Opt-out checkboxes for marketing, analytics | Immediate |
| Right to Restrict Processing | Pause account (no new jobs, matches, emails) | Immediate |

### Data Retention Policy
- **Active users**: Retain all data indefinitely (while account active)
- **Inactive users** (no login in 12 months): Email warning → Delete after 18 months
- **Deleted accounts**: Hard delete all data within 30 days
- **Backups**: Purge deleted user data from backups after 90 days

### Third-Party Data Sharing
- **OpenAI/Anthropic**: User profile + job description sent for document generation (Data Processing Agreement required)
- **n8n**: Orchestration metadata only (no PII)
- **No data selling**: Never sell or share user data with third parties

---

## Security Measures

### Application Security
- **Authentication**: OAuth 2.0 + JWT tokens (refresh + access)
- **Authorization**: Role-based access control (users can only access own data)
- **Input Validation**: All inputs sanitized (prevent SQL injection, XSS)
- **Rate Limiting**: 100 requests/min per user (prevent abuse)

### Data Security
- **Encryption at Rest**: AES-256 for database, S3 files
- **Encryption in Transit**: TLS 1.3 for all API calls
- **Secrets Management**: Environment variables (not in code)
- **API Keys**: Hashed and salted (never store plaintext)

### Compliance
- **Annual Audit**: Third-party penetration testing
- **Vulnerability Scanning**: Weekly automated scans (Snyk)
- **Incident Response**: 72-hour breach notification policy (GDPR requirement)

---

## Launch Readiness Checklist

### Pre-Launch (Week 12)
- [ ] MVP features complete and tested (end-to-end)
- [ ] GDPR compliance validated (legal review)
- [ ] Privacy policy + Terms of Service published
- [ ] Cookie consent banner implemented
- [ ] Data Processing Agreements signed (OpenAI, n8n)
- [ ] EU data residency confirmed (PostgreSQL in Frankfurt/Dublin)
- [ ] Load testing complete (500 concurrent users)
- [ ] Error monitoring configured (Sentry)
- [ ] Backup and restore tested (PostgreSQL)

### Launch (Week 13)
- [ ] Soft launch to 50 beta users (waitlist)
- [ ] Monitor error rates, performance, user feedback
- [ ] Iterate on MVP based on feedback (1-2 weeks)
- [ ] Public launch (Product Hunt, social media)

### Post-Launch (Months 4-6)
- [ ] SOC 2 Type I certification initiated
- [ ] Expand to Germany (integrate StepStone, Xing)
- [ ] Localization (German UI, document generation)
- [ ] Mobile app (React Native - optional)

---

## Success Metrics & KPIs

### Product Metrics (Monthly)

| Metric | Target (M6) | Target (M12) | Measurement |
|--------|------------|--------------|-------------|
| MAU (Monthly Active Users) | 2,500 | 10,000 | Login events |
| Paid Users | 250 | 1,200 | Stripe subscriptions |
| Free-to-Paid Conversion | 10% | 12% | Signup → Payment |
| 6-Month Retention | 60% | 65% | Paid users still active |
| Jobs Discovered (daily) | 500 | 2,000 | Scout Agent output |
| Match Satisfaction | 80% | 85% | User thumbs up/down |
| Document Quality | 85% | 90% | <5 min editing required |
| NPS (Net Promoter Score) | 40 | 50 | User surveys |

### Business Metrics

| Metric | Target (M12) |
|--------|-------------|
| MRR (Monthly Recurring Revenue) | €100,000 |
| ARR (Annual Recurring Revenue) | €1,200,000 |
| CAC (Customer Acquisition Cost) | €50 |
| LTV (Lifetime Value) | €600 |
| LTV:CAC Ratio | 12:1 |
| Churn Rate | <5% monthly |
| Gross Margin | >80% |

---

**END OF PRD**

---

## Appendix: Glossary

- **Agent**: Autonomous software component with specialized role, decision-making authority, and tools
- **HITL (Human-in-the-Loop)**: Design pattern where agent performs analysis/generation, human provides final authorization
- **Intent Equation**: Outcome + Scope + Constraints + Success Signal + Stop Rule (framework for defining agent behavior)
- **4 Buckets of Risk**: Interpret (high autonomy), Choose (guarded), Generate (HITL), Commit (human required)
- **Safety Lenses**: Reversibility (can we undo?) + Blast Radius (who gets hurt if this fails?)
- **JTBD (Jobs-to-be-Done)**: User-centric framework focusing on the "job" a product helps accomplish
- **MVP (Minimum Viable Product)**: Smallest feature set that delivers core value and validates assumptions
- **TAM/SAM/SOM**: Total Addressable Market / Serviceable Addressable Market / Serviceable Obtainable Market
- **GDPR**: General Data Protection Regulation (EU privacy law)
- **ATS**: Applicant Tracking System (software used by companies to filter applications)
- **LLM**: Large Language Model (AI system like GPT-4, Claude)
- **RAG**: Retrieval-Augmented Generation (LLM + knowledge base)

---

**Document Version**: 2.0
**Status**: Ready for Review
**Next Steps**:
1. Stakeholder review & feedback
2. Technical architecture validation
3. User research validation (interview 10 target users)
4. Finalize scope and timeline for development kickoff
