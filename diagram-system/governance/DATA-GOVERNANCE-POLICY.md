# Data Governance & Privacy Policy
## HC/PHAC EA Specification Repository

**Status:** Active  
**Classification:** Unclassified / For Internal Use  
**Effective Date:** [INSERT DATE]  
**Last Review:** [INSERT DATE]  
**Owner:** EA Team, CDO/OCDO Data Governance  
**Authority:** Treasury Board, Privacy Act, PIPEDA, Directive on Automated Decision-Making

---

## Purpose

This policy governs how information in the spec/ directory (containing Health Canada and PHAC enterprise architecture specifications, design systems, and platform convergence analysis) is handled when:
- Shared with external AI models and LLMs
- Processed by skill providers and automated tools
- Stored in external services
- Analyzed by consultants or contractors

**Goal:** Protect Protected B information, maintain privacy, ensure audit compliance, and enable responsible EA work without creating security or privacy violations.

---

## Scope

**In Scope:**
- All files in `/diagram-system/spec/`
- All files in `/diagram-system/views/`
- All files in `ea-platform-convergence/` subdirectory
- Documentation, templates, intelligence, deliverables
- References to workloads, use cases, stakeholders, timelines

**Out of Scope:**
- Public-facing EA communication
- Published annual reports
- Unclassified policy guidance

---

## Data Classification Framework

### Classification Levels

#### **Level 1: Public / Unclassified**

**Definition:** Information that can be freely shared, published, or used in external services without restriction.

