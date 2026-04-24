# ADR-002: Protected B Hosting Architecture for PATH and HAIL

**Status:** [DRAFT / PROPOSED / ACCEPTED / SUPERSEDED / DEPRECATED]
**Decision Date:** [INSERT DATE]
**Classification:** Unclassified / For Internal Use
**Authors:** [Kirk (Security), Jason (Cloud Ops)]
**Stakeholders:** EA Team, CDO/OCDO, PATH Governance Team, HAIL Operations

-----

## Title

**Protected B Hosting Architecture: SA&A Path for Azure Canada AI Workloads (SSC CBS, CCCS PBMM)**

-----

## Decision

**What procurement model and SA&A path will PATH and HAIL use to achieve Protected B authorization for AI workloads on Microsoft Azure within the Government of Canada?**

Note: Azure Government Cloud (Azure.us) is a US federal cloud product operated by Microsoft for US government entities. GC federal departments are not eligible customers. The relevant options for HC/PHAC are within the commercial Azure Canada footprint, governed by SSC and CCCS standards.

-----

## Context

### Why This Decision Matters

1. **Protected B Authorization:** HAIL is deployed but lacks Protected B production ATO. PATH is pre-prototype and requires a clear SA&A path before approval to proceed. Both platforms require Security Assessment and Authorization (SA&A) before hosting Protected B AI workloads in production.
1. **SSC as Procurement Intermediary:** For GC departments, cloud services are procured through the SSC Cloud Brokering Service (CBS). HC/PHAC Azure subscriptions are provisioned via SSC. The SA&A path and operational model must be compatible with the SSC tenant structure.
1. **CCCS PBMM Compliance Baseline:** Protected B workloads in commercial cloud must meet the CCCS Protected B, Medium Integrity, Medium Availability (PBMM) security profile. This profile is documented in ITSG-33 and the GC Cloud Security Risk Management framework. Compliance is a prerequisite for SA&A approval.
1. **TBS 12 GC Cloud Guardrails:** Treasury Board Secretariat requires all GC departments to implement the 12 GC Cloud Guardrails for Azure before onboarding any workloads. These guardrails are the mandatory baseline. PBMM controls build on top of them.
1. **Convergence and Integration:** The SA&A path chosen must be compatible with PATH/HAIL convergence. A path that creates separate tenants or separate subscription structures will add integration complexity and FinOps fragmentation.
1. **Shadow AI Risk:** If PATH and HAIL cannot achieve Protected B SA&A in time, programs will route to ungoverned tools. The hosting and SA&A path directly affects the timeline for eliminating this risk.

### Regulatory and Policy Drivers

- **CCCS PBMM Profile** (Protected B, Medium Integrity, Medium Availability) – required for Protected B in commercial cloud
- **TBS 12 GC Cloud Guardrails for Azure** – mandatory baseline before any GC workload onboarding
- **ITSG-33** (IT Security Risk Management: A Lifecycle Approach) – CCCS framework underlying the PBMM controls catalogue
- **GC Cloud Security Risk Management Framework** – overall framework for cloud SA&A
- **Directive on Automated Decision-Making (DADM)** – audit trails, explainability, and impact assessment requirements
- **Algorithmic Impact Assessment (AIA)** – required for GC AI systems; determines automation tier and associated controls
- **Privacy Impact Assessment (PIA)** – data handling and third-party processing obligations
- **SSC Cloud Brokering Service (CBS) Terms** – procurement obligations for departments using SSC-brokered cloud
- **Treasury Board Policy on Government Security** – overarching security obligation

### Stakeholder Positions

**Security (Kirk):**

- CCCS PBMM is the correct standard for Protected B in commercial cloud
- Full SA&A with validated PBMM controls provides a defensible ATO position
- Incremental SA&A building on HAIL's baseline is faster but requires HAIL controls to be further along
- Either approach acceptable if controls are validated

**Cloud Operations (Jason):**

- SSC CBS tenant structure affects subscription design and operational model
- Azure Canada (Canada Central / Canada East) provides full AI Foundry and Databricks availability
- Single tenant with shared controls is operationally simpler than separate subscription structures
- Purview governance overhead is manageable within the existing Azure Landing Zone

