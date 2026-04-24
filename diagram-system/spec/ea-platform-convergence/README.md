# EA Solution Architecture: HC/PHAC AI Platform Convergence

**Agent Charter:** Supporting ARB assessment of PATH/HAIL convergence architecture

**Target Audience:** Architecture Review Board (ARB), EA team, Treasury Board Secretariat (TBS)

**Goal:** Produce decision-ready framing documents that resolve whether PATH and HAIL should converge into a single platform or remain co-equal with integration points.

---

## Quick Start

1. **Read the Charter:** [EA-Agent-Instructions-v1.md](./EA-Agent-Instructions-v1.md)
2. **Check Configuration:** [config.json](./config.json)
3. **Use USAGE.txt:** [USAGE.txt](./USAGE.txt) (quick reference)
4. **Start with Templates:** `/templates/` (fill in with your analysis)

---

## Directory Structure

```
ea-platform-convergence/
├── EA-Agent-Instructions-v1.md   ← Your charter & full instructions
├── config.json                    ← Agent configuration & scenarios
├── USAGE.txt                      ← Quick reference (6 sections)
├── README.md                      ← This file
│
├── templates/                     ← Working templates (fill in)
│   ├── 001-convergence-framing-template.md      (P1 — ARB framing)
│   ├── 002-waf-assessment-template.md           (P2 — WAF analysis)
│   ├── 003-risk-register-template.md            (P3 — Risk tracking)
│   ├── 004-adr-template.md                      (P4 — ADR-002 decision)
│   └── 005-shadow-ai-narrative-template.md      (P5 — Business narrative)
│
├── deliverables/                 ← Completed, signed-off versions
│   ├── 001-convergence-framing.md
│   ├── 002-waf-assessment.md
│   ├── 003-risk-register.md
│   ├── 004-adr-002.md
│   └── 005-shadow-ai-narrative.md
│
└── intelligence/                 ← Reference documents (populate as needed)
    ├── GoC-AI-Platform-Intelligence.md
    ├── HAIL-current-state.md
    └── PATH-current-state.md
```

---

## The Core Question

**Should PATH (HC-led governance control plane) and HAIL (PHAC-led operational runtime) converge into a single platform or remain co-equal with defined integration points?**

### Three Scenarios

**Scenario A: Single Governed Platform (Converge)**
- HAIL = runtime layer
- PATH = governance control plane
- Single landing zone, unified FinOps, single ATO path
- Tradeoff: Longer path to production, but clearer operating model

**Scenario B: Co-Equal Platforms with Integration Points**
- PATH and HAIL remain separate
- Governance convergence at AI Responsible Committee level
- Explicit integration APIs between platforms
- Tradeoff: Faster near-term delivery, but operational overhead

**Scenario C: PHAC-Led Single Platform (Defer PATH)**
- HAIL becomes sole enterprise platform
- PATH governance vision incorporated post-production
- Fastest initial delivery
- Tradeoff: Governance deferred, higher shadow AI risk

---

## Deliverables (Priority Order)

### P1: PATH/HAIL Convergence Framing Document (2000–2500 words)

**What:** Three explicit options with tradeoff analysis and EA-recommended position

**Where:** `templates/001-convergence-framing-template.md` → `deliverables/001-convergence-framing.md`

**Sections:**
- Executive Summary (300 words)
- Option A: Single Platform (Converge)
- Option B: Co-Equal Platforms (Integration Points)
- Option C: PHAC-Led Single Platform (Defer PATH)
- Comparative Analysis (tradeoff table)
- EA-Recommended Position (with justification)
- Open Dependencies (what must resolve)

**Quality Gate:** ARB can articulate tradeoffs and move to decision

---

### P2: WAF Assessment — Operational Excellence & Reliability (1500–2000 words)

**What:** Formalize Azure Well-Architected Framework assessment

**Where:** `templates/002-waf-assessment-template.md` → `deliverables/002-waf-assessment.md`

**Covers:**
- Pillar 1: Operational Excellence (self-service, FinOps, staffing)
- Pillar 2: Reliability (RTO/RPO, shared dependencies, availability)
- Per-pillar assessment table (current state, gap, scenario feasibility)
- Scenario-by-scenario maturity analysis

**Quality Gate:** Security and finance stakeholders confirm risk characterization

---

### P3: Risk Register — Convergence Risks (1000–1500 words)

**What:** Formalize risk tracking with scenario impact analysis

**Where:** `templates/003-risk-register-template.md` → `deliverables/003-risk-register.md`

**Key Risks:**
- R-001: ATO path blocked by incomplete Statement of Sensitivity
- R-002: Shadow AI — workloads route to ungoverned platforms
- R-003: FinOps complexity (separate cost models)
- R-004: HAIL operational maturity unsustainable at scale
- R-005: ADR-002 missing (Protected B hosting decision not documented)

