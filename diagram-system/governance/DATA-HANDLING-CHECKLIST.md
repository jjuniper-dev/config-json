# Data Handling Checklist
## Quick Reference for Sharing Spec/ Directory Content

**Use this checklist BEFORE sharing any content from the spec/ directory with external services, LLMs, or skill providers.**

---

## Step 1: Classify the Content

**Ask yourself:**

- [ ] Does this content contain workload names (PMRA, FluWatch, LabScan, CANChat, HAIL, PATH, IRIDA)?
  - YES → **Level 3 (Protected B)** — Go to Step 4
  - NO → Continue

- [ ] Does this content contain stakeholder names (Kirk, Jason, Chad, Ali, Sam, Mohamed, Sanaa, Monica)?
  - YES → **Level 3 (Protected B)** — Go to Step 4
  - NO → Continue

- [ ] Does this content reveal security gaps, governance weaknesses, or specific timelines (Q1 2026, delivery dates)?
  - YES → **Level 3 (Protected B)** — Go to Step 4
  - NO → Continue

- [ ] Is this content intended for HC/PHAC internal use only (not for publication)?
  - YES → **Level 2 (Internal Use)** — Go to Step 2
  - NO → **Level 1 (Unclassified)** — Go to Step 3

---

## Step 2: Content is Level 2 (Internal Use Only)

**You can share this with:**
- ✅ Claude AI (with flag)
- ✅ HC internal tools (Azure, Microsoft 365, GitHub private)
- ❌ External LLMs (ChatGPT, Gemini, etc.)
- ❌ Third-party services (Slack, Notion, Google Drive)
- ❌ External contractors (without NDA)

**Before sharing with Claude:**

```
[Level 2: Internal Use Only]

This information is intended for HC/PHAC internal planning only.
Do NOT store, retain, or use this in external training or analytics.

Your response should:
✓ Address the question directly
✓ Omit specific HC/PHAC organizational names and stakeholder names
✓ Generalize references to programs (e.g., "regulatory intake" not "PMRA")
✗ Do NOT reference specific workloads, timelines, or confidential details

Approved use: Analysis and synthesis within this session only.
All outputs must omit Protected B details and generalize responses.
```

**Example Approved Queries:**

```
✅ "Summarize this governance approach for internal review (HC internal document)."

✅ "Review this ADR template for clarity and completeness (internal use)."

✅ "What are the key tradeoffs in this architecture decision? (internal document)"
```

**After receiving response from Claude:**
- [ ] Review output for any leaked Protected B details (workload names, stakeholder names, specific timelines)
- [ ] Redact any Protected B information that slipped through
- [ ] Proceed with internal use (share with HC team only)

---

## Step 3: Content is Level 1 (Unclassified)

**You can share this with:**
- ✅ Claude AI (no flag needed)
- ✅ Any HC/PHAC internal tool
- ✅ GitHub Copilot (for code generation)
- ✅ External LLMs (ChatGPT, Gemini, etc.)
- ✅ Third-party services (with HC approval)
- ✅ External contractors
- ✅ Published in case studies, presentations, etc.

**No special flags needed. Proceed with confidence.**

**Example Unclassified Content:**
- Design system colors and typography standards
- WAF pillar definitions and general architecture principles
- Generic governance concepts and best practices
- Public Azure Well-Architected Framework references

---

## Step 4: Content is Level 3 (Protected B / Confidential)

**🛑 STOP — Do not share without explicit approval**

**Contact:** EA Lead or CDO

**In your escalation request, provide:**

1. **What you want to do:** What analysis, synthesis, or processing is needed?
2. **Why it's necessary:** What business value justifies sharing Protected B information?
3. **What's the minimum viable content?** Can you achieve the goal with redacted/generalized information instead?
4. **What service/tool?** Claude, external LLM, external consultant?
5. **Risk assessment:** What could go wrong?

**If Approved by EA Lead/CDO:**

1. **Redact Protected B details:**
   - [ ] Remove workload names (replace with generalized descriptions)
   - [ ] Remove stakeholder names (replace with titles)
   - [ ] Redact specific timelines (replace with relative timelines: "6 weeks away")
   - [ ] Generalize program areas (replace "PMRA" with "regulatory intake")

