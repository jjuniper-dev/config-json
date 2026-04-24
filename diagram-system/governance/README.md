# Data Governance Framework
## HC/PHAC EA Specification Repository

This directory contains governance policies and guidance for handling information in the spec/ directory when sharing with external services, LLMs, skill providers, and contractors.

---

## Quick Start

**If you're in a hurry:**
1. Read **[DATA-HANDLING-CHECKLIST.md](./DATA-HANDLING-CHECKLIST.md)** (5-minute quick reference)
2. Classify your content (Level 1, 2, or 3)
3. Check the approval status in **[APPROVED-SKILLS.md](./APPROVED-SKILLS.md)**
4. Proceed or escalate

**If you need the full policy:**
- Read **[DATA-GOVERNANCE-POLICY.md](./DATA-GOVERNANCE-POLICY.md)** (comprehensive framework)

---

## The Core Rules

### Classify First

```
Does it contain workload names (PMRA, FluWatch, LabScan, HAIL, PATH)?
  YES → Level 3 (Protected B) — Escalate to EA Lead
  NO → Continue

Does it contain stakeholder names or timelines?
  YES → Level 3 (Protected B) — Escalate to EA Lead
  NO → Continue

Is it internal-use only (not for publication)?
  YES → Level 2 (Internal Use) — Can share with Claude (with flag)
  NO → Level 1 (Public/Unclassified) — Can share freely
```

### Then Apply Rules

| Level | What It Is | Can Share With | Restrictions |
|---|---|---|---|
| **1** | Public/Unclassified (design system colors, WAF principles) | Anyone (Claude, ChatGPT, external tools) | None |
| **2** | Internal Use Only (ADRs, governance, strategy) | Claude (with flag), HC internal tools | NO external services, contractors, or ChatGPT |
| **3** | Protected B (workload names, stakeholder names, security gaps) | **ONLY after CDO approval** | Escalate immediately |

---

## Key Policies

### 1. Data Classification Framework

