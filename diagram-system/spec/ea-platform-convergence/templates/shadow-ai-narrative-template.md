# Shadow AI Risk Narrative
## Why PATH/HAIL Convergence Matters to Institutional Governance

**Status:** Draft  
**Classification:** Unclassified / For Internal Use  
**Audience:** Architecture Review Board (ARB), Executive Leadership, Program Leads  
**Date:** [INSERT DATE]

---

## The Shadow AI Scenario

### Regulatory Use Case: PMRA Document Review

**Situation:**  
Health Canada's Therapeutic Products Directorate (TPD) within PMRA processes thousands of pharmaceutical company regulatory submissions each year. Reviewers manually:
- Extract key safety and efficacy data from clinical trial reports
- Cross-reference claims against regulatory requirements
- Flag inconsistencies or gaps for further investigation

Processing time per submission: 4–6 weeks (manual review, sequential).

**Capability Need:**  
An AI-assisted document review system could:
- Extract entities and relationships from trial reports (Named Entity Recognition, Relationship Extraction)
- Summarize key findings vs. regulatory requirements (Summarization)
- Flag inconsistencies or high-risk findings for human reviewer (Risk Scoring, Decision Support)
- Reduce manual review time to 1–2 weeks (faster decision-making, client satisfaction improvement)

**Governance Requirement:**  
Submission documents are Protected B (clinical trial data, proprietary information, potential PII). Regulatory decisions informed by AI must be:
1. **Auditable** — Complete audit trail of which documents were reviewed, which AI features were used, which flagged items were reviewed by humans
2. **Explainable** — Reviewers can explain why the AI flagged a particular risk or finding
3. **Governed** — AI system is approved by Health Canada's AI Responsible Committee before deployment
4. **Compliant** — Meets Privacy Impact Assessment requirements (PIA), Directive on Automated Decision-Making, Treasury Board AI Guidance

---

### The Problem: No Clear Route Today

**Current State:**
1. **PATH:** Governance control plane in pre-prototype phase. No production ATO. No confirmed hosting model. No confirmed timeline to Protected B + audit-trail capability.

2. **HAIL:** Operational runtime in Sandbox/Dev/Test. Production ATO submitted. Data sensitivity declared as Unclassified (limits to unclassified workloads). Protected B target posture unconfirmed.

**Regulatory Team Options:**

**Option A: CANChat Integration**
- ❌ Unclassified scope only. Cannot handle Protected B documents. Not viable for regulatory submissions.

**Option B: Copilot (Microsoft 365)**
- ❌ No ATO confirmation for Protected B. Licensing and data residency unclear. Enterprise terms under negotiation. Not approved.

**Option C: DIY Implementation**
- ⚠️ PMRA team implements custom AI solution (using open-source models + custom infrastructure).
- Risk: Audit trail gaps, explainability unclear, governance unverified, compliance risk.
- Time: 6–12 months to pilot, 12–24 months to production.
- **This scenario has happened before** — deprecated RADIA patterns, unauthorized API calls to external AI services, lack of governance oversight.

**Option D: External Vendor**
- ⚠️ PMRA procures AI service from external provider (AWS SageMaker, Google Vertex, custom vendor).
- Risk: Data residency (may not be Canada), governance outside GC control, regulatory audit trail incomplete.
- Time: 3–6 months for vendor selection + 6–12 months for integration.
- Cost: Higher than internal platforms.

**Option E: PATH/HAIL Readiness**
- ❌ If neither platform delivers Protected B + audit-trail capability fast enough, PMRA defers or escalates to external solution.
- Time: 6–9 months (dependent on convergence decision and ATO timeline).

---

## Why This Matters Institutionally

### 1. Regulatory Accountability

The Directive on Automated Decision-Making requires federal institutions to:
- Maintain documented audit trails for all automated decisions
- Provide transparency to affected persons (industry, public)
- Ensure human oversight and review

**If PMRA uses ungoverned AI:**
- Audit trail gaps → regulatory challenges
- Audit trail cannot be reconstructed → legal liability
- Industry can challenge regulatory decisions based on AI use without transparency
- **Bayer precedent:** Regulatory decisions informed by AI without transparent audit trail → legal challenge based on "algorithmic bias" → decision overturned or delayed