**Finance:**

- SSC CBS pricing model vs. direct agreement affects cost attribution and chargeback
- Per-workload cost tracking is the priority regardless of procurement path
- FinOps framework must be defined before Protected B workloads onboard

**EA Leadership:**

- Hosting and SA&A path must enable HAIL/PATH convergence on the same Azure Landing Zone
- Decision must not create operational or governance fragmentation between HC and PHAC
- SA&A timeline is a blocking constraint for the platform roadmap

-----

## Options Considered

### Option 1: Azure Canada via SSC CBS – Full PBMM SA&A (Standard GC Path)

**Description:**
Host all PATH and HAIL Protected B AI workloads in Azure Canada (Canada Central primary, Canada East DR) via SSC Cloud Brokering Service. Implement the full CCCS PBMM controls catalogue. Complete a full SA&A (Statement of Sensitivity, Statement of Applicability, Security Assessment, Authorization) before onboarding Protected B workloads.

**GC Procurement Path:**

- Subscription provisioned via SSC CBS
- Microsoft Canada customer commitments in effect (data residency, sovereignty)
- Compliance monitoring via SSC and departmental security authorities

**PBMM Controls Scope:**

- Encryption: Application-level + Azure Storage Service Encryption (SSE) + Transparent Data Encryption (TDE)
- Network: Azure Private Link, NSGs, Azure Firewall, DDoS Protection Standard
- Identity: RBAC with Privileged Identity Management (PIM), Entra ID conditional access
- Data Governance: Microsoft Purview Data Map, sensitivity labels, Data Loss Prevention (DLP)
- Audit: Azure Policy, Log Analytics, Microsoft Sentinel
- Guardrails: All 12 TBS GC Cloud Guardrails implemented and validated

**Advantages:**

- Full CCCS PBMM compliance – most defensible SA&A position
- Standard GC path – auditable procurement and governance chain
- Full Azure AI Foundry and Databricks availability (Canada Central / Canada East)
- Canada data residency – PIPEDA compliant, Microsoft Canada sovereignty commitments
- Enables clean HAIL/PATH convergence on same Azure Landing Zone
- Shared Purview instance, shared Azure Policy, unified governance infrastructure

**Disadvantages:**

- Longest SA&A timeline – all controls must be implemented and tested before authorization
- Full PBMM catalogue is broad – governance overhead is significant
- SSC CBS provisioning timelines add lead time at start
- Requires departmental security authority engagement throughout

**SA&A Timeline:**

- Statement of Sensitivity (SoS): Q1 2026 (in progress or complete for HAIL)
- Statement of Applicability (SoA): Q1-Q2 2026
- Security Assessment: Q2 2026
- Authorization (ATO): Q3-Q4 2026
- **Estimated Protected B production: Q3-Q4 2026**

**Convergence Impact:**

- Strongly preferred for Scenario A (Converge): both HAIL and PATH on same Landing Zone under shared SA&A
- Single residency model: Canada Central / Canada East for all workloads
- Unified FinOps, credential management, and support model

-----

### Option 2: Azure Canada via SSC CBS – Incremental SA&A Building on HAIL Baseline

**Description:**
Host PATH Protected B workloads in Azure Canada (Canada Central / Canada East) via SSC CBS, but accelerate the SA&A process by inheriting and extending HAIL's existing controls baseline. PATH SA&A would be scoped as an incremental addition to an already-assessed HAIL environment rather than a standalone SA&A.

**Prerequisite:**
HAIL must have completed or be near completion of its own PBMM SA&A. PATH inherits validated controls and documents only the delta (additional services, patterns, use cases).

**Advantages:**

- Faster SA&A timeline if HAIL baseline is validated
- Reduced documentation duplication
- Consistent controls baseline between HAIL and PATH (convergence-friendly)
- Lower governance overhead for PATH stand-up

**Disadvantages:**

- Dependency on HAIL SA&A being sufficiently complete – HAIL ATO is currently a blocking constraint
- If HAIL controls are not validated, PATH inherits unvalidated controls (security risk)
- Requires explicit agreement with departmental security authority that inheritance model is acceptable
- Less defensible if HAIL and PATH serve different workload types with different sensitivity profiles

