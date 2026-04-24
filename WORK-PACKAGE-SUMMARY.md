# EA Specification Repository — Complete Work Package
## HC/PHAC Data Governance & Platform Convergence Analysis Infrastructure

**Date:** April 24, 2026  
**Classification:** Unclassified / For Internal Use  
**Repository:** jjuniper-dev/config-json  
**Main Branch Commit:** 4923916 (Merge PR #3)

---

## Executive Summary

This work package delivers a **complete governance and analysis infrastructure** for Health Canada and PHAC enterprise architecture work, specifically:

1. **Data Governance Framework** — Policy and procedures for safely handling Protected B information when sharing with external services, LLMs (Claude, ChatGPT), and skill providers

2. **EA Platform Convergence Agent** — Structured methodology and charter for Architecture Review Board (ARB) assessment of whether PATH (HC-led governance control plane) and HAIL (PHAC-led operational runtime) should merge into a single governed platform or remain co-equal with defined integration points

**Business Value:**
- Enables safe use of external AI services (Claude, GitHub Copilot, etc.) for sensitive EA work without exposing Protected B information
- Provides decision-ready framework for critical platform convergence decision (3 scenarios with tradeoff analysis)
- Establishes audit trail and compliance procedures (Treasury Board, PIPEDA, Directive on Automated Decision-Making)
- Empowers EA team to conduct rigorous stakeholder validation and deliver ARB-ready briefings

---

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
- **Level 1 (Public):** Design system, WAF principles → Share with anyone
- **Level 2 (Internal Use):** ADRs, governance → Share with Claude (with flag), HC tools only
- **Level 3 (Protected B):** Workload names, stakeholder names, timelines → **NEVER share without CDO approval**

**Service Approval Status:**
- ✅ Claude AI (Level 1 & 2 with flag)
- ✅ GitHub private (Level 1-3 redacted)
- ✅ Microsoft 365 (Level 1-3)
- ✅ Azure (Level 1-3)
- ⚠️ ChatGPT (Level 1 only; Level 2 needs CDO approval)
- ⚠️ GitHub Copilot (Level 1 only)
- ⚠️ Slack (Level 1 only)
- ❌ Dropbox, Google Drive, Public Forums (all prohibited)

---

### 2. EA Platform Convergence Agent
**Location:** `diagram-system/spec/ea-platform-convergence/`

**Purpose:** Complete charter, configuration, and deliverable templates for ARB assessment of PATH/HAIL convergence decision.

**Core Files (4 documents + 5 templates, 2,106 lines):**

**Charter & Configuration:**
- **EA-Agent-Instructions-v1.md** (225 lines) — Master charter with 7 sections: role, context, framework, deliverables, interaction, standards, success criteria
- **config.json** (163 lines) — Agent configuration (scenarios, stakeholder map, assessment framework, success metrics)
- **USAGE.txt** (164 lines) — Quick reference (deliverables, timeline, escalation triggers)
- **README.md** (261 lines) — Agent overview, directory structure, 5-phase workflow

**Deliverable Templates (5 P-Prioritized Documents):**
1. **001-convergence-framing-template.md** (256 lines) — P1: ARB decision framing with 3 scenarios A/B/C and tradeoff analysis
2. **002-waf-assessment-template.md** (179 lines) — P2: WAF pillar assessment (Operational Excellence & Reliability)
3. **003-risk-register-template.md** (300 lines) — P3: Risk register with 5 convergence risks and scenario impact
4. **004-adr-template.md** (312 lines) — P4: ADR-002 Protected B hosting decision (Azure.us vs. Commercial Azure)
5. **005-shadow-ai-narrative-template.md** (246 lines) — P5: Shadow AI risk business narrative for executives

**Supporting Subdirectories:**
- `templates/` — Working templates (above 5 files)
- `deliverables/` — Empty; ready for completed, signed-off versions
- `intelligence/` — Empty; ready for reference documents (HAIL/PATH current state, etc.)

---

## How to Use This Package

### Phase 1: Onboarding (Day 1–2)
1. Read `EA-Agent-Instructions-v1.md` (charter, scope, success criteria)
2. Review `config.json` (scenarios, stakeholder map)
3. Skim `USAGE.txt` (quick overview)
4. Review `diagram-system/governance/README.md` (data governance rules)

### Phase 2: Stakeholder Validation (Week 1)
- Schedule meetings with Kirk (Security), Jason (Cloud Ops), Sam/Mohamed (PMRA), Chad/Ali (EA Leadership)
- Validate assumptions on ATO path, FinOps, use cases, strategy alignment
- Document feedback in feedback log

### Phase 3: Draft Deliverables (Week 2)
1. Copy templates to deliverables/ and populate with analysis
2. Start with P1 (Convergence Framing) — fill in scenarios A/B/C
3. Use P2 (WAF Assessment) as evidence
4. Draft P3 (Risk Register) in parallel
5. Reference P4 (ADR-002) and P5 (Shadow AI Narrative)

### Phase 4: Feedback & Iteration (Week 3)
- Share drafts with stakeholders
- Incorporate feedback
- Quality gate check: Does ARB have enough to decide?

### Phase 5: Final Package (Week 4)
- Obtain stakeholder sign-off
- Package all deliverables for ARB
- Ready for ARB meeting (4–6 weeks out)

---

## Data Governance Integration

**Before sharing any spec/ content with Claude, ChatGPT, GitHub Copilot, or external services:**

1. **Classify:** Level 1, 2, or 3? (Use decision tree)
2. **Check approval:** Verify tool is approved for that classification
3. **Add flag (if Level 2):** Include `[Level 2: Internal Use Only]` when sharing with Claude
4. **Redact (if Level 3):** Remove workload names, stakeholder names, specific timelines
5. **Log (if Level 2 or 3):** Record what was shared, when, why, approvers
6. **Review:** Check response for Protected B leakage

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

---

## Success Criteria

✅ **ARB has three explicit convergence options** with tradeoff analysis (P1)

✅ **EA recommended position is stated and defensible** (e.g., "Scenario A reduces shadow AI risk fastest and delivers single ATO path by Q3 2026")

✅ **Stakeholders reviewed and signed off:**
- Security (Kirk): ATO path and data residency confirmed
- Cloud Ops (Jason): Foundry availability and FinOps feasibility confirmed
- PMRA (Sam, Mohamed): Use case priority and governance confirmed
- EA Leadership (Chad, Ali): DTB strategy alignment confirmed

✅ **Risk register is current** (flags three P1 items mitigated by convergence decision)

✅ **ADR-002 completed** (linked from P1 document)

✅ **All deliverables are clean, single-file, ARB-ready** (minimal adaptation needed)

---

## Escalation Triggers

**Stop and escalate to EA Lead immediately if:**
- Timeline slips past 2-week P1 draft deadline
- Stakeholder feedback contradicts core assumptions
- Risk register identifies new P1 item
- ADR-002 decision blocked by unresolved constraint
- Protected B information accidentally exposed
- Any convergence scenario becomes infeasible

**Escalation Chain:**
1. EA Lead (Chad or Ali)
2. Security Lead (Kirk) if data breach suspected
3. CDO if policy violation

---

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

---

## Package Statistics

**Total Deliverables:** 13 files  
**Total Lines:** ~3,870 lines of policy, procedures, and templates  
**Git Status:** Merged to main (2026-04-24, Commit 4923916)  
**Ready for Use:** ✅ Yes

---

## Next Steps

1. **Confirm charter scope** — Does role, constraints, and success criteria align?
2. **Schedule stakeholder meetings** — Kirk, Jason, Sam/Mohamed, Chad/Ali (Week 1)
3. **Begin P1 draft** — Copy template, fill in scenarios A/B/C (Week 2)
4. **Validate governance policy** — Confirm data handling rules with team (immediate)
5. **Establish audit log** — Start tracking Level 2 & 3 sharing (immediate)

---

**Repository:** jjuniper-dev/config-json  
**Classification:** Unclassified / For Internal Use
