# ADR-002: Protected B Hosting Architecture for PATH

**Status:** [DRAFT / PROPOSED / ACCEPTED / SUPERSEDED / DEPRECATED]  
**Decision Date:** [INSERT DATE]  
**Classification:** Unclassified / For Internal Use  
**Authors:** [Kirk (Security), Jason (Cloud Ops)]  
**Stakeholders:** EA Team, CDO/OCDO, PATH Governance Team, HAIL Operations

---

## Title

**Protected B Hosting Architecture: Azure Government Cloud vs. Commercial Azure with Enhanced Controls**

---

## Decision

**Will PATH host Protected B AI workloads on Azure Government Cloud (Azure.us) or commercial Azure (Canada regions) with additional security controls?**

---

## Context

### Why This Decision Matters

1. **Data Residency & Sovereignty:** Protected B information may require residency in government-designated infrastructure. Azure.us (Government Cloud) vs. commercial Azure (Canada) affects regulatory compliance and control assurance.

2. **Shadow AI Risk:** If PATH cannot confidently deliver Protected B governance in time, workloads will route to ungoverned platforms (CANChat, Copilot, deprecated RADIA). Hosting model affects ATO timeline and governance confidence.

3. **Service Availability:** Azure.us has limited service availability compared to commercial Azure. Some services (e.g., Azure AI Foundry, Databricks) may not be available in Azure.us, constraining platform architecture.

4. **FinOps Impact:** Azure.us typically has cost premium vs. commercial Azure. Affects client billing and platform sustainability.

5. **Operational Complexity:** Azure.us requires separate credentials, separate networking, separate governance infrastructure. Commercial Azure + enhanced controls enables single unified infrastructure.

### Regulatory Drivers

- **Directive on Automated Decision-Making:** Audit trails, explainability requirements
- **Treasury Board AI Guidance:** Data governance, risk mitigation
- **GCSEC / ITSP.40.111:** Information Security Controls for cloud environments
- **Privacy Impact Assessment (PIA):** Data handling, third-party processing

### Stakeholder Positions

**Security (Kirk):**
- Azure.us provides highest assurance for Protected B
- Commercial Azure + controls is operationally simpler
- Either requires formal ATO approval; both acceptable

**Cloud Operations (Jason):**
- Commercial Azure enables full AI Foundry availability
- Azure.us limits PaaS service selection
- Commercial Azure has lower operational overhead

**Finance:**
- Azure.us cost premium is secondary concern
- Cost predictability and per-workload attribution matter more
- Either option acceptable if cost model is clear

**EA Leadership:**
- Hosting decision affects convergence timeline
- Should enable HAIL/PATH integration (consistent residency)
- Should not create operational fragmentation

---

## Options Considered

### Option 1: Azure Government Cloud (Azure.us)

**Description:**  
Host all PATH Protected B workloads in Azure Government Cloud (Azure.us). Requires separate Azure subscriptions, separate credential management, separate governance infrastructure.

**Rationale:**
- Highest assurance for Protected B data residency
- Explicit government regulatory alignment
- Separates Protected B workloads from commercial Azure

**Advantages:**
- ✅ Highest assurance for Protected B residency
- ✅ Explicit government cloud governance model
- ✅ Clear regulatory alignment (GC AI policy)
- ✅ Physical separation from commercial infrastructure (security boundary)

**Disadvantages:**
- ❌ Azure AI Foundry not available (or limited capability)
- ❌ Databricks not available
- ❌ Limited PaaS service portfolio (App Service, Functions, SQL, Storage available but limited SKUs)
- ❌ Vendor lock-in to Azure Government (higher switching cost)
- ❌ Cost premium (~15–20% vs. commercial Azure)
- ❌ Separate credential and access management (operational overhead)
- ❌ May require separate HAIL deployment in Azure.us (integration complexity)
- ❌ Slower service release cycle (features lag commercial Azure by 6–12 months)

**ATO Timeline:**
- SoS approval faster (government cloud implicit compliance)
- ATO review slightly faster (~2 weeks shorter)
- **Estimated ATO completion: Q3 2026**

**Operational Complexity:**
- Separate Azure environment (credential management, billing, support)
- No integration with commercial Azure (if HAIL remains in Canada)
- Separate ops team or extended ops training required

**Convergence Impact (Scenario A/B/C):**
- If HAIL remains in commercial Azure, creates data residency split (Protected B in.us, Unclassified in Canada)
- Requires explicit integration gateway (adds complexity)
- May force HAIL to migrate to Azure.us as well (convergence cost)

---

### Option 2: Commercial Azure + Enhanced Controls

**Description:**  
Host PATH Protected B workloads in commercial Azure (Canada Central, Canada East). Implement additional encryption, network controls, and Purview governance to meet Protected B assurance requirements.