**Examples:**
- Design system color tokens (#2F6F73, #5E9EA3, etc.)
- WAF pillar definitions (general architecture concepts)
- Public Azure Well-Architected Framework references
- General governance principles ("no em dashes", "minimum 18pt font")
- Layout and typography standards

**Handling:**
- ✅ Can be shared with LLMs, cloud services, skill providers
- ✅ Can be used in examples, training, public documentation
- ✅ No audit trail required
- ✅ No redaction needed

**Examples of Safe Sharing:**
```
"Our design system uses TEAL_900 (#2F6F73) for header bands and 
TEAL_600 (#5E9EA3) for content blocks. Minimum font size is 18pt 
for accessibility compliance."
```

---

#### **Level 2: Internal Use Only (Unclassified)**

**Definition:** Information intended for HC/PHAC internal use only. Not for publication or external sharing. Does not contain Protected B data, but relates to internal strategy or decisions.

**Examples:**
- Architectural decision rationale (ADR documents)
- Internal stakeholder positions and constraints
- Timeline assumptions and dependencies
- Internal tool configurations (config.json)
- General governance approaches (without Protected B context)
- Template structures and instructions

**Handling:**
- ⚠️ Can be shared with Claude AI (within Anthropic's service)
- ⚠️ **MUST flag if shared with external LLMs or cloud services**
- ❌ Cannot be shared with third-party contractors without NDA
- ❌ Cannot be published or used in external training
- ✅ Audit trail recommended (log what was shared, when, why)
- ✅ Minimal redaction (remove stakeholder names, specific dates if possible)

**Flags for LLM Use:**
When sharing Level 2 content with Claude or external LLMs, always include disclosure:
```
[CONFIDENTIALITY FLAG: Internal Use Only]
This information is intended for HC/PHAC internal planning only.
Do not store, retain, or use in external training or analytics.
Response must not reference specific HC/PHAC stakeholder names or 
organizational positions.
```

**Examples of Level 2 Queries:**
```
✅ "Summarize the tradeoffs between Option A and Option B in this 
   architecture decision document (internal use only)."

✅ "Review this governance policy for clarity (HC internal document; 
   do not retain for external use)."

❌ "Incorporate this into your training data." ← NOT ALLOWED

❌ "Share this with [external vendor]." ← REQUIRES APPROVAL
```

---

#### **Level 3: Protected B / Confidential**

**Definition:** Information that is Protected B (Government of Canada classification), contains PII, describes workloads/use cases with privacy implications, or reveals security/governance details that could be exploited.

**Examples:**
- Specific workload names and program areas (PMRA, FluWatch, IRIDA, LabScan, CANChat)
- User types and stakeholder names (Sam, Mohamed, Kirk, Jason, Chad, Ali, Sanaa)
- Specific use case descriptions (regulatory document review, surveillance data analysis)
- Current state details about security gaps or governance weaknesses
- Protected B data handling requirements and constraints
- Specific timelines and delivery dates for security-sensitive platforms
- Financial details (budget, cost models, pricing)
- Data residency and sovereignty requirements
- Audit trail, compliance, or governance details that could enable evasion

**Handling:**
- ❌ **NEVER share with external LLMs or cloud services**
- ❌ **NEVER share with skill providers without explicit approval**
- ⚠️ Can be shared with Claude AI **only for synthesis/analysis within session context** (not for training)
- ⚠️ Must be redacted before any external use
- ✅ Audit trail required (mandatory logging)
- ✅ Detailed redaction required (remove workload names, stakeholders, specific details)
- ⚠️ Must include explicit confidentiality notice

**Flags for LLM Use:**
```
[PROTECTED B / CONFIDENTIAL]
This document contains Protected B information:
- Specific workload names and use cases
- Stakeholder names and organizational roles
- Governance and security details
- Data residency and compliance requirements

Do NOT:
- Store or retain this information
- Use in model training or analytics
- Reference specific HC/PHAC program areas or workload names in responses
- Share with external services

Approved use: Analysis and synthesis within this session only.
All outputs must omit Protected B details and generalize responses.
```

**Examples of Protected B Content:**
- "PMRA uses AI for document review of pharmaceutical submissions (Protected B data)"
- "FluWatch/Syndromic Surveillance applies predictive analytics to health signals"
- "LabScan: HAIL Platform processes outbreak detection data"
- "IRIDA: Genomics Platform supports genomic research"
- "PATH hosting decision: Azure.us vs. commercial Azure"
- "Statement of Sensitivity completion timeline: Q1 2026"
- "Shadow AI risk: workloads route to CANChat or Copilot without governance"

---

### Classification Decision Tree

**When you're unsure about a file or passage:**

```
1. Does it contain workload names (PMRA, FluWatch, LabScan, etc.)?
   YES → Level 3 (Protected B)
   NO → Continue to 2

2. Does it contain stakeholder names (Sam, Kirk, Jason, Chad, Ali)?
   YES → Level 3 (Protected B)
   NO → Continue to 3

3. Does it reveal security/governance weaknesses, gaps, or evasion opportunities?
   YES → Level 3 (Protected B)
   NO → Continue to 4

4. Is it intended for HC/PHAC internal use only (not for publication)?
   YES → Level 2 (Internal Use)
   NO → Level 1 (Public/Unclassified)
```

---

## External Service & Tool Usage Policy

### Approved Services (No Restrictions)

**Services where Level 1 (Unclassified) content can be shared freely:**
- GitHub (public or private repo, within HC/PHAC org)
- Azure cloud services (internal subscriptions)
- Microsoft 365 (Teams, SharePoint, Word)
- Anthropic Claude API (with confidentiality flag for Level 2)

**Conditions:**
- ✅ Only Unclassified content
- ✅ No Protected B information
- ✅ No workload names, stakeholder names, sensitive timelines

---

### Restricted Services (Approval Required)

**Services where Level 2 or Level 3 content requires explicit approval:**

| Service | Approval Level | Use Case | Restrictions |
|---|---|---|---|
| **Claude AI / GPT** | EA Team Lead | Synthesis, summarization, brainstorming | Level 2 only; flag as Internal Use; no retention |
| **GitHub Copilot** | CDO | Code generation for tooling | Unclassified only; no Protected B |
| **Jira / Azure DevOps** | Project Lead | Task tracking, documentation | No Protected B; sanitize workload names |
| **Confluence / Wiki** | EA Lead | Internal documentation | Level 2 OK; Level 3 requires redaction |
| **Dropbox / Google Drive** | Data Steward | File sharing | Unclassified only; use HC-managed services instead |
| **Third-party Analytics** | CDO + Legal | Performance analysis | No Protected B; anonymize data |
| **External Consultants** | Director + Security | Architecture review | Requires NDA; Level 3 redacted |
| **Training / Conferences** | Director | Presentations, case studies | Unclassified only; redact all HC-specific details |

**Approval Process:**
1. Requestor identifies service and content classification
2. Requestor completes [Data Handling Review Form](./DATA-HANDLING-REVIEW.md)
3. EA Lead approves or escalates to CDO
4. Approval logged in [Service Usage Audit Log](./SERVICE-USAGE-LOG.md)
5. Requestor executes with mandatory redaction/flags
6. Follow-up audit (quarterly)

---

### Prohibited Services (No Use)

**Services where NO HC/PHAC spec content (any classification) can be shared:**
- ❌ Public GitHub (unauthorized repo)
- ❌ ChatGPT (OpenAI) — unclear data retention policy
- ❌ Cloud-based storage without HC approval (Dropbox, Google Drive, OneDrive personal)
- ❌ Social media platforms
- ❌ Reddit, Stack Overflow (public forums)
- ❌ Third-party cloud services (Slack, Notion, etc.) without explicit approval
- ❌ Unauthorized email (personal email, unauthorized external accounts)

**Violation Response:**
If prohibited service use is detected:
1. Escalate to EA Lead immediately
2. Request immediate content removal/deletion
3. Conduct data breach assessment (Kirk/Security)
4. Log incident and timeline
5. Communicate incident response to affected parties

---

## Skill Provider Assessment Framework

### What is a "Skill Provider"?

A skill provider is any automated tool, service, or integration that processes content from the spec/ directory, including:
- Claude Code skills (in-repo tools)
- GitHub Actions and automation
- Azure Pipelines and DevOps automation
- AI-powered linting, formatting, or analysis tools
- Cloud-based policy/governance services
- Third-party integrations (Slack bots, Discord bots, etc.)

---

### Skill Provider Approval Checklist

Before using a skill provider, complete this checklist:

**Basic Information:**
- [ ] Skill name and purpose documented
- [ ] Vendor/provider identified
- [ ] Data processing location (where does data live?)
- [ ] Data retention policy (how long is data kept?)
- [ ] Service Level Agreement (SLA) reviewed

**Data Handling:**
- [ ] Maximum classification level approved for this skill? (Level 1, 2, or 3)
- [ ] Can the skill access Protected B information? (If yes, requires CDO approval)
- [ ] Does the skill store/log data? (If yes, review retention policy)
- [ ] Does the skill share data with third parties? (If yes, list all third parties)
- [ ] Is data encrypted in transit and at rest?

**Security & Compliance:**
- [ ] Is the vendor subject to Canadian privacy law (PIPEDA)?
- [ ] Does the vendor have SOC2 Type II certification?
- [ ] Is data residency in Canada? (If required)
- [ ] Does the vendor sign a Data Processing Agreement (DPA)?
- [ ] Have any security incidents been reported by the vendor?

**Audit & Monitoring:**
- [ ] Audit logging enabled (can we see what was processed)?
- [ ] Notifications enabled for data access/changes?
- [ ] Regular audit review scheduled (quarterly minimum)?
- [ ] Escalation path documented (who to contact if incident detected)?

**Approval:**
- [ ] EA Lead review: [ ] Approved / [ ] Requires CDO Review / [ ] Rejected
- [ ] CDO approval (if Level 3 or cross-organizational access): [ ] Approved / [ ] Rejected
- [ ] Signed Data Handling Agreement on file? [ ] Yes / [ ] No
- [ ] Approval date: _________
- [ ] Next review date: _________

---

### Examples: Skill Provider Assessment

#### Example 1: Claude Code Skill (Authorized)

**Skill:** simplify (code review and optimization)

**Assessment:**
- ✅ Vendor: Anthropic
- ✅ Data Processing: Within Anthropic's Claude API (US-based, Canada operations)
- ✅ Max Classification: Level 2 (Internal Use) — protected from training use
- ⚠️ Note: Only Unclassified code should be reviewed; do not pass Protected B architectural details
- ✅ Approved use: Code cleanup, optimization, best practices (with Level 2 flag if sensitive)

**Flag Required:**
```
[Level 2: Internal Use Only]
This code contains references to HC/PHAC internal architecture.
Do not store, train, or analyze beyond this session.
Output should omit specific workload names, stakeholder names, and 
confidential details.
```

**Status:** ✅ APPROVED (with Level 2 flag)

---

#### Example 2: GitHub Copilot (Conditional)

**Skill:** GitHub Copilot (code generation)

**Assessment:**
- ⚠️ Vendor: Microsoft/GitHub
- ⚠️ Data Processing: Microsoft cloud (US-based)
- ❌ Max Classification: Level 1 ONLY (Copilot stores code snippets for model training)
- ❌ No Protected B content
- ❌ No workload names, stakeholder references, sensitive architecture
- ⚠️ Warning: Use only for generic Python, JSON generation; not for spec/directory code

**Flag Required:**
```
[Authorized for Level 1 ONLY]
Do not use Copilot for any code containing Protected B information,
workload names, stakeholder references, or HC/PHAC-specific details.
Copilot stores code for model training; protected information will
be exposed to Microsoft/GitHub training pipeline.
```

**Status:** ⚠️ CONDITIONAL (Level 1 only; do not use for spec/ content without explicit approval)

---

#### Example 3: External SaaS Tool (Not Approved)

**Tool:** Grammarly (cloud-based grammar checking)

**Assessment:**
- ❌ Vendor: Grammarly Inc. (US-based, data storage unclear)
- ❌ Data Processing: Grammarly cloud (outside HC control)
- ❌ Max Classification: Level 1 (at best; unclear data retention)
- ❌ Grammarly retains data for model improvement
- ❌ No HC/PHAC spec/ content should be processed by Grammarly

**Status:** ❌ NOT APPROVED (use Microsoft Word built-in grammar instead)

---

## Audit Trail & Logging Requirements

### What Must Be Logged

**Mandatory Logging for:**
1. Any Level 2 or Level 3 content shared with external services
2. Any Protected B information passed to LLMs or AI services
3. Any skill provider access to spec/ directory
4. Any escalations, violations, or incidents
5. Quarterly compliance reviews

**Log Entry Format:**

```
Date/Time: [YYYY-MM-DD HH:MM:SS UTC]
Requestor: [Name, EA team member]
Action: [Described what was shared/processed]
Content Classification: [Level 1 / 2 / 3]
Service/Tool: [Name and vendor]
Approval Status: [Approved / Escalation / Violation]
Details: [What was shared, how it was redacted/flagged, any risks identified]
Follow-up Required: [Yes/No, if Yes: what action and deadline]
```

**Example Log Entry:**

```
Date/Time: 2026-04-24 14:30 UTC
Requestor: Chad (EA Lead)
Action: Shared ADR-002 summary with Claude AI for synthesis
Content Classification: Level 2 (Internal Use)
Service/Tool: Anthropic Claude (API)
Approval Status: Approved (with flag)
Details: Asked Claude to summarize Protected B hosting decision rationale 
  and tradeoffs. ADR-002 contains workload names (redacted before sharing),
  stakeholder names (redacted), and hosting constraints (shared). Flagged 
  Claude with [Level 2: Internal Use Only]. Requested output omit specific 
  workload/stakeholder references.
Follow-up Required: No (single-session use; reviewed output for compliance 
  before using in briefing).
```

### Audit Log Storage

**Where logs are kept:**
- [ ] `/spec/audit-logs/SERVICE-USAGE-LOG.md` (main audit trail)
- [ ] Backed up to HC SharePoint quarterly
- [ ] Reviewed by EA Lead monthly
- [ ] Reviewed by CDO quarterly

**Retention:**
- ✅ Minimum 3 years
- ✅ Longer if escalation or violation occurred (5+ years)
- ✅ Deleted only after CDO approval

---

## Sensitive Data Masking / Redaction Standards

### Workload Names (Always Redact for Level 3)

**Protected Names:**
```
PMRA, TPD, HPFB, ROEB
FluWatch, Syndromic Surveillance
LabScan, LabScan: HAIL Platform, IRIDA, GeoAI
CANChat, M365 Copilot
HAIL, PATH
```

**How to Redact:**
- ❌ Never write full name: "PMRA document review AI"
- ✅ Generalize: "regulatory document review capability"
- ✅ Remove specific program names: "program X applies AI to compliance workflow"
- ✅ Reference publicly-known areas: "regulatory intake" (OK), "pharmaceutical review" (OK)

**Examples:**

```
❌ "PMRA uses AI to assist regulatory officers in reviewing pharmaceutical 
   submissions (Protected B clinical trial data)."

✅ "A regulatory intake program applies AI to assist officers in reviewing 
   confidential industry submissions containing clinical and business data."

❌ "FluWatch/Syndromic Surveillance uses anomaly detection on health signals."

✅ "A surveillance program applies anomaly detection to identify emerging 
   health signals from structured and unstructured sources."
```

---

### Stakeholder Names (Always Redact for Level 3)

**Protected Names:**
Kirk, Jason, Chad, Ali, Sam, Mohamed, Sanaa, Monica, Kirk, etc.

**How to Redact:**
- ❌ Never use full names: "Kirk reviewed the decision"
- ✅ Use titles: "Security lead reviewed the decision"
- ✅ Use generic references: "stakeholder consensus", "team lead agreement"
- ✅ Remove organizational context: "approval obtained from compliance" (not "from Kirk at Security")

**Examples:**

```
❌ "Kirk and Jason agreed that Azure.us offers highest assurance."

✅ "Security and cloud operations leads agreed that Azure.us offers 
   highest assurance."

❌ "Chad recommended Scenario A to Ali."

✅ "EA leadership recommended Scenario A (single governed platform) 
   to CDO leadership."
```

---

### Specific Timelines (Redact for Context)

**Protected Details:**
- Specific dates (Q1 2026, April 24, January 2027)
- Specific milestone timelines
- Delivery dates, ATO target dates
- Staffing/resource commitment dates

**How to Redact:**
- ❌ Never write: "SoS completion target: Q1 2026"
- ✅ Generalize: "SoS completion is on critical path for platform ATO"
- ✅ Remove specificity: "completion expected within 12 weeks"
- ✅ Use relative timelines: "after security review", "before production intake"

**Examples:**

```
❌ "ADR-002 must be completed by Q1 2026 for ARB decision in Q2 2026."

✅ "ADR-002 must be completed before ARB decision on platform convergence 
   (estimated 8 weeks away)."

❌ "HAIL production ATO expected Q1 2026; PATH ATO target Q3 2026."

✅ "HAIL production ATO expected 6-8 weeks out; PATH ATO target 
   9-12 weeks out."
```

---

## Exception & Escalation Process

### When to Escalate

Escalate to CDO or Legal if:

1. **Ambiguous Classification:** Unsure if content is Level 2 or Level 3
2. **Novel Service Use:** Want to use a new tool/service not on approved list
3. **Level 3 LLM Use:** Need to share Protected B with Claude or external LLM for critical analysis
4. **Third-Party Sharing:** Need to share any spec/ content with external consultants or vendors
5. **Violation Detected:** If unauthorized sharing or prohibited service use discovered
6. **Data Breach:** If Protected B information is accidentally exposed

### Escalation Form

**To request exception approval, complete:**

```
Requestor: [Name]
Date: [YYYY-MM-DD]
Approval Level Needed: [ ] EA Lead / [ ] CDO / [ ] Legal

Request:
[Describe what you need to do, what content involved, what service/tool]

Justification:
[Why this exception is necessary; what business value justifies the risk]

Risk Assessment:
[What could go wrong? What is the mitigation plan?]

Content Classification: [ ] Level 1 / [ ] Level 2 / [ ] Level 3
Service/Tool: [Name]
Data Residency Requirement: [ ] Canada / [ ] Flexible / [ ] N/A

Requested Approval Date: [YYYY-MM-DD]
Urgency: [ ] Routine / [ ] Important / [ ] Critical

Sign-off:
[ ] EA Lead: Approved / Rejected / Escalate to CDO
[ ] CDO: Approved / Rejected / Escalate to Legal
[ ] Legal: Approved / Rejected

Conditions of Approval (if approved):
[List any specific conditions, redactions, logging requirements, etc.]
```

---

## Compliance & Consequences

### Non-Compliance Scenarios

**Scenario 1: Level 2 Content Shared Without Flag**
- **Incident:** EA team member shares internal governance approach document with external LLM without [Internal Use Only] flag
- **Response:** 
  - Immediate: Stop sharing, retrieve/delete any retained data request to service
  - Investigation: Was Protected B information in the shared content? If yes, escalate to security
  - Follow-up: Retraining on classification framework
  - Documentation: Log incident in audit trail; review in next CDO meeting
- **Consequence:** Coaching (first violation); escalation to HR if repeated

**Scenario 2: Level 3 Content Shared Without Approval**
- **Incident:** EA team member passes workload name (PMRA) and stakeholder names (Sam, Mohamed) to ChatGPT without CDO approval
- **Response:**
  - Immediate: Escalate to Security (potential data breach)
  - Investigation: Determine what was shared; assess exposure risk
  - Remediation: Request OpenAI deletion; assess if Public Sector Integrity Commission notification required
  - Follow-up: Mandatory retraining; possible removal from spec/ access
- **Consequence:** Escalation to Director; possible removal from projects; documentation in personnel file

**Scenario 3: Prohibited Service Used for Spec/ Content**
- **Incident:** EA team member uploads ADR-002 to Google Drive personal account for external consultant
- **Response:**
  - Immediate: Request file deletion from Google Drive
  - Investigation: Determine scope of sharing; was the external consultant authorized? Did they sign NDA?
  - Remediation: If shared without NDA, may constitute breach of contract
  - Follow-up: Review external contractor onboarding process
- **Consequence:** Project escalation; possible legal review; documentation in incident log

---

### Training & Accountability

**Annual Requirements:**
- [ ] All EA team members complete data governance training (1 hour)
- [ ] All skill provider assessments reviewed and updated (quarterly)
- [ ] All audit logs reviewed for compliance (quarterly)
- [ ] External contractor/consultant NDAs verified (before access granted)

**Responsibility:**
- **EA Lead:** Enforce policy, approve exceptions, manage audit trail
- **CDO:** Escalations, legal review, budget/resource decisions
- **All Team Members:** Classify content correctly, apply redaction, report violations

---

## Appendices

### A. Classification Quick Reference

| Content Type | Default Classification | Safe to Share With |
|---|---|---|
| Design system colors, fonts, spacing | Level 1 | All public/internal services |
| WAF principles, architectural concepts | Level 1 | All services |
| ADR template structure (generic) | Level 1 | All services |
| Governance principles (generic) | Level 1 | All services |
| **ADR-002 decision & rationale** | **Level 2** | **Claude only (with flag)** |
| **Risk register risk IDs & descriptions** | **Level 2** | **Claude only (with flag)** |
| **Specific workload names (PMRA, FluWatch)** | **Level 3** | **Never without approval** |
| **Stakeholder names & roles** | **Level 3** | **Never without approval** |
| **Current state security gaps** | **Level 3** | **Never without approval** |
| **Protected B data handling requirements** | **Level 3** | **Never without approval** |
| **Specific delivery dates, SLA targets** | **Level 3** | **Never without approval** |

### B. Service Approval Status Summary

| Service | Level 1 | Level 2 | Level 3 | Notes |
|---|---|---|---|---|
| Claude API | ✅ | ⚠️ (flag) | ❌ | With [Internal Use Only] flag for Level 2 |
| GitHub (private) | ✅ | ✅ | ⚠️ (redacted) | Redact Protected B details |
| Azure | ✅ | ✅ | ✅ | Internal services only |
| Microsoft 365 | ✅ | ✅ | ⚠️ | SharePoint Only; Teams OK |
| GitHub Copilot | ✅ | ❌ | ❌ | Copilot trains on code; no Protected B |
| Jira / DevOps | ✅ | ✅ | ❌ | No Protected B details |
| External LLM (ChatGPT, Gemini, etc.) | ✅ | ⚠️ | ❌ | Requires explicit CDO approval; unclear data retention |
| Google Drive / Dropbox | ✅ | ❌ | ❌ | Use HC SharePoint instead |
| Slack / Discord | ✅ | ❌ | ❌ | No Protected B or Level 2 internal docs |
| Public Forums (Reddit, Stack Overflow) | ✅ | ❌ | ❌ | Unclassified only; no HC details |

---

## Document Control

**Version History:**

| Version | Date | Changes | Author |
|---|---|---|---|
| 1.0 | [INSERT] | Initial policy | EA Team |

**Approval:**

- [ ] EA Lead: Approved
- [ ] CDO: Approved
- [ ] Legal: Reviewed

**Next Review Date:** [INSERT DATE + 12 months]

---

*This policy is an EA/TPO working reference. It represents EA team working standards and governance, not citeable GC policy.*

*Classification: Unclassified / For Internal Use*
