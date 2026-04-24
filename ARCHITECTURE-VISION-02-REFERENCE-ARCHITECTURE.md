# Architectural Vision: Reference Architecture
## EA Platform Convergence Analysis (PATH/HAIL)

**Status:** Working Document / This Reference Architecture  
**Classification:** Unclassified / For Internal Use  
**Date:** April 24, 2026

---

## 1. Problem Statement (Why This Architecture Exists)

**Business Problem:**
HC and PHAC are building two AI platforms simultaneously (PATH and HAIL) without a formally resolved convergence architecture. ARB needs to decide: Merge into single platform or remain co-equal with integration points?

**Architecture Problem:**
How do we structure EA analysis so that:
- Modularity: Analysis components (governance, risk, framing) are reusable
- Reasoning: Claude can query relationships between scenarios, risks, tradeoffs
- Governance: Protected B information is handled safely when shared with external services
- Evidence: Every recommendation is traceable to documented reasoning (ADRs, data, stakeholder feedback)
- Iteration: Prototypes by Week 2, feedback by Week 3, final by Week 4

**Why This Matters:**
This isn't just PATH/HAIL. This pattern should work for any future platform convergence, architecture decision, or complex tradeoff analysis. The architecture is a reference for how we do EA work.

---

## 2. Reference Architecture (High Level)

```
┌─────────────────────────────────────────────────────────────────┐
│                    USER (ARB, EA Team)                          │
└────────────┬────────────────────────────────────────────────────┘
             │
             │ Query: "Should PATH and HAIL converge?"
             │
┌────────────▼──────────────────────────────────────────────────┐
│              CLAUDE + AGENT ORCHESTRATION                      │
│  (Reason over scenarios, query graph, compose analysis)        │
└────────────┬──────────────────────────────────────────────────┘
             │
    ┌────────┴────────────────────────────────────────┐
    │                                                  │
┌───▼──────────────────┐                ┌───────────────────────┐
│  MODULARITY LAYER    │                │  KNOWLEDGE LAYER      │
│  (Data Governance)   │                │  (Neo4j Graph)        │
│                      │                │                       │
│ • Classify content   │                │ Convergence scenarios │
│ • Approve sharing    │                │ Risks & tradeoffs     │
│ • Redact Protected B │                │ Stakeholder positions │
│ • Log interactions   │                │ ADR decisions         │
│                      │                │ Dependencies          │
└───┬──────────────────┘                └────────────┬──────────┘
    │                                                 │
    │ ("Is this Level 2?")                           │ MCP Server
    │                                    ("What risks affect Scenario A?")
    │                                                 │
┌───▼──────────────────────────────────────────────▼─────────────┐
│                    PERSISTENT STATE                             │
│                                                                 │
│  • Data Governance Rules (Levels, Approvals, Services)        │
│  • Neo4j: Convergence graph (scenarios, risks, dependencies) │
│  • Audit Log: All Level 2+ sharing (what, when, why, who)     │
│  • ADRs & Decisions: Protected B hosting, governance model    │
└─────────────────────────────────────────────────────────────────┘

FLOW:
1. Claude receives query about convergence
2. Classifies required data (Level 1/2/3)
3. Invokes modular skills (governance, analysis, knowledge)
4. Queries Neo4j graph for scenario relationships
5. Composes evidence-based analysis
6. Logs any external sharing
7. Delivers ARB-ready framing
```

---

## 3. Architectural Layers

### Layer 1: Data Governance (Modular)
**Purpose:** Control what data goes where; ensure Protected B safety

**Components:**
- **Classification Engine** — Determines Level 1/2/3 for any content
- **Approval Matrix** — Tracks what services/people can access what levels
- **Redaction Service** — Removes workload names, stakeholder names, timelines
- **Audit Logger** — Records all Level 2+ interactions
- **Escalation Handler** — Routes Protected B requests to EA Lead/CDO

