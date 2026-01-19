# **Agent \- Adapter (System Intelligence Architect)**

**Identity**: LLM-powered agent that semantically understands user feedback, designs learning strategies, and governs how CareerAgent evolves. 

**Architecture**: LLM-Enhanced Hybrid (semantic analysis → structured output) 

**Competitive Moat**: Proprietary understanding of *why* profiles succeed (not just *that* they do)

---

## **1\. Objective**

### **Problem & Business Impact**

**Problem**: Job platforms provide generic recommendations without semantic understanding of user feedback. Users waste time on dead-end applications because systems can't learn why certain profiles succeed.

**Business Impact**:

* **Time Saved**: 2-3 hours/week per user on better-matched applications  
* **Scale**: For 5,000 users \= 10,000-15,000 hours saved weekly  
* **Quality**: 10-percentage-point improvement in match accuracy  
* **Cognitive Load**: System learns user preferences → fewer manual edits (20% reduction after 5 applications)

### **Why AI Agent (Not automation)?**

**Rule-based approach** (automation):

* "User edits leadership words 80% of the time" → Decrease leadership weight  
* **Problem**: Captures *what* changed, not *why*

**LLM Agent approach**:

* User changes: "Managed cross-functional teams" → "Facilitated autonomous squad collaboration"  
* **Agent reasons**: "User prefers servant leadership framing over command-control language. Signals collaborative style emphasis."  
* **Result**: Updates leadership\_tone \= 'facilitative' (semantic understanding → actionable insight)

**Why this needs reasoning**: Understanding edit *intent* requires semantic analysis. Rules count patterns. Agents understand meaning. This is a judgment task, not a calculation.

### **Agent Purpose**

Close the learning loop through semantic understanding:

1. **Understand** why users edit CVs/Cover Letters (LLM reasoning vs pattern matching)  
2. **Design** learning strategies that adapt Matcher weights & Composer styles  
3. **Govern** quality standards (observability, evals, statistical rigor)  
4. **Create** competitive moat through proprietary semantic intelligence

**Key Innovation**: LLM analyzes meaning → Code node extracts structured data → Maintains all system contracts (zero breaking changes).

**Execution**: n8n LLM Nodes \+ Code Nodes | Nightly batch (2am UTC) | Full autonomy (within ±5% guardrails)

---

## **2\. Desired Outcomes**

| Outcome | Target | Measurement |
| :---- | :---- | :---- |
| LLM Reasoning Accuracy | \>85% | Human review 50/week |
| Match Quality Improvement | \+5pp/month | Avg rating for jobs \>70 |
| Style Convergence | 20% edit reduction | After 5 applications |
| LLM vs Baseline | \+5% interview rate | A/B test |
| User Trust | ≥4.0/5.0 | Monthly survey |
| Voice Authenticity | \<10% mismatch | After 3 apps |

---

## **3\. Core Architecture \- n8n Workflow**

**Trigger**: Cron (nightly 2am UTC)

**Flow**:

PostgreSQL Query → Fetch: composer\_feedback, feedback, jobs

↓

LLM Reasoning Node

  • Prompt: "Analyze user edits, explain WHY preferences changed"

  • Input: {original\_cv, edited\_cv, job\_desc, user\_history}

  • Model: TBD (Claude/GPT/Gemini), Temperature: 0.3

  • Output: JSON {reasoning, confidence, tone, formality, metrics\_density, leadership\_emphasis}

↓

Code Node (extract structured data)

  • Parse LLM JSON

  • Map: "prefers servant leadership" → leadership\_emphasis \= 0.9

  • Apply constraints: ±5% weight changes, enum validation

  • Log to adapter\_reasoning\_log

↓

PostgreSQL Update

  • user\_style\_profiles (UNCHANGED SCHEMA \- see below)

  • matcher\_learned\_weights (±5% constraint)

  • adapter\_reasoning\_log (observability)

### **Schema Contracts** 

### **For Composer** (user\_style\_profiles):

user\_style\_profiles (

  user\_id UUID PRIMARY KEY,

  tone VARCHAR(20) CHECK (tone IN ('analytical', 'narrative', 'conversational')),

  formality DECIMAL(3,2) CHECK (0.0-1.0),

  metrics\_density DECIMAL(3,2),

  leadership\_emphasis DECIMAL(3,2),

  generic\_skills\_usage DECIMAL(3,2),

  sample\_size INTEGER,

  last\_updated TIMESTAMP

);

**For Observability** (adapter\_reasoning\_log \- new, Adapter-only):

adapter\_reasoning\_log (

  id UUID, user\_id UUID, feedback\_id UUID,

  llm\_model VARCHAR(50), llm\_reasoning TEXT,

  extracted\_insights JSONB, confidence\_score DECIMAL(3,2)

);

### **LLM Prompt (Core Structure)**

Analyze user edits to understand preferences:

\- Tone: analytical|narrative|conversational

\- Formality: 0.0 (casual) \- 1.0 (formal)

\- Metrics density, leadership style, generic skills usage

Output JSON: {reasoning, confidence, tone, formality, ...}

### **Dependencies**

| From | To | Data | Breaking Changes? |
| :---- | :---- | :---- | :---- |
| Composer → Adapter | Read | composer\_feedback (edits) | ✅ NO |
| Adapter → Composer | Write | user\_style\_profiles | ✅ NO \- maintains schema |
| Adapter → Matcher | Write | matcher\_learned\_weights | ✅ NO \- maintains schema |

**Tech Stack**: n8n LLM Nodes \+ PostgreSQL \+ REST API (for Matcher/Composer queries)

---

## **4\. Guardrails & Observability**

### **Core Constraints**

**LLM Safety**:

* ✓ Structured JSON output required (reasoning \+ confidence)  
* ✓ Confidence \<0.6 → escalate to human review  
* ✗ CANNOT update weights \>±5%/week  
* ✗ CANNOT override user style for "optimization"  
* ✓ MUST log all LLM reasoning (audit trail)  
* ✓ MUST fallback to statistical if LLM unavailable

**Privacy**: Anonymized views only, respect GDPR deletion, require outcome\_sharing\_consent \= TRUE

**Performance**: Nightly batch only (not real-time), \<30 min runtime, \<$10/day LLM costs

### **Evaluation Framework**

| Metric | Eval Method | Target |
| :---- | :---- | :---- |
| Reasoning Accuracy | Human review 50 random/week | \>85% |
| Outcome Improvement | A/B test (10% LLM vs 90% baseline) | \+5% interview rate |
| Style Convergence | Edit distance over time | 20% reduction after 5 apps |

**Continuous Learning**: If outcomes don't improve → Analyze failed patterns → Adjust prompts → Re-eval

---

## **5\. Autonomy & Stop Rules**

| Autonomy Level | Examples | Approval |
| :---- | :---- | :---- |
| **Full** | Capture feedback, run LLM analysis, update weights (±5%), update profiles | None |
| **Guarded** | Weights 5-10%, low-confidence reasoning (\<0.6), company insights | Human reviews after |
| **Proposal** | Weights \>10%, change LLM prompts, add Matcher features | Human approves before |
| **None** | Delete data (GDPR), share with 3rd parties, override thresholds | Human performs |

**Halt When**: LLM accuracy \<75% (2 weeks) | LLM failures \>20% | Score instability \>25% | Bias detected 

**Escalate When**: LLM suggests \>±5% | Low confidence | Feedback capture \<70% (3+ days) | Interview rate declines (2+ weeks) 

**Success When**: Batch completes \<30 min | A/B test shows ≥5% improvement | User sees insights with LLM reasoning

