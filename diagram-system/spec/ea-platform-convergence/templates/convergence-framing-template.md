# PATH/HAIL Convergence Framing Document

**Status:** Draft  
**Classification:** Unclassified / For Internal Use  
**Target Audience:** Architecture Review Board (ARB), EA Leadership, Digital Transformation Branch  
**Timeline:** [INSERT: ARB meeting date]

---

## Executive Summary

[200–300 words]

**The Decision:** Should PATH (HC-led governance control plane) and HAIL (PHAC-led operational AI runtime) converge into a single enterprise platform or remain as co-equal platforms with defined integration points?

**Why It Matters:**
- Shadow AI Risk: Workloads routing to ungoverned platforms (CANChat, Copilot, deprecated RADIA) if neither PATH nor HAIL delivers Protected B + audit-trail capability in time
- FinOps Clarity: Separate platforms require separate cost models; convergence enables unified cost attribution
- Governance Coherence: Two platforms = two governance models; single platform = consistent enforcement across all workloads

**Three Options:**
- **Option A:** Single Governed Platform (Converge)
- **Option B:** Co-Equal Platforms with Defined Integration Points
- **Option C:** PHAC-Led Single Platform (Defer PATH)

**EA Recommendation:** [State position; justify based on shadow AI risk, ATO timeline, operational simplicity]

**Open Dependencies:** [List what must resolve for recommendation to proceed]

---

## Option A: Single Governed Platform (Converge)

### Architecture
- HAIL becomes the operational runtime layer
- PATH becomes the governance control plane
- Single Azure landing zone with unified access controls
- Unified FinOps model and cost attribution
- Single ATO path for Protected B workloads

### Rationale

[Explain why this option addresses the convergence question]

### Tradeoffs

**Advantages:**
- Single ATO path (faster to decision than two parallel ATOs)
- Unified governance enforced consistently across all workloads
- Simplified FinOps and cost attribution
- Clearer long-term operating model for enterprise AI platform

**Disadvantages:**
- Longer path to initial production (requires PATH to mature to governance-ready state)
- Higher upfront integration cost (merging two teams, two architectural approaches)
- Architectural rework of HAIL's self-service model to accommodate PATH's centralized governance gates
- Risk of PATH delays cascading to HAIL's production timeline

### Timeline Impact
[When can this scenario deliver first Protected B workload with governance?]