**Skills:**
- `/classify-data` — Input: content → Output: Level 1/2/3 + reasoning
- `/approve-sharing` — Input: data + service → Output: approved or escalated
- `/redact` — Input: Protected B content → Output: sanitized version
- `/log-sharing` — Input: what, when, who, why → Output: audit record

**How It Works (Concrete Example):**
```
Claude: "I want to analyze ADR-002 (Protected B hosting decision) with ChatGPT"
Governance Layer:
  1. /classify-data → "ADR-002 is Level 2 (Internal Use)"
  2. /approve-sharing → "ChatGPT not approved for Level 2"
  3. Escalation → "EA Lead approval required for ChatGPT + Level 2"
Claude: "I'll use Claude instead (approved for Level 2 with flag)"
Governance Layer:
  1. /log-sharing → Record: "ADR-002 to Claude, flag applied, [timestamp]"
Claude: [Includes flag in prompt]
```

**Integration Points:**
- MCP: Not used (stateless, synchronous)
- Skills: 5 independent skills above
- Knowledge Graph: References approval matrix, maintains audit log

---

### Layer 2: Knowledge Graph (Persistent, Queryable)
**Purpose:** Make EA relationships explicit; enable reasoning over complexity

**What Lives Here:**
- **Convergence Scenarios** (A, B, C) with attributes
- **Risks** (R-001 through R-005) with current status
- **Tradeoffs** (time to delivery, cost, governance maturity, operational overhead)
- **Stakeholder Positions** (Kirk's ATO assumptions, Jason's FinOps concerns, etc.)
- **Architecture Decisions** (ADRs, with decision context)
- **Dependencies** (which risks affect which scenario, which components are shared)

**Why This Matters:**
- Relationships are explicit, not buried in documents
- Claude can ask questions: "What risks affect Scenario A?"
- Graph enables future analysis: "What did we learn from PATH/HAIL for the next platform decision?"