**Enhanced Controls Detail:**
- **Encryption:** Application-level encryption + Azure Storage Service Encryption (SSE) + Transparent Data Encryption (TDE) for database
- **Network:** Azure Private Link, Network Security Groups (NSGs), Azure Firewall, DDoS Protection Standard
- **Data Governance:** Purview Data Map, sensitivity labels, data classification, Data Loss Prevention (DLP) policies
- **Access Control:** RBAC with Privileged Identity Management (PIM), Azure AD conditional access
- **Audit & Compliance:** Azure Policy enforcement, compliance monitoring, audit logging to Log Analytics, Microsoft Sentinel

**Rationale:**
- Full Azure service availability (including AI Foundry, Databricks)
- Operationally simpler (single Azure environment)
- Cost-effective (no premium vs. commercial Azure)
- Enables HAIL/PATH integration on same cloud
- Canada data residency (PIPEDA compliant)

**Advantages:**
- ✅ Full Azure AI Foundry + Databricks availability (no feature constraints)
- ✅ Lower operational complexity (single Azure environment)
- ✅ No cost premium (commercial Azure pricing)
- ✅ Faster service updates (commercial release cycle)
- ✅ Enables easy HAIL/PATH integration (same cloud)
- ✅ Canada data residency (PIPEDA alignment)
- ✅ Established enterprise Azure controls portfolio (Microsoft, GC partners validate controls)

**Disadvantages:**
- ❌ Controls must be validated for Protected B assurance (SoS process required)
- ❌ Higher governance overhead (multiple controls to manage)
- ❌ Operational complexity: teams must understand enhanced controls, enforce consistently
- ❌ Risk of control misconfiguration (requires training, oversight)
- ❌ SoS approval may take longer (controls must be validated case-by-case, not implicit)

**ATO Timeline:**
- SoS approval requires control validation (longer review)
- Controls must be audited and tested
- **Estimated ATO completion: Q3–Q4 2026 (2–4 weeks longer than Azure.us)**

**Operational Complexity:**
- Single Azure environment (credential management shared with HAIL if converged)
- Enhanced controls require ongoing monitoring and compliance validation
- Purview governance overhead (PII tagging, sensitivity labels, DLP enforcement)

**Convergence Impact (Scenario A/B/C):**
- Enables clean HAIL/PATH convergence (both on same cloud)
- Single residency decision (Canada or US) applies to both
- Shared Purview instance, shared Azure Policy, unified governance infrastructure
- **Strongly preferred for Scenario A (Converge)**

---

### Option 3: Hybrid — Phase 1 Commercial Azure, Phase 2 Azure.us (If Required)

**Description:**  
Phase 1: Deploy PATH on commercial Azure + enhanced controls by Q3 2026 (fast to ATO). Phase 2: If regulatory requirement becomes mandatory, migrate to Azure.us by Q4 2026–Q1 2027.

**Rationale:**
- Fast initial delivery (no waiting on Azure.us validation)
- Risk mitigation option (migrate if regulatory requirement emerges)
- Preserves option to converge with HAIL initially, then diverge if needed

**Advantages:**
- ✅ Fastest path to initial ATO (Q3 2026, no delay)
- ✅ Preserves HAIL/PATH convergence option (both on commercial initially)
- ✅ Mitigation option if regulatory requirement changes
- ✅ Lower upfront cost

**Disadvantages:**
- ❌ Requires architectural rework in Phase 2 (if migration needed)
- ❌ Operational overhead of maintaining two platforms temporarily (Phase 1 + Phase 2 transition)
- ❌ SoS and ATO work may duplicate (Phase 1 controls validation + Phase 2 Azure.us validation)
- ❌ Risk of Phase 2 never occurring (technical debt accumulates in Phase 1)
- ❌ Client confusion about residency posture during transition

**ATO Timeline:**
- Phase 1: Q3 2026 (commercial Azure ATO)
- Phase 2: Q4 2026–Q1 2027 (if migration approved; ~12 weeks for migration + Azure.us ATO)
- **Total: 6–9 months**

**Operational Complexity:**
- Phase 1: Single platform on commercial Azure
- Transition: Migration planning, parallel ops during cutover
- Phase 2: Single platform on Azure.us

**Convergence Impact (Scenario A/B/C):**
- Phase 1: Enables HAIL/PATH convergence on commercial Azure
- Phase 2: If HAIL does not migrate, creates residency split (complexity)
- Deferred decision on HAIL residency (not ideal)

---

## Decision Rationale

### Recommended Option: **Option 2 — Commercial Azure + Enhanced Controls**

**Justification:**

