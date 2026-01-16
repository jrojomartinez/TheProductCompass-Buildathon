# 4 Buckets of Risk Matrix

## Visual Representation

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                        AUTONOMY DECISION FRAMEWORK                          │
└─────────────────────────────────────────────────────────────────────────────┘

┌──────────────┬──────────────────┬─────────────────┬──────────────┬──────────┐
│   BUCKET     │   TASK TYPE      │   DESCRIPTION   │  AUTONOMY    │  AGENTS  │
├──────────────┼──────────────────┼─────────────────┼──────────────┼──────────┤
│              │                  │ Understanding   │              │          │
│  INTERPRET   │ Data Analysis    │ data, parsing   │     HIGH     │  Scout   │
│   (Green)    │ Pattern          │ patterns,       │  Autonomous  │  Tracker │
│              │ Recognition      │ classification  │              │          │
│              │                  │                 │              │          │
│  RISK: LOW   │ Reversible: YES  │ Blast Radius: LOW            │          │
├──────────────┼──────────────────┼─────────────────┼──────────────┼──────────┤
│              │                  │ Ranking,        │              │          │
│   CHOOSE     │ Recommendation   │ filtering,      │   GUARDED    │  Matcher │
│  (Yellow)    │ Scoring          │ prioritizing    │   Suggests   │          │
│              │ Filtering        │ options         │ User decides │          │
│              │                  │                 │              │          │
│  RISK: MED   │ Reversible: YES  │ Blast Radius: MEDIUM         │          │
├──────────────┼──────────────────┼─────────────────┼──────────────┼──────────┤
│              │                  │ Creating new    │              │          │
│  GENERATE    │ Content Creation │ content that    │     HITL     │ Composer │
│  (Orange)    │ Document         │ represents      │ Human Must   │          │
│              │ Writing          │ user identity   │   Approve    │          │
│              │                  │                 │              │          │
│  RISK: HIGH  │ Reversible: YES  │ Blast Radius: HIGH           │          │
├──────────────┼──────────────────┼─────────────────┼──────────────┼──────────┤
│              │                  │ Irreversible    │              │          │
│   COMMIT     │ Transactions     │ external        │    HUMAN     │   None   │
│    (Red)     │ Financial        │ actions with    │  REQUIRED    │  (Not    │
│              │ Legal            │ consequences    │              │automated)│
│              │                  │                 │              │          │
│  RISK: CRITICAL │ Reversible: NO │ Blast Radius: VERY HIGH      │          │
└──────────────┴──────────────────┴─────────────────┴──────────────┴──────────┘

┌─────────────────────────────────────────────────────────────────────────────┐
│                           SAFETY LENSES                                     │
│                                                                             │
│  1. REVERSIBILITY: Can we undo this action?                                │
│     → YES = More autonomy allowed                                          │
│     → NO = Human approval required                                         │
│                                                                             │
│  2. BLAST RADIUS: Who gets hurt if this fails?                             │
│     → Small = Autonomous execution okay                                    │
│     → Large = Human in the loop mandatory                                  │
└─────────────────────────────────────────────────────────────────────────────┘
```

## Mermaid Version (for rendering)

```mermaid
graph LR
    subgraph INTERPRET[INTERPRET - Green - HIGH AUTONOMY]
        I1[Scout Agent]
        I2[Tracker Agent]
        I3[Data Analysis<br/>Pattern Recognition]
        I4[Risk: LOW<br/>Reversible: YES<br/>Blast Radius: LOW]
    end

    subgraph CHOOSE[CHOOSE - Yellow - GUARDED AUTONOMY]
        C1[Matcher Agent]
        C2[Recommendation<br/>Scoring/Ranking]
        C3[Risk: MEDIUM<br/>Reversible: YES<br/>Blast Radius: MEDIUM]
    end

    subgraph GENERATE[GENERATE - Orange - HITL REQUIRED]
        G1[Composer Agent]
        G2[Content Creation<br/>Document Writing]
        G3[Risk: HIGH<br/>Reversible: YES<br/>Blast Radius: HIGH]
    end

    subgraph COMMIT[COMMIT - Red - HUMAN ONLY]
        CO1[Not Automated]
        CO2[Transactions<br/>Financial/Legal]
        CO3[Risk: CRITICAL<br/>Reversible: NO<br/>Blast Radius: VERY HIGH]
    end

    style INTERPRET fill:#50C878,stroke:#2E7D4E,color:#fff
    style CHOOSE fill:#FFB347,stroke:#CC8A3A,color:#000
    style GENERATE fill:#FF6B6B,stroke:#CC5555,color:#fff
    style COMMIT fill:#E74C3C,stroke:#C0392B,color:#fff
```