2. **Add confidentiality flag:**

```
[PROTECTED B / CONFIDENTIAL]

This content contains Protected B information related to HC/PHAC 
enterprise platforms. Approved for Claude AI processing only.

DO NOT:
- Store or retain this information
- Use in model training or analytics
- Reference specific HC/PHAC workload names in responses
- Share with external services
- Provide to external consultants

Approved use: [Specific use case approved by EA Lead, e.g., 
"risk analysis for ARB briefing"]

Session-only processing: All outputs must omit Protected B details.
Generalize all responses and avoid specific program/workload references.
```

3. **Log the sharing:**
   - What was shared
   - Approval date and approver
   - Why it was necessary
   - How it was flagged/redacted

4. **Review the response:**
   - [ ] Check for any Protected B leakage (workload names, stakeholder names, specific timelines)
   - [ ] Redact any leaked details
   - [ ] Validate output for confidentiality compliance

5. **Document the outcome:**
   - What analysis was produced
   - Whether it achieved the objective
   - Any follow-up actions

---

## Step 5: Skill Provider Approval

**Before using any automation tool, script, or skill provider to process spec/ content:**

- [ ] Skill name and vendor identified
- [ ] Maximum classification level approved (Level 1, 2, or 3)?
  - [ ] Level 1 only — approved without restriction
  - [ ] Level 2 — approved with Data Handling Agreement
  - [ ] Level 3 — requires CDO approval (or prohibited)
- [ ] Is this skill on the **[APPROVED SKILL PROVIDERS](./APPROVED-SKILLS.md)** list?
  - [ ] YES — Proceed with confidence
  - [ ] NO — Submit [Skill Assessment](./SKILL-ASSESSMENT-FORM.md) before use

**If skill is not approved:**
- Don't use it until assessment is complete
- Submit assessment form to EA Lead
- EA Lead reviews and either approves or rejects

---

## Decision Tree: Quick Approval Guide

```
START
  |
  ├─ Does content contain workload names (PMRA, FluWatch, etc.)?
  │  └─ YES → LEVEL 3 (Protected B) → Escalate to EA Lead/CDO
  │  └─ NO → Continue
  |
  ├─ Does content contain stakeholder names or personal details?
  │  └─ YES → LEVEL 3 (Protected B) → Escalate to EA Lead/CDO
  │  └─ NO → Continue
  |
  ├─ Does content reveal security gaps or governance weaknesses?
  │  └─ YES → LEVEL 3 (Protected B) → Escalate to EA Lead/CDO
  │  └─ NO → Continue
  |
  ├─ Is content intended for HC/PHAC internal use only?
  │  └─ YES → LEVEL 2 (Internal Use) → Can share with Claude (with flag)
  │  └─ NO → LEVEL 1 (Unclassified) → Can share anywhere
  |
  └─ END: Proceed accordingly
```

---

## Common Scenarios

### Scenario 1: You want to ask Claude for a summary of an ADR

**ADR Content:** "ADR-002: Protected B Hosting Architecture for PATH (Azure.us vs. Commercial Azure)"

**Classification:**
- Contains architectural decision (Level 2)
- Contains security constraints (Level 2)
- May contain specific data residency requirements (Level 2)
- **→ Level 2 (Internal Use)**

**Approved Action:**
```
✅ Share with Claude + flag

[Level 2: Internal Use Only]
Please summarize the key tradeoffs and recommendation in this ADR.
Omit specific workload names and external vendor references in your response.
```

---

### Scenario 2: You want to ask an external consultant to review governance approach

**Content:** EA-Agent-Instructions-v1.md (governance charter)

**Classification:**
- Contains internal governance approach (Level 2)
- Contains stakeholder references (Level 3)
- **→ Level 2/3 Mix → Requires Approval + Redaction**

**Required Action:**
- [ ] Escalate to EA Lead: "Need external consultant to review governance approach"
- [ ] Redact stakeholder names (Kirk, Jason, Chad, Ali, etc.)
- [ ] Ensure consultant has signed NDA
- [ ] Share redacted version only
- [ ] Log in audit trail

