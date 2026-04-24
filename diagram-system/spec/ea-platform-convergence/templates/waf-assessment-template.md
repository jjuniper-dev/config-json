# WAF Assessment: Operational Excellence & Reliability Pillars
## HC/PHAC AI Platform Convergence

**Status:** Draft  
**Classification:** Unclassified / For Internal Use  
**Assessment Date:** [INSERT DATE]  
**Reviewers:** [Security, Finance, Cloud Ops stakeholders]

---

## Purpose

Formalize the Azure Well-Architected Framework (WAF) assessment for PATH/HAIL convergence. Document which pillar gaps are addressable within each convergence scenario (A: Converge, B: Co-Equal, C: PHAC-Led).

This assessment provides the evidence base for the P1 Convergence Framing Document.

---

## Assessment Framework

**Primary Pillars (Direct Impact on Convergence):**
1. **Operational Excellence** — Platform integration, self-service feasibility, FinOps unification
2. **Reliability** — RTO/RPO targets, shared dependency risk, cascade failure scenarios

**Secondary Dimensions (Context):**
- Governance Coherence
- Data Residency & Sovereignty
- FinOps Clarity
- Shadow AI Risk

---

## Pillar 1: Operational Excellence

### 1.1 Self-Service Model Integration

| Dimension | Current State | Gap | Scenario A | Scenario B | Scenario C | Priority |
|---|---|---|---|---|---|---|
| **Self-Service Model** | HAIL is self-service (teams deploy own resources). PATH assumes centralized governance. | Conflict: Can PATH scale to support self-service deployment while maintaining governance gates? | Resolved — PATH governance gates as CI/CD pipeline pre-requisites. Teams self-serve within policy bounds. | Partial — requires explicit API contract between HAIL (runtime) and PATH (governance). Risk of coordination gaps at scale. | Resolved — HAIL remains self-service; governance maturity deferred. | P1 |
| **Governance Gate Enforcement** | HAIL has no formal governance gates. PATH design includes Gatekeeper pattern (AI Responsible Committee review before deployment). | How are governance decisions enforced in deployment pipeline? Can both platforms enforce consistently? | Yes — single governance plane enforces consistently. Gates apply to all workloads. | Yes — PATH gates apply; HAIL enforces. Requires explicit integration testing. | Deferred — governance gates added post-production. Initial self-service without formal gates. | P1 |
| **Policy Compliance Scanning** | Neither platform has formal pre-deployment compliance scanning. | Which platform is responsible for policy compliance checks (data residency, audit logging, PII handling)? | PATH owns compliance scanning; enforces before HAIL deployment. | Both platforms required to implement; coordination overhead. | HAIL implements post-production ATO. | P2 |

### 1.2 FinOps Attribution & Cost Clarity