### Operational Implications
[How do teams operate? What changes to HAIL's current self-service model?]

### FinOps Impact
[Unified cost model per workload]

---

## Option B: Co-Equal Platforms with Defined Integration Points

### Architecture
- PATH and HAIL remain separate platforms
- Governance convergence at policy enforcement layer (AI Responsible Committee gates)
- HAIL handles operational runtime
- PATH handles governance, audit trails, and Protected B policy enforcement
- Explicit integration APIs between platforms

### Rationale

[Explain why this option preserves current momentum while addressing governance]

### Tradeoffs

**Advantages:**
- Faster near-term delivery (both platforms can proceed in parallel)
- Reduces architectural disruption to HAIL's current operational model
- PHAC retains operational independence; HC retains governance authority
- Lower integration cost (explicit APIs rather than deep platform merge)

**Disadvantages:**
- Operational overhead of maintaining two separate platforms
- FinOps complexity (per-platform cost models; overhead of cost allocation logic)
- Governance inconsistency risk (two governance enforcement layers; potential coordination gaps)
- Two parallel ATO processes (longer total timeline)
- Two sets of shared infrastructure (Azure Policy, audit tooling, etc.)

### Timeline Impact
[When can this scenario deliver first Protected B workload? When are both ATOs complete?]

### Operational Implications
[How do teams operate? What is the API contract between platforms?]

### FinOps Impact
[Separate cost models; overhead of cost-sharing agreement]

---

## Option C: PHAC-Led Single Platform (Defer PATH)

### Architecture
- HAIL becomes the sole enterprise AI platform
- PATH governance vision incorporated into HAIL's operational model
- AI Responsible Committee gates integrated into HAIL's CI/CD pipeline
- Governance maturity deferred to post-production-ATO

### Rationale

[Explain why this option accelerates delivery while deferring governance complexity]

### Tradeoffs

**Advantages:**
- Fastest path to initial Protected B capability (HAIL continues as-is)
- Simplest near-term architecture (one platform, one team)
- Lowest upfront cost
- Fastest to production ATO

**Disadvantages:**
- Moves governance responsibility entirely to PHAC (HC loses architectural voice)
- Requires HAIL to mature operational discipline beyond current self-service model
- Governance enforcement maturity deferred; increased shadow AI risk in interim
- Risk of governance gaps if HAIL prioritizes operational agility over audit compliance
- May not meet HC's governance expectations for regulatory workloads

### Timeline Impact
[When can HAIL achieve Protected B? When is governance maturity reached?]

### Operational Implications
[HAIL takes on governance responsibility; what does this cost operationally?]

### FinOps Impact
[Single platform; unified cost model]

---

## Comparative Analysis

| Dimension | Option A (Converge) | Option B (Co-Equal) | Option C (PHAC-Led) |
|---|---|---|---|
| **Time to Protected B** | Q3 2026 (longer) | Q2 2026 (parallel) | Q1 2026 (fastest) |
| **Time to Single ATO** | Q3 2026 (one ATO process) | Q3–Q4 2026 (two ATO processes) | Q1–Q2 2026 (one ATO process) |
| **Shadow AI Risk** | Lowest (unified governance) | Medium (two platforms, coordination overhead) | Medium-High (governance deferred) |
| **FinOps Complexity** | Low (unified) | High (separate models, cost allocation) | Low (unified) |
| **Governance Coherence** | High (single enforcement layer) | Medium (two layers, integration points) | Medium (dependent on HAIL maturity) |
| **Operational Overhead** | Medium (integration cost upfront) | High (two platforms ongoing) | Low (single platform) |
| **HC Governance Voice** | Strong (HC leads governance plane) | Strong (PATH = HC governance layer) | Weak (PHAC-led, HC as stakeholder) |

---

## EA-Recommended Position

[State your analytical recommendation clearly. Example:]

**Recommended Option: A (Single Governed Platform — Converge)**

**Justification:**
- Option A minimizes shadow AI risk fastest by delivering unified Protected B + audit-trail capability as single integrated system
- Unified governance reduces institutional risk of inconsistent enforcement across two platforms
- Single ATO path is clearer and faster than coordinating two parallel ATOs
- Long-term operating model is simpler and more sustainable
- Higher upfront cost is justified by reduced operational complexity and lower shadow AI risk

**Conditions:**
- PATH must reach governance-ready prototype status by Q2 2026 (target date for PATH resource commitment confirmation)
- HAIL and PATH teams must agree on governance integration APIs and governance gate specifications by Q1 2026
- FinOps unified model must be finalized and approved by Finance by Q2 2026

---

## Open Dependencies (Must Resolve Before Proceeding)

1. **ATO Path Confirmation**
   - Dependent: All three options
   - Impact: Determines which scenario delivers Protected B fastest
   - Owner: Kirk (Security/ATO)
   - Deadline: Q2 2026

2. **Statement of Sensitivity Completion (HAIL)**
   - Dependent: All three options (blocks HAIL production ATO)
   - Impact: If not completed, Option C delays into Q2 2026
   - Owner: PHAC/HAIL team
   - Deadline: Q1 2026

3. **FinOps Model Alignment**
   - Dependent: Option A (unified model); Option B (cost-sharing agreement)
   - Impact: Determines sustainability of platform strategy
   - Owner: Finance, EA leadership
   - Deadline: Q2 2026

4. **PATH Governance Integration Specification**
   - Dependent: Option A (convergence); Option B (integration APIs)
   - Impact: Determines feasibility of governance enforcement
   - Owner: PATH and HAIL architecture teams
   - Deadline: Q1 2026

5. **ADR-002: Protected B Hosting Model**
   - Dependent: All three options
   - Impact: Determines Azure.us vs. commercial Azure decision
   - Owner: Kirk (Security), Jason (Cloud Ops)
   - Deadline: Q2 2026

---

## Risk Summary

**P1 Risks That This Decision Directly Mitigates:**

1. **Shadow AI Risk** — Workloads routing to ungoverned platforms
   - Option A mitigates fastest (single platform, unified governance)
   - Option C mitigates slowest (governance deferred)

2. **FinOps Complexity** — Separate platforms require separate cost models
   - Option A resolves (unified cost model)
   - Option B increases complexity (two cost models, allocation overhead)

3. **ATO Path Ambiguity** — No clear single path to Protected B capability
   - Option A resolves (single ATO process)
   - Option B extends timeline (two parallel ATOs)

See Risk Register (003-risk-register.md) for full risk assessment per scenario.

---

## Next Steps

1. **ARB Review & Feedback** [Timeline]
2. **Stakeholder Validation** [Security, Cloud Ops, PMRA, EA Leadership sign-off]
3. **Decision Point** [ARB approves recommended option or selects alternative]
4. **Implementation Planning** [If Option A or B approved, begin convergence workstream setup]

---

## Appendices

- **Appendix A:** Current State Detail (PATH and HAIL architecture summary)
- **Appendix B:** WAF Assessment — Operational Excellence & Reliability Pillars
- **Appendix C:** ADR-002 — Protected B Hosting Architecture Decision
- **Appendix D:** Shadow AI Risk Narrative
- **Appendix E:** Stakeholder Feedback Log

---

*This document is an EA/TPO working reference. It represents EA team working interpretation, not citeable GC policy.*

*Classification: Unclassified / For Internal Use*