**Level 1 (Public/Unclassified):**
- Design system specifications (colors #2F6F73, fonts, spacing)
- General architectural concepts and WAF principles
- Generic governance terminology
- ✅ Safe to share with anyone

**Level 2 (Internal Use):**
- Architectural Decision Records (ADRs)
- Internal governance approaches
- Strategic planning documents
- ⚠️ Can share with Claude (with [Level 2: Internal Use Only] flag)
- ❌ Cannot share with external services or contractors

**Level 3 (Protected B/Confidential):**
- Workload names: PMRA, FluWatch, LabScan, IRIDA, CANChat, HAIL, PATH
- Stakeholder names: Kirk, Jason, Chad, Ali, Sam, Mohamed, Sanaa, Monica
- Specific timelines and delivery dates
- Security gaps and governance weaknesses
- Data residency and compliance details
- 🛑 **NEVER share without explicit CDO approval**

### 2. Approved Services

| Service | Approval | Level 1 | Level 2 | Level 3 |
|---|---|---|---|---|
| **Claude AI** | ✅ Full | ✅ | ✅ (with flag) | ❌ |
| **ChatGPT** | ⚠️ Conditional | ✅ | ❌ (needs CDO approval) | ❌ |
| **GitHub (private)** | ✅ Full | ✅ | ✅ | ⚠️ (redacted) |
| **GitHub Copilot** | ⚠️ Conditional | ✅ | ❌ | ❌ |
| **Microsoft 365** | ✅ Full | ✅ | ✅ | ✅ (SharePoint) |
| **Azure** | ✅ Full | ✅ | ✅ | ✅ |
| **Dropbox** | ❌ Not Approved | ❌ | ❌ | ❌ |
| **Google Drive** | ❌ Not Approved | ❌ | ❌ | ❌ |
| **Public Forums** | ❌ Prohibited | ❌ | ❌ | ❌ |

### 3. How to Share Level 2 Content with Claude

Always include this flag:

```
[Level 2: Internal Use Only]

This information is intended for HC/PHAC internal planning only.
Do NOT store, retain, or use in external training or analytics.

Your response should:
✓ Address the question directly
✓ Omit specific HC/PHAC organizational names
✓ Generalize workload and stakeholder references
✗ Do NOT reference specific programs, timelines, or confidential details

Approved use: Analysis and synthesis within this session only.
```

### 4. When to Escalate (Red Flags)

🛑 **Stop and escalate to EA Lead immediately if:**
- You want to share content with an unauthorized external service
- Content contains workload or stakeholder names and you're unsure
- A third-party requests spec/ content without signing an NDA
- You discover Protected B information was shared without approval
- An external tool accessed the spec/ directory without approval
- You're unsure about classification level

**Escalation Contact:**
- **First:** EA Lead (Chad or Ali)
- **If urgent/breach:** Security Lead (Kirk)
- **If violation:** CDO or Director

---

## Sensitive Data Masking Examples

### ❌ INCORRECT — Full Workload Names

```
"PMRA uses AI for pharmaceutical document review."
"FluWatch applies anomaly detection to syndromic surveillance data."
"LabScan: HAIL Platform detects outbreak conditions."
```

### ✅ CORRECT — Generalized

```
"A regulatory intake program applies AI to document review."
"A surveillance program applies anomaly detection to health signal data."
"An outbreak detection platform applies predictive models."
```

---

## Document Inventory

| Document | Purpose | Audience | Read Time |
|---|---|---|---|
| **README.md** (this file) | Overview and quick reference | Everyone | 5 min |
| **DATA-HANDLING-CHECKLIST.md** | Step-by-step guidance for team members | EA team, contractors | 10 min |
| **DATA-GOVERNANCE-POLICY.md** | Complete policy with all details | EA leadership, compliance | 30 min |
| **APPROVED-SKILLS.md** | Tool and service approval status | Team members before using tools | 15 min |

---

## Common Questions

**Q: Can I share this ADR with Claude for analysis?**

A: Depends on content:
- If ADR contains workload names or timelines → Level 3 → Escalate to EA Lead
- If ADR is generic governance approach → Level 2 → OK with [Level 2 flag]
- If ADR contains no HC-specific details → Level 1 → OK without flag

**Q: Can I use GitHub Copilot to write code for spec/ tools?**

A: Only if code is Level 1 (unclassified, no Protected B). Copilot trains on code snippets, so:
- ✅ Generic Python or JSON code (Level 1)
- ❌ Code containing workload names or HC-specific logic (Level 2+)

**Q: Can I share the risk register with an external consultant?**

A: No, unless:
1. Consultant has signed NDA
2. Content is redacted (remove workload names, specific timelines)
3. EA Lead approves in writing
4. Sharing is logged in audit trail

**Q: Is my personal ChatGPT account OK for this?**

A: No. Use Claude or approved HC services only. OpenAI's data retention policy is unclear.

**Q: What if I accidentally shared Protected B information?**

A: Escalate to Security Lead (Kirk) immediately. Do not delay.

---

## Getting Help

| Question | Contact |
|---|---|
| Content classification unclear | EA Lead |
| Want to use a new tool/service | Submit tool assessment form to EA Lead |
| Data governance question | EA Lead or CDO |
| Suspected breach or violation | Security Lead (Kirk) immediately |

---

## Compliance & Audit

**You will be audited on:**
- Whether content was classified correctly
- Whether you followed approval rules for the classification level
- Whether you included flags when sharing Level 2 with external services
- Whether you logged in audit trail (for Level 2 & 3)

**Non-compliance can result in:**
- Coaching and retraining
- Removal from project access
- Disciplinary action (repeated violations)
- Documentation in personnel file

**Be compliant. Be safe. Ask first if unsure.**

---

## Version History

| Version | Date | Change |
|---|---|---|
| 1.0 | [INSERT DATE] | Initial governance framework |

---

*Last Updated: [INSERT DATE]*

*Classification: Unclassified / For Internal Use*