**If PMRA routes to external vendor:**
- Data exits Canada → not compliant with PIPEDA, government data policy
- Governance outside GC control → security/privacy risk
- Audit trail may not meet Treasury Board standards
- Vendor may not sign GC terms of reference

### 2. Treasury Board Directive Compliance

Treasury Board AI Guidance (TB 2024) requires:
- Data governance and protection controls
- Risk mitigation for automated decision-making
- Audit trails for all AI use in regulatory decisions
- Evidence of human review and override capability

**Shadow AI scenario:** PMRA uses unauthorized AI → does not meet TB compliance → audit exposure → potential financial liability

### 3. HC AI Strategy Alignment

Health Canada's AI Strategy (DTBCC) identifies three priority focus areas:
1. **Empower the Workforce** — AI streamlines regulatory work
2. **Scale and Strengthen Surveillance** — AI supports health monitoring
3. **Enhance Regulatory Processes and Services** — AI improves regulatory efficiency

**Regulatory document review** is explicitly listed as a priority capability (aligns with Focus Area 3: Enhance Regulatory Processes).

**Shadow AI risk:** If capability is delivered ungoverned (external vendor, DIY), institution loses strategic control over AI adoption. Does not align with HC AI Strategy governance model.

### 4. Competitive Risk

**Current state:**
- Regulatory review time: 4–6 weeks (competitive disadvantage vs. US, EU)
- Industry feedback: "HC regulatory approval is slower than other jurisdictions"
- Retention risk: Pharmaceutical companies submit to faster agencies first

**PATH/HAIL delivery impact:**
- If Path/HAIL delivers Protected B + audit capability: PMRA can reduce review time to 1–2 weeks (competitive parity with US/EU)
- If PATH/HAIL delayed and PMRA uses external vendor: Canada's regulatory process remains slow, competitive disadvantage continues

---

## Why Convergence Decision Matters

### Convergence Scenario Comparison

**Scenario A: Single Governed Platform (Converge)**

**Delivery Timeline:**
- Platform maturity: Q3 2026 (unified governance + audit trail, single ATO)
- PMRA readiness: Q4 2026 (pilot with first Protected B workload)
- Production capability: Q1 2027 (full enterprise readiness)

**Risk Mitigation:**
- ✅ Single ATO path (faster decision than two parallel ATOs)
- ✅ Unified governance enforced consistently
- ✅ Audit trail capability built into platform (not retrofit)
- ✅ PMRA can deploy with confidence (governance is institutional, not DIY)

**Shadow AI Risk:** **LOWEST** — Single platform with built-in governance reduces PMRA incentive to use external/shadow solutions. PMRA sees clear path to compliant capability.

---

**Scenario B: Co-Equal Platforms with Integration Points**

**Delivery Timeline:**
- HAIL runtime: Q1 2026 (production ATO, but Protected B status unclear)
- PATH governance: Q3 2026 (governance layer ready)
- PMRA readiness: Q3–Q4 2026 (HAIL handles documents, PATH governs; requires integration testing)
- Production capability: Q1 2027 (both platforms stabilized)

**Risk Mitigation:**
- ⚠️ Two platforms require coordination (governance + runtime separation)
- ⚠️ Two parallel ATO processes (longer total timeline)
- ⚠️ PMRA sees longer delivery window; may explore external options during delay

**Shadow AI Risk:** **MEDIUM** — Two platforms create coordination overhead and potential delays. PMRA may start external vendor evaluation while waiting for both platforms to mature.

---

**Scenario C: PHAC-Led Single Platform (Defer PATH)**

**Delivery Timeline:**
- HAIL production: Q1 2026 (runtime available, but Protected B/audit-trail unconfirmed)
- HAIL governance maturity: Q2–Q3 2026 (deferred to post-production; AI Responsible Committee gates added post-ATO)
- PMRA readiness: Q3–Q4 2026 (HAIL with governance, but maturity unproven)
- Production capability: Q4 2026 (governance still being operationalized)