**Interface:**
- MCP Server (Claude's window into the graph)
- Does NOT require Neo4j knowledge (MCP abstracts complexity)
- Queries feel natural ("What risks matter for Scenario B?")

**Example Queries:**
```
"What risks does Scenario A leave open?"
→ Graph finds: R-002 (Shadow AI) still exposed in Scenario A

"Which stakeholders are concerned about FinOps?"
→ Graph finds: Jason (Cloud Ops), Finance VP concerned about R-003

"What's the shortest path from current state to Protected B capability?"
→ Graph finds: Scenario C (fastest), Scenario B (medium), Scenario A (slowest)
```

**Integration Points:**
- MCP: Yes (Neo4j MCP server provides Claude interface)
- Skills: Reference graph to answer questions
- Governance: Graph maintains audit trail of decisions

---

### Layer 3: Analysis & Framing (Modular, Reusable)
**Purpose:** Structure EA work into deliverable components

**Components:**
1. **Scenario Framework** (Convergence, WAF, Risk Assessment, ADR, Narrative)
2. **Stakeholder Validation Process** (Kirk, Jason, PMRA, EA Leadership)
3. **Evidence Gathering** (current state docs, Azure WAF, project intakes)
4. **Tradeoff Analysis** (timeline, cost, governance maturity, operational burden)
5. **Decision Packaging** (P1–P5 deliverables, ARB-ready format)

**How It Works:**
- Week 1: Prototype scenarios with real data → validate with stakeholders
- Week 2: Incorporate feedback → build risk register, WAF assessment
- Week 3: Iterate → stakeholder sign-off
- Week 4: Finalize → ARB package

**Templates:**
- `001-convergence-framing.md` — 3 scenarios + tradeoff analysis
- `002-waf-assessment.md` — Operational Excellence & Reliability pillars
- `003-risk-register.md` — 5 risks with scenario impact
- `004-adr-002.md` — Protected B hosting decision record
- `005-shadow-ai-narrative.md` — Business case for executives

**Modularity:**
- Each template is independent (can use P1 without P2)
- Each template reuses previous decisions (ADRs, risk register)
- Templates are starting points, not prescriptive (adapt for context)

**Integration Points:**
- Knowledge Graph: Feeds evidence (stakeholder positions, risk impacts)
- Governance: Ensures Protected B is redacted before external sharing
- Skills: Use /redact when preparing for stakeholder review

---

## 4. Data & Information Flow

### Input (Week 1)
```
Current State Docs → Stakeholder Meetings → Project Intakes
       ↓                      ↓                    ↓
   (read)                (discuss)            (analyze)
       └──────────────────────┬───────────────────┘
                              ↓
                    Knowledge Graph (populate)
                              ↓
                    Prototype Scenarios (draft P1)
                              ↓
                    Stakeholder Feedback (iterate)
```

### Processing (Week 2–3)
```
Scenarios + Feedback
       ↓
WAF Analysis (Operational Excellence, Reliability)
       ↓
Risk Assessment (R-001 through R-005)
       ↓
Tradeoff Table (Scenario A/B/C comparison)
       ↓
Recommended Position (EA analysis + stakeholder input)
       ↓
Final Deliverables (P1–P5, signed-off)
```

### Output (Week 4)
```
P1: Convergence Framing (executive summary for ARB)
P2: WAF Assessment (evidence for operational excellence/reliability)
P3: Risk Register (current status, mitigation, escalation)
P4: ADR-002 (decision record for Protected B hosting)
P5: Shadow AI Narrative (business case for executives)
    ↓
ARB Package (ready for briefing, no rework needed)
    ↓
Knowledge Graph (updated with final decisions for future reference)
```

---

## 5. Reusability: How Other Projects Adapt This

**Future Scenario: PHAC Surveillance Platform Decision**

New question: "Should we converge Surveillance Platform X and Platform Y?"

**How This Reference Architecture Applies:**

1. **Modularity:** Reuse same governance layer (classification, approval, redaction)
2. **Structure:** Use same 5-deliverable template (P1–P5)
3. **Stakeholder Validation:** Same 4-step process (Kirk, Jason, stakeholder team, EA leadership)
4. **Knowledge Graph:** Add new nodes (Surveillance Scenario A/B/C, Surveillance risks)
5. **Tradeoffs:** Same comparative table format
6. **ADRs:** Same decision record template

**What Changes:**
- Scenarios specific to Surveillance (not PATH/HAIL)
- Stakeholders specific to Surveillance program
- Risks specific to Surveillance architecture
- WAF assessment same; tradeoff dimensions might shift

**Why Reusability Matters:**
- Don't reinvent analysis structure each time
- Team learns from PATH/HAIL (what worked, what didn't)
- Faster to get to decision (2 weeks, not 4)
- Easier to onboard new people (pattern is familiar)

---

## 6. Key Design Decisions (Current Preference)

| Decision | Current Preference | Rationale | Alternative |
|---|---|---|---|
| **Modularity** | 5 separate deliverables (P1–P5) | Easy to iterate, reuse, adapt | Monolithic document (simpler, less reusable) |
| **Knowledge Graph** | Neo4j for scenario relationships | Enables reasoning, queries, future analysis | Spreadsheet/relational DB (simpler, less powerful) |
| **MCP Usage** | Neo4j MCP server only | Justified complexity, high value; no MCP overhead elsewhere | Session-based analysis (simpler, less persistent) |
| **Governance Integration** | Inline (data classified at point of use) | Catches issues early, forces discipline | Separate governance review (simpler, risky) |
| **Stakeholder Validation** | Week 1 prototype feedback | Catches misalignment early, reduces rework | Final-stage reviews (cleaner, riskier) |
| **Reusability** | Reference architecture with adaptation points | Balances consistency and context-fit | Rigid blueprints (consistent, inflexible) |
| **ADR Inclusion** | Part of core deliverables (P4) | Architecture decisions are first-class, not afterthought | Decisions documented separately (less integrated) |

---

## 7. Implementation Checklist (How to Execute This Architecture)

### Week 1: Setup & Prototype
- [ ] Read all 7 architecture vision documents
- [ ] Populate Neo4j with 3 scenarios (A, B, C) and 5 initial risks
- [ ] Schedule stakeholder meetings (Kirk, Jason, PMRA, EA Leadership)
- [ ] Draft P1 (Convergence Framing) with initial scenarios
- [ ] Classify P1 content (should be Level 2: Internal Use)
- [ ] Obtain Week 1 stakeholder feedback
- [ ] Update scenarios based on feedback

### Week 2: Draft All Deliverables
- [ ] Update Neo4j graph with stakeholder positions and initial WAF assessment
- [ ] Draft P2 (WAF Assessment) — Operational Excellence & Reliability
- [ ] Draft P3 (Risk Register) — 5 risks with scenario impact
- [ ] Draft P4 (ADR-002) — Protected B hosting decision
- [ ] Draft P5 (Shadow AI Narrative) — business case
- [ ] Create tradeoff comparison table (P1 + P2 + P3 synthesis)
- [ ] Redact all Protected B before stakeholder sharing
- [ ] Classify all materials (Levels 1/2/3)

### Week 3: Iterate & Consolidate
- [ ] Stakeholder feedback on all drafts
- [ ] Consolidate feedback into revised versions
- [ ] Quality gate: Does ARB have enough to decide?
- [ ] Obtain sign-off from Kirk (security), Jason (cloud ops), PMRA, EA leadership
- [ ] Update Neo4j with final stakeholder positions and risk mitigations
- [ ] Move drafts → final versions (templates → deliverables/)

### Week 4: Package & Finalize
- [ ] Compile ARB package (P1–P5 + supporting evidence)
- [ ] Prepare executive briefing deck
- [ ] Obtain final approvals
- [ ] Generate knowledge graph summary (interesting queries/findings)
- [ ] Ready for ARB meeting

---

## 8. What Success Looks Like

✅ **Execution Success:**
- Prototypes by end of Week 1 (not abstract planning)
- Stakeholder feedback incorporated by Week 2
- Three explicit scenarios with clear tradeoffs
- EA-recommended position stated and defensible
- All Protected B properly redacted before sharing
- 100% of Level 2+ interactions logged
- ADR-002 completed with security/cloud ops sign-off

✅ **Reusability Success:**
- This architecture is used again for next platform convergence
- Team spends less time on structure, more on analysis
- Lessons learned from PATH/HAIL apply to next decision

✅ **Governance Success:**
- Zero Protected B leaks (or contained immediately if one occurs)
- Audit log complete and traceable
- ARB confident analysis is governance-compliant

---

## 9. Tensions & Limits (Honest Assessment)

**When This Architecture Might Not Fit:**
- Simple yes/no decisions (overkill complexity)
- Time pressure < 1 week (can't do stakeholder validation)
- Stakeholders unavailable (feedback-driven iteration won't work)
- Mature decision (not exploratory; known path forward)

**When to Adapt:**
- Lower governance rigor (if not Protected B)
- Fewer stakeholders (can compress timeline)
- Different industry (replace ARB with relevant decision body)
- Different technology (replace PATH/HAIL examples)

---

## 10. Next Steps

This reference architecture is:
- ✅ **Template for future EA work** (reuse pattern, adapt specifics)
- ✅ **Training example** (show new team members how we do analysis)
- ⚠️ **Not universal** (adapt for different contexts)
- 🔲 **To be proven** (does it actually work? We'll find out in Week 1)

---

## Navigation

This is Part 2 of 7. Read in order:

1. Core Principles & Philosophy
2. **Reference Architecture: EA Platform Convergence** ← You are here
3. Neo4j Knowledge Graph Schema
4. Modular Agent & Skill Components
5. Zero Trust Governance Framework
6. Modularity & Reuse Patterns
7. Architectural Vision Synthesis

**Next Document:** Neo4j Knowledge Graph Schema

*Classification: Unclassified / For Internal Use*