1. **Convergence Enablement:** Option 2 enables clean HAIL/PATH convergence on the same cloud (critical for Scenario A). Option 1 forces HAIL to migrate to Azure.us or creates residency fragmentation (bad for Scenario B).

2. **Service Availability:** AI Foundry and Databricks are core to PATH and HAIL architecture. Option 1 constrains feature set; Option 2 enables full capability.

3. **Operational Simplicity:** Single Azure environment (Option 2) is operationally simpler than separate Azure.us + commercial Azure (Option 1) or phased migration (Option 3).

4. **ATO Timeline:** Option 2 timeline (Q3–Q4 2026) is acceptable and enables convergence decision by Q2 2026. Option 1 timeline is not significantly faster (SoS approval gain ~2 weeks; offset by validation overhead).

5. **Cost:** Option 2 is cost-neutral vs. commercial Azure. Option 1 is 15–20% premium. Option 3 has rework cost.

6. **Regulatory Alignment:** Enhanced controls (encryption, network isolation, Purview governance) meet Protected B assurance requirements without forcing Azure.us. Treasury Board and GCSEC guidance support controls-based approach.

**Success Condition:**  
SoS process must validate that enhanced controls meet Protected B assurance requirements. If SoS validation fails, escalate to Option 1 (Azure.us).

---

## Consequences

### What This Decision Enables

1. **HAIL/PATH Convergence:** Both platforms on same Azure cloud. Unified governance infrastructure, single Purview instance, shared Azure Policy.

2. **Federated Residency Model:** Canada regions for Unclassified + Protected B. Explicit separation from US-based infrastructure (reduces geopolitical risk).

3. **Operational Simplicity:** Single credential management, single support model, unified FinOps.

4. **Full Feature Availability:** AI Foundry, Databricks, all modern PaaS services available for PATH and HAIL.

5. **Cost Efficiency:** Commercial Azure pricing; no premium for government cloud; economies of scale on shared infrastructure.

### What This Decision Constrains

1. **No Azure.us Residency:** Protected B data remains on commercial Azure. Not suitable for workloads requiring explicit government cloud residency (rare for Health Canada; none currently identified).

2. **Enhanced Controls Burden:** Teams must understand and enforce additional governance (Purview, DLP, PIM). Training required.

3. **Canada-Only Residency:** Data must reside in Canada. No multi-region failover to US (if future requirement emerges).

4. **Compliance Monitoring:** Purview and Azure Policy must be continuously monitored. Non-compliance must be remediated quickly (governance gates enforce).

---

## Alternatives Rejected

### Why Not Option 1 (Azure.us)?

- ❌ Constrains AI Foundry and Databricks availability (features PATH/HAIL depend on)
- ❌ Prevents HAIL/PATH convergence on same cloud (creates integration complexity)
- ❌ Higher operational overhead (separate environment, separate creds, separate support)
- ❌ No significant ATO timeline benefit (2-week gain offset by validation overhead)
- ❌ Cost premium not justified for current use case

### Why Not Option 3 (Hybrid)?

- ❌ Defers decision on HAIL residency (architectural ambiguity)
- ❌ Rework cost and operational overhead during migration
- ❌ Risk of Phase 2 never occurring (technical debt accumulates)
- ❌ Client confusion during transition period

---

## Dependencies & Open Items

1. **SoS Validation:** Enhanced controls must pass Protected B validation in SoS process (Q1–Q2 2026)
2. **Purview Configuration:** Must be finalized and tested before production ATO (Q2 2026)
3. **Data Classification:** Must establish data classification taxonomy and labeling standards (Q1 2026)
4. **DLP Policy:** Must define DLP rules and enforcement for Protected B data (Q2 2026)
5. **HAIL Convergence Agreement:** If Scenario A, HAIL must agree to commercial Azure residency (pending HAIL production intake decisions)

---

## Review & Approval

**Proposed By:** EA Team  
**Security Review:** Kirk (Sign-off Required)  
**Cloud Operations Review:** Jason (Sign-off Required)  
**Finance Review:** [Finance Lead] (Advisory)  
**EA Leadership Approval:** Chad / Ali (Final Approval)

---

## Sign-Off

- [ ] Kirk (Security) — Reviewed and concurs with enhanced controls approach
- [ ] Jason (Cloud Ops) — Confirmed AI Foundry + Databricks availability on commercial Azure
- [ ] EA Leadership — Approved for PATH architecture planning

---

## Revision History

| Version | Date | Change |
|---|---|---|
| 0.1 | [INSERT DATE] | Initial draft; options assessment |

---

*This ADR is an EA/TPO working reference. It represents EA team working interpretation, not citeable GC policy.*

*Classification: Unclassified / For Internal Use*