**Per Risk:**
- Risk statement
- Current mitigation
- Residual risk
- Convergence scenario impact
- Escalation trigger

**Quality Gate:** Risk register tells coherent story; DG understands impact

---

### P4: ADR-002 — Protected B Hosting Architecture (800–1200 words)

**What:** Resolve architectural decision on PATH Protected B hosting model

**Where:** `templates/004-adr-template.md` → `deliverables/004-adr-002.md`

**Decision:** Azure Government Cloud (Azure.us) vs. Commercial Azure + Enhanced Controls?

**Sections:**
- Decision statement
- Context (why it matters)
- Options considered (pros/cons per option)
- Decision & justification
- Consequences (what it enables, what it constrains)
- Alternatives rejected & why

**Quality Gate:** Security and cloud ops leads sign off on rationale

---

### P5: Shadow AI Risk Narrative (800–1200 words)

**What:** Business risk frame connecting convergence decision to institutional governance

**Where:** `templates/005-shadow-ai-narrative-template.md` → `deliverables/005-shadow-ai-narrative.md`

**Sections:**
- The Shadow AI Scenario (regulatory use case: PMRA document review)
- Why This Matters Institutionally (regulatory accountability, TB compliance, HC AI Strategy)
- Why Convergence Decision Matters (scenario comparison: A vs. B vs. C)
- Key Insight (convergence decision affects shadow AI adoption velocity)
- Recommendations to ARB

**Quality Gate:** PMRA stakeholders recognize their use case; briefing-ready for DM/ADM

---

## How to Use This Agent

### Phase 1: Understand the Charter (Day 1)

- [ ] Read EA-Agent-Instructions-v1.md (full scope, constraints, success criteria)
- [ ] Review config.json (scenarios, stakeholder map, framework)
- [ ] Skim USAGE.txt (quick overview)

### Phase 2: Validate Assumptions (Week 1)

- [ ] Schedule stakeholder validation meetings:
  - Security (Kirk): ATO path assumptions, data residency implications
  - Cloud Ops (Jason): Foundry availability, FinOps feasibility
  - PMRA (Sam, Mohamed): Use case priority, governance requirements
  - EA Leadership (Chad, Ali): Alignment with DTB strategy

- [ ] Document feedback in simple feedback log

### Phase 3: Produce Draft Deliverables (Week 2)

- [ ] Start with P1 (Convergence Framing)
- [ ] Use P2 (WAF Assessment) as evidence for P1
- [ ] Draft P3 (Risk Register) in parallel
- [ ] Reference P4 (ADR-002) and P5 (Shadow AI) as supporting narratives

### Phase 4: Iterate & Finalize (Week 3–4)

- [ ] Share drafts with stakeholders
- [ ] Incorporate feedback
- [ ] Move drafts from `templates/` to `deliverables/`
- [ ] Obtain sign-off from security, finance, EA leadership
- [ ] Finalize package for ARB

---

## Quality Standards

✅ **Single-file artifacts** — Each deliverable is clean, standalone, ready for ARB/DM handoff

✅ **No unjustified jargon** — Define terms on first use; assume ARB includes non-architects

✅ **Evidence-based** — Every claim grounded in documented source (Azure WAF, SoS, meeting transcripts)

✅ **Decision-ready** — ARB moves to decision without requesting clarification

---

## Key Assumptions

- ARB meets within 4–6 weeks
- Draft framing needed within 2 weeks
- One iteration cycle on feedback
- Stakeholder availability for validation meetings
- ADR-002 decision can be recorded without major rework

---

## Success Metrics

✓ ARB has three explicit convergence options with clear tradeoff analysis  
✓ EA recommended position is stated and defensible  
✓ Stakeholders (security, cloud ops, PMRA, EA leadership) reviewed and signed off  
✓ Risk register flags three P1 items that convergence decision mitigates  
✓ ADR-002 completed and linked from P1 document  
✓ All deliverables are clean, ARB-ready outputs  

---

## Support & Questions

**Classification unclear?** → EA Lead  
**Want to use external service?** → Check `/governance/` policies  
**Suspected data breach?** → Security Lead (Kirk) immediately  
**Timeline slipping?** → Escalate to CDO/OCDO immediately  

---

## Document Control

**Version:** 1.0  
**Created:** April 2026  
**Owner:** EA Team / Digital Transformation Branch  
**Classification:** Unclassified / For Internal Use  

---

*This agent charter and supporting templates represent EA team working standards for HC/PHAC enterprise architecture analysis. Templates are ready-to-fill; populate with HC/PHAC-specific analysis, stakeholder feedback, and organizational context.*