**SA&A Timeline:**

- Contingent on HAIL SA&A milestone: if HAIL achieves ATO Q2 2026, PATH incremental SA&A could complete Q3 2026
- If HAIL ATO slips, PATH timeline slips equally
- **Estimated Protected B production: Q3 2026 (optimistic) / Q4 2026 (contingent)**

**Convergence Impact:**

- Strongly aligned with Scenario A (Converge): shared SA&A baseline enforces convergence
- Risk: if HAIL and PATH teams are not coordinated, incremental SA&A may diverge in scope

-----

### Option 3: SSC-Managed On-Premises / GC Data Centre

**Description:**
Host PATH Protected B AI workloads in SSC-managed on-premises infrastructure (GC data centre). Protected B assured without cloud SA&A. No commercial cloud dependency.

Note: This option is included for completeness and to formally reject it. It is not viable for the PATH/HAIL AI platform architecture.

**Advantages:**

- Protected B assured without cloud SA&A process
- No commercial cloud procurement dependency
- Highest physical control over infrastructure

**Disadvantages:**

- Azure AI Foundry not available
- Databricks not available
- No access to Azure Landing Zone services (Purview, Sentinel, AI Search, Cosmos DB, Key Vault)
- Long provisioning timelines (months to years for new capacity)
- High capital and operational cost
- No path to converge with HAIL (which is Azure-based)
- Incompatible with enterprise AI platform architecture direction

**SA&A Timeline:**

- Not applicable in current form – would require re-architecting the platform
- **Estimated Protected B production: Not viable within EA planning horizon**

**Convergence Impact:**

- Incompatible with HAIL/PATH convergence (HAIL is Azure-based)
- Effectively represents abandoning the enterprise AI platform architecture

-----

## Decision Rationale

### Recommended Option: **Option 1 – Azure Canada via SSC CBS with Full PBMM SA&A**

**With an accelerated execution approach aligned to Option 2 where HAIL's validated controls baseline can be inherited.**

**Justification:**

1. **Regulatory Defensibility:** Full PBMM SA&A via SSC CBS is the standard GC path and the most auditable position. ARB and OCDO scrutiny is expected; a non-standard path introduces governance risk.
1. **Convergence Enablement:** Both HAIL and PATH on the same Azure Landing Zone, same SSC CBS subscription structure, same PBMM controls baseline. This is the cleanest path to Scenario A convergence.
1. **Service Availability:** Azure AI Foundry and Databricks are core to the platform architecture. Canada Central / Canada East provide full commercial Azure service availability with no feature constraints.
1. **Canada Data Residency:** Canada Central / Canada East data centres. Microsoft Canada customer commitments. PIPEDA-aligned. Data does not cross into US infrastructure.
1. **Timeline:** Q3-Q4 2026 for Protected B production is consistent with the enterprise planning horizon. If HAIL controls baseline matures faster, Option 2 acceleration is available without changing the overall architecture.
1. **FinOps Simplicity:** Single SSC CBS procurement model. Shared cost attribution, unified billing, clear per-workload chargeback.

**Success Condition:**
Departmental security authority accepts PBMM controls as satisfying Protected B requirements for AI Landing Zone workloads. If scope of AI workloads expands beyond current use cases, SA&A must be re-scoped and re-authorized.

-----

## Consequences

### What This Decision Enables

1. **HAIL/PATH Convergence:** Both platforms on same Azure Landing Zone (Canada Central / Canada East). Unified governance infrastructure: single Purview instance, shared Azure Policy, unified Sentinel workspace.
1. **Canada Residency Model:** All Unclassified and Protected B workloads reside in Canada. No cross-border data flow to US infrastructure. Consistent with Microsoft Canada commitments.
1. **Full Platform Capability:** AI Foundry, Databricks, Unity Catalog, AI Search, Cosmos DB, Key Vault – all available in Canada regions. No feature constraints from hosting choice.
1. **Operational Simplicity:** Single SSC CBS tenant and subscription structure. Single credential management, single support model, unified FinOps.
1. **Compliance Chain:** Clear audit trail from TBS Guardrails through PBMM controls through SA&A authorization. Defensible at ARB and audit.