**Risk Mitigation:**
- ⚠️ Fastest initial delivery (HAIL already in Sandbox)
- ❌ Governance is deferred (PMRA may start with ungoverned pilot, retrofit governance later)
- ❌ Audit trail maturity unproven (PMRA may run unaudited first, audit later)

**Shadow AI Risk:** **MEDIUM-HIGH** — HAIL is production-ready but governance is post-production. PMRA may deploy ungoverned pilot to meet timeline pressure. Retrofit governance later. Audit trail gaps accumulate.

---

## Key Insight: Convergence Decision Affects Shadow AI Adoption Velocity

**The core risk:** If institutional platforms (PATH/HAIL) are perceived as delayed or governance-uncertain, workload owners (PMRA, Surveillance, Data teams) will:

1. Start evaluating external vendors immediately (without waiting for internal platforms)
2. Deploy ungoverned pilots (to meet timeline pressure)
3. Accumulate technical debt (governance retrofit is harder than design-first)
4. Lose institutional control over AI adoption model

**Convergence decision resolves this by:**
- **Scenario A:** Clear single platform, unified governance → PMRA confident in capability, waits for PATH/HAIL → no shadow AI
- **Scenario B:** Two platforms with integration → PMRA sees coordination delay, may start external evaluation → medium shadow AI risk
- **Scenario C:** Fast HAIL delivery but deferred governance → PMRA starts ungoverned pilot → high shadow AI risk

---

## Recommendations to ARB

1. **Prioritize Convergence Decision:** Choose Scenario A (Converge) or B (Co-Equal) by Q2 2026. Defer PATH (Scenario C) increases shadow AI risk unacceptably.

2. **Communicate with PMRA:** Once convergence decision is made, brief PMRA leadership on timeline and capability delivery. Establish interim governance policy for Protected B requests (queue requests, clarify timeline) to prevent external evaluation.

3. **Prepare Pilot Program:** Begin PMRA pilot planning by Q1 2026 (document selection, success metrics, governance test scenarios). Ready to deploy first protected B workload by Q4 2026 / Q1 2027.

4. **Track Shadow AI Signals:** Monitor for external vendor evaluations, DIY projects, unauthorized API usage. If detected, escalate to executive (signal that institutional platforms are perceived as delayed).

---

## Appendix: Regulatory Decision-Making as AI Use Case

### Why This Matters to ARB

Regulatory decisions (pharmaceutical approvals, inspection priorities, compliance determination) have the following characteristics:

1. **High Stakes** — Decisions affect public health, industry economics, institutional credibility
2. **Audit-Heavy** — Industry can challenge decisions; complete audit trail required
3. **Explainability-Required** — Regulators must explain why an AI recommendation was accepted or overridden
4. **AI-Adjacent** — AI can assist (extract data, summarize findings) but cannot replace human judgment
5. **Compliance-Critical** — Must meet Treasury Board, Privacy Act, Directive on Automated Decision-Making requirements

**Shadow AI in this context is particularly risky** because:
- Regulatory challenges require transparent audit trails (missing in shadow AI)
- Industry trust depends on verifiable, explainable decisions (not possible with ungoverned AI)
- Financial liability (to industry, public, institution) if AI is used without proper governance

**Example:** Bayer pharmaceutical challenge to FDA decision: "FDA's automated review process did not provide transparent audit trail; decision is not defensible." FDA required to re-review manually. **Result: Regulatory delay + reputational damage.**

**HC Risk:** Similar challenge to PMRA decision informed by ungoverned AI → audit trail missing → decision overturned → regulatory delay → industry loses confidence in HC review process.

---

## Sources

- Directive on Automated Decision-Making (Treasury Board)
- Treasury Board AI Guidance (2024)
- Health Canada AI Strategy (DTBCC, 2025)
- PATH Governance Vision (EA documentation)
- HAIL Current State Assessment (EA documentation)
- PMRA AI Use Case Requirements (meeting transcript, [DATE])

---

*This narrative is an EA/TPO working reference. It represents EA team working interpretation, not citeable GC policy.*

*Classification: Unclassified / For Internal Use*
