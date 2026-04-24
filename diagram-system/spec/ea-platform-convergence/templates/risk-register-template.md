# Risk Register: AI Platform Convergence
## HC/PHAC PATH/HAIL Convergence Architecture

**Status:** Draft  
**Classification:** Unclassified / For Internal Use  
**Last Updated:** [INSERT DATE]  
**Owners:** EA Team, CDO/OCDO Leadership  
**Review Frequency:** Monthly (until convergence decision made); then quarterly

---

## Purpose

Track and monitor risks specific to PATH/HAIL platform convergence. Each risk is assessed with current mitigation, residual risk, and scenario impact. Identifies escalation triggers for executive attention.

---

## Risk Register Summary

| Risk ID | Risk Statement | Priority | Current Status | Mitigation Owner | Escalation Trigger |
|---|---|---|---|---|---|
| R-001 | ATO path blocked by incomplete Statement of Sensitivity (HAIL) | P1 | Open | PHAC/HAIL Team | SoS not completed by Q1 2026 |
| R-002 | Shadow AI: Protected B workloads route to ungoverned platforms | P1 | Open | EA Leadership | First Protected B request; no clear route through PATH/HAIL |
| R-003 | FinOps complexity: Separate cost models if platforms don't converge | P1 | Open | Finance, EA Leadership | Cost model not finalized by Q2 2026 |
| R-004 | HAIL operational maturity: Self-service model unsustainable at scale | P1 | Open | PHAC/HAIL Operations | HAIL production SLA not defined by Q2 2026 |
| R-005 | ADR-002 missing: Protected B hosting decision not documented | P1 | Open | Security (Kirk), Cloud Ops (Jason) | ADR-002 not completed before ARB review |

---

## Risk Details

---

### R-001: ATO Path Blocked by Incomplete Statement of Sensitivity (HAIL)

**Risk Statement:**  
HAIL production ATO cannot proceed until Statement of Sensitivity (SoS) is completed and approved by security. Current SoS is incomplete; blocks HAIL from moving to production intake.

**Current Status:** Open / Active  
**Probability:** High (SoS completion is external dependency)  
**Impact:** High (delays HAIL production ATO into Q2 2026 or later)

**Current Mitigation:**
- PHAC team assigned to complete SoS; timeline TBD
- Progress tracked in HAIL project schedule
- Kirk (Security) has reviewed partial SoS and provided feedback

**Residual Risk:** High  
**Why:** SoS not yet completed; no firm target date; production ATO cannot proceed without it

**Convergence Scenario Impact:**

| Scenario | Impact |
|---|---|
| **A (Converge)** | Single SoS process — reduces duplication, clearer single ATO path. Requires PATH and HAIL SoS alignment on Protected B requirements. |
| **B (Co-Equal)** | Two SoS documents — parallel effort, but HAIL production still waiting. May allow PATH to proceed independently if it accepts risk. |
| **C (PHAC-Led)** | Single SoS process (HAIL). HAIL production still blocked until complete. |

**Escalation Trigger:**
- SoS completion date slips past Q1 2026 (8 weeks from now)
- Security feedback requires significant rework of SoS content
- PHAC team reports resource constraint blocking SoS completion

**Mitigation Actions:**
- [ ] Weekly check-in with PHAC SoS lead
- [ ] Clear target completion date (Q1 2026 soft deadline; Q2 2026 hard deadline)
- [ ] If blocked, escalate to PHAC Director / DTB CDO

**Owner:** PHAC/HAIL Team  
**Last Updated:** [DATE]

---

### R-002: Shadow AI Risk — Protected B Workloads Route to Ungoverned Platforms

**Risk Statement:**  
Protected B workloads (regulatory, surveillance, PII-sensitive) require governance and audit-trail enforcement. If neither PATH nor HAIL delivers this capability fast enough, workloads will route to ungoverned platforms (CANChat unclassified-only, Copilot without Protected B ATO, deprecated RADIA patterns) or be deferred, creating regulatory and operational risk.

**Current Status:** Open / Active  
**Probability:** Medium (high if convergence decision deferred)  
**Impact:** High (regulatory exposure, audit trail gaps, institutional accountability risk)

**Current Mitigation:**
- PATH/HAIL convergence decision in progress (resolves ambiguity)
- ARB discussion flagged this risk; decision pending
- PMRA team is aware; no Protected B requests submitted yet (but anticipated Q2–Q3 2026)

**Residual Risk:** Medium-High  
**Why:** Convergence is still unresolved; unclear which platform owns governance enforcement; decision timeline compressed

**Convergence Scenario Impact:**