---

### Scenario 3: You want to use GitHub Copilot to generate code for a new tool

**Scenario:** Generating Python script to parse config.json files

**Classification:**
- Config.json contains internal architecture configuration (Level 1–2)
- No workload names or stakeholder references (Level 1)
- **→ Level 1 (Unclassified)**

**Approved Action:**
```
✅ Use GitHub Copilot for code generation

# Generate Python function to parse this config schema
# (paste generic config structure, no HC-specific details)

⚠️ Note: Do NOT include workload names or stakeholder references
         in code comments or variable names
```

---

### Scenario 4: You want to pass a risk register entry to Claude for analysis

**Content:** Risk R-002 (Shadow AI Risk — workloads route to ungoverned platforms)

**Classification:**
- Contains workload names (PMRA, FluWatch, CANChat, Copilot) (Level 3)
- Contains specific current state information (Level 2–3)
- **→ Level 3 (Protected B) → Escalate**

**Required Action:**
- [ ] Escalate to EA Lead: "Need risk analysis for R-002 (shadow AI risk)"
- [ ] Provide approval (or rejection)
- [ ] If approved: Redact workload names before sharing
- [ ] Redacted version: "This risk describes the scenario where workloads route to ungoverned external platforms due to delays in internal platform maturity..."

---

## Red Flags — Stop and Escalate

🛑 **STOP immediately and escalate to EA Lead / Security if:**

- [ ] You're about to share content with an unauthorized external service
- [ ] Content contains workload or stakeholder names and you're unsure if it's safe
- [ ] A third-party asked for spec/ content without signing an NDA
- [ ] You discovered Protected B information was shared without approval
- [ ] An external tool accessed the spec/ directory without approval
- [ ] You're unsure about classification level (ask first, don't guess)
- [ ] Someone requested content for purposes outside EA governance

**Escalation Contact:**
- **First:** EA Lead (Chad or Ali)
- **If urgent or breach suspected:** Security Lead (Kirk)
- **If violation confirmed:** CDO or Director

---

## Examples of Correct vs. Incorrect Sharing

### ❌ INCORRECT — No Flag, No Redaction

```
User: "Analyze this for me"
[Shares full ADR-002, risk register, governance approach]
[No Level 2 flag, no redaction of workload/stakeholder names]

This is a violation. Protected information shared without flag.
Response: Escalate immediately.
```

### ✅ CORRECT — With Flag and Redaction

```
User: "Analyze this governance approach (internal document; Level 2 flag included)"
[Shares redacted governance document]
[Includes: [Level 2: Internal Use Only] flag]
[Redacted: workload names, stakeholder names, specific timelines]

This is compliant. Protected information flagged and redacted.
Response: Proceed.
```

### ❌ INCORRECT — Level 3 Shared Without Approval

```
User: "Here's the risk register entry on shadow AI risk"
[Shares full risk R-002 with workload names: PMRA, FluWatch, CANChat, etc.]
[No flag, no approval, no redaction]

This is a violation. Level 3 content shared without CDO approval.
Response: Escalate immediately; request content removal.
```

### ✅ CORRECT — Level 3 With Approval & Redaction

```
User: "EA Lead approved this analysis. Here's the redacted risk scenario."
[Shares redacted risk description]
[Includes: [Protected B / Confidential] flag]
[Redacted: specific workload names, replaced with "regulatory program", etc.]
[Approval logged in audit trail]

This is compliant. Protected information flagged, approved, and redacted.
Response: Proceed.
```

---

## Contact & Questions

**Data governance questions?**
- EA Lead: [INSERT NAME/EMAIL]

**Classification unclear?**
- Ask first, don't guess
- Contact: EA Lead

**Want to use a new service?**
- Submit skill assessment form
- Contact: EA Lead

**Suspected violation or breach?**
- Contact Security Lead immediately
- Email: [INSERT SECURITY EMAIL]
- Phone: [INSERT EMERGENCY NUMBER]

---

*Last Updated: [INSERT DATE]*

*Classification: Unclassified / For Internal Use*
