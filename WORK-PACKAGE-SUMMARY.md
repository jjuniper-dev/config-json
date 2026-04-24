# EA Specification Repository — Complete Work Package

## HC/PHAC Data Governance & Platform Convergence Analysis Infrastructure

**Date:** April 24, 2026
**Classification:** Unclassified / For Internal Use
**Working Copy:** jjuniper-dev/config-json (GitHub — personal account, working copy only)
**Canonical Repository (Required):** GCcode (SSC-hosted GitLab CE) — to be registered under a DTB group account before circulation or citation
**Main Branch Commit:** 4923916 (Merge PR #3)

> **Storage governance note:** Per HC/PHAC EA working standards, unclassified EA artifacts must be version-controlled on GCcode under a registered group account. This GitHub repository is a personal working environment and must not be treated as the authoritative or citable source. Migration to GCcode is required before this work package is shared with stakeholders, cited in ARB submissions, or referenced in any deliverable.

-----

## Executive Summary

This work package delivers a governance and analysis infrastructure for Health Canada and PHAC enterprise architecture work, specifically:

1. **Data Governance Framework** — Policy and procedures for safely handling Protected B information when sharing with external services, LLMs (Claude, ChatGPT), and skill providers
1. **EA Platform Convergence Agent** — Structured methodology and charter for Architecture Review Board (ARB) assessment of the PATH/HAIL convergence decision. PATH is the AI Runtime / Execution Layer pattern framework (HC-led, pre-prototype, not approved to proceed). HAIL is the operational AI runtime environment (PHAC-led, deployed March 2026). The convergence question concerns whether these two components of the enterprise AI platform should be governed under a unified operating model or remain independently managed with defined integration points.

**Scope:**

- Enables safe use of external AI services for EA work without exposing Protected B information
- Provides a decision framework for the PATH/HAIL convergence ARB decision (3 scenarios with tradeoff analysis)
- Establishes audit trail and compliance procedures (DADM, AIA, PIA, TBS Policy on Government Security)
- Supports stakeholder validation and ARB-ready briefing preparation

-----

## Package Components

### 1. Data Governance Framework

**Location:** `diagram-system/governance/`

**Purpose:** Policies and procedures for classifying and handling spec/ directory content when sharing with external services, cloud tools, and AI services.

**Files (4 documents, 1,696 lines):**

- **README.md** (227 lines) — Quick start guide, core rules, FAQ
- **DATA-GOVERNANCE-POLICY.md** (679 lines) — Comprehensive policy
- **DATA-HANDLING-CHECKLIST.md** (375 lines) — Step-by-step team guidance
- **APPROVED-SKILLS.md** (415 lines) — Tool approval status matrix

**Data Classification (3 Levels):**

- **Level 1 (Public):** Design system, WAF principles. Share with anyone.
- **Level 2 (Internal Use):** ADRs, governance content. Share with Claude (with flag) and HC tools only. Note: "Internal Use" is a working classification for this framework and does not replace standard GC classification (Unclassified / Protected A / Protected B).
- **Level 3 (Protected B):** Workload names, stakeholder names, timelines. Never share without CDO approval.

**Service Approval Status:**

Note: The approvals below reflect EA team working practice for personal use of these tools. They are not citeable GC policy and do not substitute for departmental authorization. The GC-sanctioned AI tools for HC/PHAC are CANChat, GCTranslate, Microsoft Copilot (Phase 3 in development), and Cohere. CANChat ATO dependency is a registered risk.

- Claude AI (Level 1 and 2 with flag) — personal EA working use; not departmentally authorized
- GitHub private (Level 1-3 redacted) — working copy only; canonical storage must be GCcode
- Microsoft 365 (Level 1-3) — GC-authorized
- Azure (Level 1-3) — GC-authorized via SSC CBS
- ChatGPT (Level 1 only; Level 2 needs CDO approval) — not GC-authorized
- GitHub Copilot (Level 1 only) — not GC-authorized
- Slack (Level 1 only) — verify departmental authorization
- Dropbox, Google Drive, Public Forums — prohibited

-----

### 2. EA Platform Convergence Agent

**Location:** `diagram-system/spec/ea-platform-convergence/`

**Purpose:** Complete charter, configuration, and deliverable templates for ARB assessment of the PATH/HAIL convergence decision.

**Core Files (4 documents + 5 templates, 2,106 lines):**

**Charter and Configuration:**

- **EA-Agent-Instructions-v1.md** (225 lines) — Master charter with 7 sections: role, context, framework, deliverables, interaction, standards, success criteria
- **config.json** (163 lines) — Agent configuration (scenarios, stakeholder map, assessment framework, success metrics)
- **USAGE.txt** (164 lines) — Quick reference (deliverables, timeline, escalation triggers)
- **README.md** (261 lines) — Agent overview, directory structure, 5-phase workflow

**Deliverable Templates (5 P-Prioritized Documents):**

1. **convergence-framing-template.md** (256 lines) — P1: ARB decision framing with 3 scenarios A/B/C and tradeoff analysis
1. **waf-assessment-template.md** (179 lines) — P2: WAF pillar assessment (Operational Excellence, Reliability, Security, Cost Optimization)
1. **risk-register-template.md** (300 lines) — P3: Risk register with 5 convergence risks and scenario impact
1. **adr-template.md** (est. lines) — P4: ADR-002 Protected B hosting architecture (SA&A path for Azure Canada via SSC CBS and CCCS PBMM compliance)
1. **shadow-ai-narrative-template.md** (246 lines) — P5: Shadow AI risk business narrative for executives

**Supporting Subdirectories:**

- `templates/` — Working templates (above 5 files)
- `deliverables/` — Empty; ready for completed, signed-off versions
- `intelligence/` — Empty; ready for reference documents (HAIL/PATH current state, etc.)

-----

## How to Use This Package

### Phase 1: Onboarding (Day 1-2)

1. Read `EA-Agent-Instructions-v1.md` (charter, scope, success criteria)
1. Review `config.json` (scenarios, stakeholder map)
1. Skim `USAGE.txt` (quick overview)
1. Review `diagram-system/governance/README.md` (data governance rules)

### Phase 2: Stakeholder Validation (Week 1)

- Schedule meetings with Kirk (Security), Jason (Cloud Ops), Sam (PMRA), Chad (EA Leadership)
- Validate assumptions on ATO path, FinOps, use cases, strategy alignment
- Document feedback in feedback log

### Phase 3: Draft Deliverables (Week 2)

1. Copy templates to deliverables/ and populate with analysis
1. Start with P1 (Convergence Framing) — fill in scenarios A/B/C
1. Use P2 (WAF Assessment) as evidence
1. Draft P3 (Risk Register) in parallel
1. Reference P4 (ADR-002) and P5 (Shadow AI Narrative)

### Phase 4: Feedback and Iteration (Week 3)

- Share drafts with stakeholders
- Incorporate feedback
- Quality gate: Does ARB have enough to decide?

### Phase 5: Final Package (Week 4)

- Obtain stakeholder sign-off
- Package all deliverables for ARB
- Ready for ARB meeting (4-6 weeks out)

-----

## Data Governance Integration

**Before sharing any spec/ content with Claude, ChatGPT, GitHub Copilot, or external services:**

1. **Classify:** Level 1, 2, or 3? (Use decision tree)
1. **Check approval:** Verify tool is approved for that classification
1. **Add flag (if Level 2):** Include `[Level 2: Internal Use Only]` when sharing with Claude
1. **Redact (if Level 3):** Remove workload names, stakeholder names, specific timelines
1. **Log (if Level 2 or 3):** Record what was shared, when, why, approvers
1. **Review:** Check response for Protected B leakage

**Example Safe Claude Query (Level 2):**

```
[Level 2: Internal Use Only]

Please summarize the tradeoffs in this approach.
Omit HC/PHAC organizational references.
```

**Example Protected B Escalation (Level 3):**

```
Content contains workload names (PMRA, FluWatch) and stakeholder names.
This is Level 3 (Protected B).
Action: Escalate to EA Lead before sharing anywhere.
```

-----

## Success Criteria

ARB has three explicit convergence options with tradeoff analysis (P1).

EA recommended position is stated and defensible.

Stakeholders reviewed and signed off:

- Security (Kirk): ATO path and data residency confirmed
- Cloud Ops (Jason): Foundry availability and FinOps feasibility confirmed
- PMRA (Sam): Use case priority and governance confirmed
- EA Leadership (Chad): DTB strategy alignment confirmed

Risk register is current (flags P1 items mitigated by convergence decision).

ADR-002 completed (linked from P1 document).

All deliverables are clean, single-file, ARB-ready.

-----

## Escalation Triggers

Stop and escalate to EA Lead immediately if:

- Timeline slips past 2-week P1 draft deadline
- Stakeholder feedback contradicts core assumptions
- Risk register identifies new P1 item
- ADR-002 decision blocked by unresolved constraint
- Protected B information accidentally exposed
- Any convergence scenario becomes infeasible

**Escalation Chain:**

1. EA Lead (Chad)
1. Security Lead (Kirk) if data breach suspected
1. CDO if policy violation

-----

## Directory Structure

```
diagram-system/
├── governance/
│   ├── README.md
│   ├── DATA-GOVERNANCE-POLICY.md
│   ├── DATA-HANDLING-CHECKLIST.md
│   └── APPROVED-SKILLS.md
│
├── spec/
│   ├── [visual design specs]
│   └── ea-platform-convergence/
│       ├── EA-Agent-Instructions-v1.md
│       ├── config.json
│       ├── USAGE.txt
│       ├── README.md
│       ├── templates/ (5 deliverable templates)
│       ├── deliverables/ (empty, ready)
│       └── intelligence/ (empty, ready)
│
├── views/
│   └── [architecture views]
│
└── output/
    ├── pptx/
    └── svg/
```

-----

## Package Statistics

**Total Deliverables:** 13 files
**Git Status:** Merged to main (2026-04-24, Commit 4923916)
**Ready for Use:** Yes (working copy only; migrate to GCcode before stakeholder circulation)

-----

## Next Steps

1. **Migrate to GCcode** — Register repository under a DTB group account on GCcode before any stakeholder sharing or ARB citation (immediate)
1. **Confirm charter scope** — Does role, constraints, and success criteria align?
1. **Schedule stakeholder meetings** — Kirk, Jason, Sam, Chad (Week 1)
1. **Begin P1 draft** — Copy template, fill in scenarios A/B/C (Week 2)
1. **Validate governance policy** — Confirm data handling rules with team (immediate)
1. **Establish audit log** — Start tracking Level 2 and 3 sharing (immediate)

-----

**Working Copy:** jjuniper-dev/config-json (GitHub — personal account)
**Canonical Repository (Required):** GCcode (SSC-hosted GitLab CE) under DTB group account
**Classification:** Unclassified / For Internal Use

*This document is an EA/TPO working reference. It represents EA team working standards, not citeable GC policy.*