| Dimension | Current State | Gap | Scenario A | Scenario B | Scenario C | Priority |
|---|---|---|---|---|---|---|
| **Per-Workload Cost Attribution** | HAIL: per-workload visibility via resource tagging. PATH: assumed enterprise-pooled cost model. | How are costs attributed to clients if platforms merge? If separate, how is shared infrastructure cost split? | Resolved — single FinOps model, shared cost pool, transparent per-client allocation via tags/subscriptions. | Unresolved — requires per-platform FinOps agreement; overhead of cost allocation logic. Must define shared service cost-sharing (e.g., two instances of Azure Policy, Purview). | Resolved — HAIL continues per-workload tagging. Single FinOps model. | P1 |
| **Shared Service Costs** | HAIL manages own shared services (logging, policy, Purview). PATH would introduce parallel governance shared services. | Will there be duplicate shared infrastructure? How are shared service costs allocated across platforms? | Unified shared services (one instance per service type). Cost allocated proportionally across workloads. | Duplicated — two instances of Azure Policy, Purview, audit logging infrastructure. Higher operational cost. | Single set of shared services (HAIL's current model). | P1 |
| **Budget Planning & Forecasting** | HAIL provides per-project cost projections. PATH cost model undefined. | Can finance plan for converged platform costs? Are cost projections consistent across scenarios? | Single FinOps model enables transparent budget planning. Cost forecasting simplified. | Two cost models make forecasting complex. Finance must maintain separate budgets per platform. | Single cost model (HAIL). Simpler budget planning. | P1 |

### 1.3 Operational Readiness & Staffing

| Dimension | Current State | Gap | Scenario A | Scenario B | Scenario C | Priority |
|---|---|---|---|---|---|---|
| **Platform Operations Team** | HAIL: minimal ops team; relies on self-service. PATH: governance team assigned, ops team undefined. | Who operates the converged platform? Does PATH governance team scale to operational support? | Single ops team. PATH governance embedded in CI/CD gates. HAIL ops scales to enterprise workload. | Two ops teams (one per platform). Coordination overhead. Potential SLA inconsistency. | HAIL ops team expands to include governance gates. | P1 |
| **SLA Definition** | HAIL: no formal SLA defined. PATH: no formal SLA defined. | What are RTO/RPO targets for each scenario? Are they consistent? | Single SLA across all workloads. Enforced consistently. | Per-platform SLAs (risk of inconsistency). Coordination overhead in escalation. | Single SLA (HAIL). | P2 |
| **Escalation Paths** | HAIL: escalates to PHAC operations. PATH: escalates to HC governance. | If workload fails, which team responds? Are escalation paths clear? | Single escalation path. Clear ownership. | Dual escalation paths (potential confusion). Requires explicit escalation contract. | Single escalation path (HAIL -> PHAC). | P2 |

---

## Pillar 2: Reliability

### 2.1 RTO/RPO Targets

| Dimension | Current State | Gap | Scenario A | Scenario B | Scenario C | Priority |
|---|---|---|---|---|---|---|
| **RTO Target** | Neither platform has defined RTO targets. Both assume 24-hour RPO by default. | Are 24-hour RPO targets acceptable for Protected B regulatory workloads (PMRA, surveillance)? | Must define jointly — single platform enforces single RTO/RPO posture. Likely: RTO 4 hours, RPO 1 hour for Protected B workloads. | Must define per-platform — potential inconsistency if standards differ. Risk: HAIL SLA differs from PATH's regulatory requirements. | Must define — HAIL's current implicit 24-hour RPO insufficient for regulatory use cases. Requires upgrade. | P1 |
| **Failover Mechanism** | HAIL: geo-redundant backup assumed but not validated. PATH: failover mechanism undefined. | Can both platforms fail over independently? Is failover behavior consistent? | Single failover mechanism. Validated and tested. Clear RTO/RPO guarantees. | Two failover mechanisms. Risk of cascading failures if PATH governance layer becomes unavailable. | Single failover mechanism (HAIL). Governance logic does not have independent failover. | P1 |
| **Backup & Recovery Testing** | Neither platform has formal backup testing schedule. | How often are backups tested? Can the platform actually recover within stated RPO? | Regular backup testing (quarterly minimum) enforced as part of governance gates. | Separate backup testing per platform. Higher overhead. | Backup testing coordinated with HAIL's operational process. | P2 |

### 2.2 Shared Dependencies & Cascade Failure Risk

| Dimension | Current State | Gap | Scenario A | Scenario B | Scenario C | Priority |
|---|---|---|---|---|---|---|
| **Shared Azure Components** | HAIL uses: AI Foundry, Databricks, App Service, PostgreSQL, Storage, Key Vault. PATH assumes similar stack. | Single point of failure if shared resource fails. Cascade impact unclear. | Mitigated — single platform, single governance layer for dependency management. Shared resources managed centrally. Clear cascade failure mitigation strategy. | Exposed — if platforms maintain separate instances, cascade risk duplicated (two Foundry instances, two governance models). Risk: if shared Foundry fails, both platforms down. | Mitigated — single set of shared resources. HAIL's current dependency management applies. | P1 |
| **Data Residency Constraints** | HAIL: declared Unclassified (Azure Canada regions). PATH: assumes Protected B (may require Azure.us). | Different data residency requirements create cascade risk. If Foundry only available in US, can Unclassified workloads run there? | Resolved — single platform enforces single data residency policy. All workloads on same cloud (Azure.us or Canada). | Risk — two platforms in different clouds (HAIL in Canada, PATH in US) creates data sovereignty complexity. Governance sync required. | Single data residency decision. HAIL determines if Canada or US. | P1 |
| **Cascading Dependency Failure** | No formal dependency map. | If Azure Policy fails, can workloads still deploy? Which platform is affected? | Single dependency map maintained. Governance plane separated from runtime plane — policy failure does not cascade to runtime. | Dual dependency maps. Risk of cascade if coordination layer (AI Responsible Committee) fails. | Single dependency map (HAIL). Policy dependency failure cascades to all deployments (governance deferred). | P1 |

### 2.3 Service Availability & Multi-Region Strategy

| Dimension | Current State | Gap | Scenario A | Scenario B | Scenario C | Priority |
|---|---|---|---|---|---|---|
| **Multi-Region Availability** | HAIL: single-region deployment (Canada Central assumed). PATH: undefined. | Can workloads run in multiple regions? Is failover cross-region or within-region? | Single multi-region strategy. Governance applied consistently across regions. | Per-platform multi-region strategy (may differ). Risk: redundancy models differ. | Single multi-region strategy (HAIL's choice). | P2 |
| **Service Availability SLA** | HAIL: no published SLA. PATH: no published SLA. | What is the target service availability (99.5%, 99.9%, 99.95%)? | Single published SLA (likely 99.5% for Sandbox, 99.9% for Production). | Per-platform SLAs (coordination overhead). Risk: inconsistent availability targets create operational confusion. | Single published SLA (HAIL). | P2 |

---

## Summary: Pillar Readiness by Scenario

### Scenario A (Converge): Operational Excellence & Reliability

**Operational Excellence:**
- ✅ Self-service model integrated into governance gates
- ✅ FinOps unified (resolved)
- ✅ Single ops team (clear ownership)
- ✅ Single SLA

**Reliability:**
- ✅ RTO/RPO targets defined jointly
- ✅ Single dependency map
- ✅ Cascade failure risk mitigated

**Maturity:** All P1 gaps addressable. Requires upfront integration work (2–3 months). Recommended.

---

### Scenario B (Co-Equal): Operational Excellence & Reliability

**Operational Excellence:**
- ⚠️ Self-service model requires explicit API contract (partial mitigation)
- ⚠️ FinOps complexity (two cost models, allocation overhead)
- ⚠️ Two ops teams (coordination overhead)
- ⚠️ Per-platform SLAs (risk of inconsistency)

**Reliability:**
- ⚠️ Per-platform RTO/RPO targets (risk of inconsistency)
- ⚠️ Dual dependency maps (cascade failure risk exposed)
- ⚠️ Two-platform failure scenarios (coordination required)

**Maturity:** P1 gaps partially addressable. Ongoing coordination overhead. Higher operational risk.

---

### Scenario C (PHAC-Led): Operational Excellence & Reliability

**Operational Excellence:**
- ✅ Self-service model continues (no change)
- ✅ FinOps unified (HAIL model)
- ✅ Single ops team (HAIL expands)
- ✅ Single SLA

**Reliability:**
- ⚠️ RTO/RPO targets must be upgraded (HAIL's 24-hour RPO insufficient for Protected B)
- ✅ Single dependency map
- ⚠️ Governance enforcement deferred (cascade risk unmitigated initially)

**Maturity:** Fastest path to initial delivery. Governance maturity deferred. Medium reliability risk.

---

## Recommendations

### For ARB Decision:

1. **Scenario A (Converge)** is most mature from WAF perspective. Operational Excellence and Reliability gaps are resolvable within integration timeline.

2. **Scenario B (Co-Equal)** introduces ongoing operational overhead. Recommend only if Scenario A timeline is unacceptable.

3. **Scenario C (PHAC-Led)** requires post-production governance and reliability upgrades. Higher risk of shadow AI and SLA gaps during interim period.

### For Implementation (If Scenario A or B Selected):

1. **Operational Excellence Workstream:**
   - Finalize FinOps model (unified vs. split) by Q2 2026
   - Define governance gates and CI/CD integration by Q1 2026
   - Plan ops team structure and SLA definitions by Q2 2026

2. **Reliability Workstream:**
   - Define RTO/RPO targets aligned with regulatory requirements by Q1 2026
   - Map shared dependencies and cascade failure scenarios by Q1 2026
   - Design governance failure isolation (governance plane independent from runtime) by Q2 2026
   - Schedule quarterly backup recovery testing by Q3 2026

---

## Quality Gate

**Stakeholder Sign-off:**

- [ ] Security (Kirk): ATO path and data residency constraints confirmed
- [ ] Cloud Operations (Jason): FinOps model and Foundry availability feasible
- [ ] Finance: Cost attribution model acceptable
- [ ] PMRA/Regulatory (Sam): SLA targets meet regulatory requirements

---

*This assessment is an EA/TPO working reference. It represents EA team working interpretation, not citeable GC policy.*

*Classification: Unclassified / For Internal Use*