### What This Decision Constrains

1. **SSC CBS Dependency:** Provisioning timelines and subscription changes go through SSC CBS. Departments cannot unilaterally modify subscription structure.
1. **PBMM Controls Overhead:** Full PBMM catalogue requires ongoing monitoring, Purview governance, DLP enforcement, PIM access reviews. Operational burden is significant.
1. **SA&A Lead Time:** SA&A completion is required before Protected B production onboarding. Timeline is not compressible below the security authority review cycle.
1. **Canada-Only Residency:** Data resides in Canada only. Not suitable for workloads requiring cross-border or US data processing (none currently identified for HC/PHAC).

-----

## Alternatives Rejected

### Why Not Option 2 (Incremental SA&A) as Primary Path?

Incremental SA&A is an acceleration tactic, not a standalone architecture. It is appropriate where HAIL's controls baseline is validated. As the primary path it creates a hard dependency on HAIL's SA&A completion before PATH can proceed independently. Option 1 as primary, with Option 2 elements where controls can be inherited, avoids this single-point-of-failure risk.

### Why Not Option 3 (On-Premises)?

No AI/PaaS capability. Incompatible with HAIL. Incompatible with enterprise AI platform architecture. Not viable within the EA planning horizon.

### Why Not Azure Government Cloud (Azure.us)?

Azure Government Cloud (azure.us) is operated by Microsoft for US federal, state, and local government entities. Government of Canada departments are not eligible customers. This option does not exist for HC or PHAC and must not appear in GC architecture decisions.

-----

## Dependencies and Open Items

1. **HAIL SA&A Status:** Current HAIL ATO for Protected B production is a blocking constraint. Confirm current SA&A stage with Kirk before finalizing PATH SA&A approach.
1. **SSC CBS Subscription Structure:** Confirm whether PATH will use the same SSC CBS subscription as HAIL or require a separate subscription. Decision affects FinOps and SA&A scope.
1. **TBS 12 Guardrails Validation:** Confirm current guardrail implementation status for the existing Azure Landing Zone. Document gaps before SA&A submission.
1. **Purview Configuration:** Sensitivity labels, DLP policies, and data classification taxonomy must be finalized before Protected B workloads onboard.
1. **AIA Completion:** Algorithmic Impact Assessment must be completed for each AI use case before Protected B production. Confirm AIA status for HAIL workloads (IDP, epidemiological pipelines).
1. **HAIL/PATH Convergence Agreement:** If Scenario A, HAIL and PATH must agree on shared Landing Zone, shared controls baseline, and shared SA&A approach. Requires CDO/OCDO alignment.

-----

## Review and Approval

**Proposed By:** EA Team
**Security Review:** Kirk (Sign-off Required)
**Cloud Operations Review:** Jason (Sign-off Required)
**SSC Relationship:** [SSC Account Executive or CBS Contact] (Advisory)
**Finance Review:** [Finance Lead] (Advisory)
**EA Leadership Approval:** Chad (Final Approval)

-----

## Sign-Off

- [ ] Kirk (Security) – PBMM controls approach validated for Protected B assurance
- [ ] Jason (Cloud Ops) – SSC CBS subscription structure and AI Foundry / Databricks availability confirmed for Canada Central / Canada East
- [ ] EA Leadership – Approved for PATH and HAIL architecture planning

-----

## Revision History

|Version|Date         |Change                                                                                                                                                                                                                                                                     |
|-------|-------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|0.1    |[INSERT DATE]|Initial draft; options assessment                                                                                                                                                                                                                                          |
|0.2    |2026-04-24   |Corrected hosting framing: replaced Azure Government Cloud (Azure.us) with GC-correct framing (SSC CBS, CCCS PBMM, Canada Central / Canada East). Added AIA, ITSG-33, TBS Guardrails to regulatory drivers. Formally rejected Azure.us as not applicable to GC departments.|

-----

*This ADR is an EA/TPO working reference. It represents EA team working interpretation, not citeable GC policy.*
*Classification: Unclassified / For Internal Use*