| Scenario | Impact |
|---|---|
| **A (Converge)** | Reduces risk fastest. Single platform with unified governance + audit trail delivers Protected B capability by Q3 2026. Clear enforcement path. |
| **B (Co-Equal)** | Maintains risk (two platforms, potential coordination gap). Slower time to governance enforcement. PMRA may explore external alternatives while waiting. |
| **C (PHAC-Led)** | Risk maintained (governance deferred to post-production). PMRA likely to request Protected B capability before governance maturity. High interim risk. |

**Escalation Trigger:**
- First Protected B workload request received; no clear route through PATH or HAIL
- PMRA team requests external/shadow AI alternative
- ARB decision delayed past Q2 2026 (workload requests anticipated Q2–Q3)

**Mitigation Actions:**
- [ ] Communicate convergence decision to PMRA leadership by Q2 2026
- [ ] Establish interim governance policy for Protected B requests (pending full platform readiness)
- [ ] Create "holding pattern" process for PMRA (queue requests, clarify timeline)
- [ ] Escalate if PMRA reports pressure to use external platforms

**Owner:** EA Leadership (Chad, Ali), PMRA Executive  
**Last Updated:** [DATE]

---

### R-003: FinOps Complexity — Separate Platforms Require Separate Cost Models

**Risk Statement:**  
PATH and HAIL may implement separate FinOps models if convergence doesn't proceed. This creates complexity in per-workload cost attribution, budget planning, and client billing. Clients cannot compare costs across platforms; finance cannot forecast enterprise AI spend accurately.

**Current Status:** Open / Active  
**Probability:** Medium-High (if Scenario B or C selected)  
**Impact:** Medium (affects budget planning, client onboarding, platform sustainability)

**Current Mitigation:**
- Current mitigation: none — cost model not yet designed for either platform
- EA team aware; financial implications flagged in earlier documentation

**Residual Risk:** High  
**Why:** FinOps model directly affects client onboarding, budget approvals, platform sustainability; no working group established yet

**Convergence Scenario Impact:**

| Scenario | Impact |
|---|---|
| **A (Converge)** | Resolved. Single FinOps model, unified cost pool, transparent per-client allocation via resource tags/subscriptions. Finance can forecast enterprise AI spend. |
| **B (Co-Equal)** | Increases complexity. Requires explicit cost-sharing agreement for shared services (e.g., two instances of Azure Policy, Purview). Per-platform budgets. Finance overhead of cost allocation logic. |
| **C (PHAC-Led)** | Resolved. HAIL's current per-workload tagging model extends to enterprise. Single FinOps model. |

**Escalation Trigger:**
- Finance escalation: per-workload cost cannot be attributed clearly
- Client complaint: cost opacity prevents budget planning
- Cost model not finalized by Q2 2026

**Mitigation Actions:**
- [ ] Establish FinOps working group (EA, Finance, Cloud Ops) by Q1 2026
- [ ] Draft unified cost model (Scenario A) and per-platform cost-sharing agreement (Scenario B) by Q2 2026
- [ ] Validate with Finance leadership by Q2 2026
- [ ] Communicate cost model to early clients (PMRA, Surveillance) by Q3 2026

**Owner:** Finance, EA Leadership  
**Last Updated:** [DATE]

---

### R-004: HAIL Operational Maturity — Self-Service Model Unsustainable at Scale

**Risk Statement:**  
HAIL's operational model is self-service with minimal platform team. Current workload is Sandbox/Dev/Test. If HAIL scales to enterprise production without formalizing SLA, escalation procedures, and on-call support, operational burden will exceed team capacity. Self-service deployment will create orphaned or poorly-managed workloads.

**Current Status:** Open / Active  
**Probability:** Medium (likely to occur if HAIL production SLA not defined)  
**Impact:** Medium (operational failures, support burden, client dissatisfaction)

**Current Mitigation:**
- Assumption: PHAC team will formalize operating model post-production-ATO
- Operations team assigned; on-call procedure being defined

**Residual Risk:** Medium  
**Why:** HAIL running Sandbox/Dev/Test but production operations not yet staffed; SLA commitment unclear

**Convergence Scenario Impact:**

| Scenario | Impact |
|---|---|
| **A (Converge)** | PATH governance layer matures HAIL's ops discipline. Governance gates enforce SLA compliance, audit trail requirements, incident escalation. Single ops team. |
| **B (Co-Equal)** | HAIL must mature ops model independently. PATH governance gates add compliance overhead but don't formalize ops SLA. Parallel work required. |
| **C (PHAC-Led)** | HAIL must mature ops model independently. Governance logic added post-production (deferred). Higher interim operational risk. |

**Escalation Trigger:**
- HAIL production SLA not defined by Q2 2026
- First production incident exceeds team response capacity
- Client complaint about support responsiveness

**Mitigation Actions:**
- [ ] Define HAIL production SLA by Q1 2026 (RTO 4 hours, RPO 1 hour for Protected B assumed)
- [ ] Establish on-call rotation and escalation procedures by Q2 2026
- [ ] Schedule SLA compliance audit by Q3 2026
- [ ] Plan ops team expansion if workload volume exceeds current capacity

**Owner:** PHAC/HAIL Operations, EA Leadership  
**Last Updated:** [DATE]

---

### R-005: ADR-002 Missing — Protected B Hosting Architecture Decision Not Documented

**Risk Statement:**  
Architectural decision on PATH Protected B hosting model (Azure.us vs. commercial Azure with enhanced controls) is referenced in documentation but the ADR record itself does not exist. This creates audit trail gap; ARB cannot verify decision context or tradeoff analysis.

**Current Status:** Open / Active  
**Probability:** High (ADR missing, known gap)  
**Impact:** Medium (audit trail incomplete, ARB cannot verify decision rationale, rework risk if decision challenged)

**Current Mitigation:**
- Referenced in PATH governance vision, but ADR-002 record does not exist
- Kirk (Security) and Jason (Cloud Ops) have discussed decision informally

**Residual Risk:** Medium  
**Why:** Missing decision record creates audit and traceability gap; formal decision needed before ARB approval

**Convergence Scenario Impact:**

| Scenario | Impact |
|---|---|
| **A (Converge)** | Both platforms require ADR-002 completion. Single platform decision (Azure.us or commercial). Prioritizes ADR-002. |
| **B (Co-Equal)** | Both platforms require ADR-002. Single decision required (both platforms cannot have different data residency). |
| **C (PHAC-Led)** | HAIL hosting determines decision. ADR-002 required (HAIL declares Unclassified or Protected B residency requirement). |

**Escalation Trigger:**
- ARB review cannot proceed without ADR-002
- Security audit flags missing decision record
- Discrepancy between informal decision and formal ADR (if ADR differs from conversation)

**Mitigation Actions:**
- [ ] Schedule decision recording session with Kirk and Jason by Q1 2026
- [ ] Draft ADR-002 (decision, context, options considered, consequences) by Q1 2026
- [ ] Obtain security and cloud ops sign-off on ADR-002 by Q1 2026
- [ ] Link ADR-002 from convergence framing document

**Owner:** Security (Kirk), Cloud Ops (Jason), EA Team  
**Last Updated:** [DATE]

---

## Risk Trend & Monitoring

### Current Risk Status: **5 P1 Risks Open**

| Risk ID | Trend | Status | Mitigation Progress |
|---|---|---|---|
| R-001 | ↔️ | Open | Monitoring SoS completion |
| R-002 | ↑️ | Active | Depends on ARB decision (in progress) |
| R-003 | ↔️ | Open | FinOps working group not yet established |
| R-004 | ↔️ | Open | SLA definition deferred to post-production |
| R-005 | ↔️ | Open | ADR-002 not yet drafted |

---

## Escalation Matrix

| Escalation Trigger | Escalation To | Action | Timeline |
|---|---|---|---|
| SoS completion slips past Q1 2026 | PHAC Director, DTB CDO | Risk review, resource escalation | Immediate |
| First Protected B workload request; no clear route | PMRA Executive, EA Leadership | Interim governance policy, communication | 1 week |
| FinOps model not finalized by Q2 2026 | Finance VP, DTB CDO | FinOps working group establishment | 1 week |
| HAIL production SLA not defined by Q2 2026 | PHAC Director, Operations Lead | Operations planning, resource allocation | 2 weeks |
| ADR-002 not completed before ARB | Security lead, EA Team | ADR decision recording, expedited approval | 1 week |

---

## Risk Owner Responsibilities

**EA Leadership (Chad, Ali):**
- Weekly risk review with mitigation owners
- Escalate P1 risks to CDO/OCDO
- Prioritize ADR-002 and convergence framing completion

**PHAC/HAIL Team:**
- Complete Statement of Sensitivity by Q1 2026
- Define HAIL production SLA by Q1 2026
- Report progress weekly

**Finance:**
- Establish FinOps working group by Q1 2026
- Draft unified cost model by Q2 2026

**Security (Kirk):**
- Complete ADR-002 decision record by Q1 2026
- Validate ATO path for each scenario by Q2 2026

**Cloud Operations (Jason):**
- Co-author ADR-002 by Q1 2026
- Confirm Foundry availability constraints by Q1 2026

---

## Quality Gate

**Sign-off by Risk Owners:**

- [ ] PHAC/HAIL: SoS timeline confirmed
- [ ] EA Leadership: Escalation procedures understood
- [ ] Finance: FinOps working group availability confirmed
- [ ] Security & Cloud Ops: ADR-002 scheduling confirmed

---

*This risk register is an EA/TPO working reference. It represents EA team working interpretation, not citeable GC policy. Monthly reviews until convergence decision; then quarterly.*

*Classification: Unclassified / For Internal Use*
