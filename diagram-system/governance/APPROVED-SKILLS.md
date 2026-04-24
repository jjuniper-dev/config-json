# Approved Skills & Tools
## Data Governance Approval Status for Spec/ Directory

**Maintained by:** EA Team  
**Last Updated:** [INSERT DATE]  
**Review Frequency:** Quarterly

---

## Status Legend

| Symbol | Meaning |
|---|---|
| ✅ | Approved for use (follow conditions) |
| ⚠️ | Conditional approval (restrictions apply) |
| ❌ | Not approved (do not use) |
| 🔄 | Pending assessment |

---

## Claude AI & LLM Services

### Claude (Anthropic) — ✅ APPROVED

**Overview:**
- Service: Anthropic Claude API / claude.ai
- Vendor: Anthropic (US-based, Canada operations)
- Data Residency: US/Canada (Anthropic handles residency compliance)
- Retention: No training on user queries (can be verified)

**Approved Classification Levels:**
- Level 1 (Unclassified): ✅ Yes, no flag needed
- Level 2 (Internal Use): ✅ Yes, with [Level 2 flag]
- Level 3 (Protected B): ❌ No, requires CDO escalation

**Conditions:**
- Level 2 content MUST include [Level 2: Internal Use Only] flag
- DO NOT share specific workload names, stakeholder names, or timelines with Level 2 content
- NO Protected B content unless explicitly approved by CDO in writing
- Session-only use (do not retain outputs that contain HC/PHAC details)

**Data Handling Agreement:** Signed and on file  
**Last Security Review:** [INSERT DATE]

**Example Approved Use:**
```
[Level 2: Internal Use Only]
Please summarize the tradeoffs in this governance approach.
Generalize all responses and omit specific HC/PHAC organizational references.
```

**Approval Date:** [INSERT DATE]  
**Next Review:** [INSERT DATE + 3 months]

---

### ChatGPT (OpenAI) — ⚠️ CONDITIONAL

**Overview:**
- Service: OpenAI ChatGPT (GPT-4, ChatGPT Plus)
- Vendor: OpenAI (US-based)
- Data Residency: US (no Canada residency option)
- Retention: User queries may be used for model training (OpenAI policy unclear)

**Approved Classification Levels:**
- Level 1 (Unclassified): ✅ Yes
- Level 2 (Internal Use): ⚠️ Only with explicit CDO approval
- Level 3 (Protected B): ❌ No

**Conditions:**
- Default policy: DO NOT use for Level 2 or Level 3 content
- Only Level 1 (completely unclassified, generic) content approved
- If Level 2 use is necessary, must escalate to CDO for approval
- Cannot use personal ChatGPT accounts; only enterprise accounts with data processing agreements

**Data Handling Agreement:** Unsigned — requires negotiation  
**Last Security Review:** [INSERT DATE; flagged as unclear data retention]

**Why Conditional?**
- OpenAI's data retention policy is unclear (may use queries for training)
- No signed Data Processing Agreement with HC
- US-based with no explicit Canada residency guarantees
- Use is conditional on business need and CDO approval

**If You Need to Use ChatGPT for Level 2:**
1. Escalate to CDO with justification
2. Redact all Protected B details (workload names, stakeholder names, timelines)
3. Include confidentiality notice
4. Request approval in writing
5. Log in audit trail

**Approval Date:** [INSERT DATE; conditional status]  
**Next Review:** [INSERT DATE + quarterly; pending DPA negotiation]

---

### Google Gemini — ❌ NOT APPROVED

**Overview:**
- Service: Google Gemini (Bard)
- Vendor: Google (US-based)
- Data Residency: Unclear (US, potentially global)
- Retention: User prompts used for model improvement (confirmed)

**Approved Classification Levels:**
- Level 1 (Unclassified): ❌ Not recommended
- Level 2 (Internal Use): ❌ No
- Level 3 (Protected B): ❌ No

**Reason for Non-Approval:**
- Google Gemini explicitly uses user prompts for model training
- No signed Data Processing Agreement
- Data residency outside Canada
- No HC precedent for using Google consumer AI services

**Alternative:** Use Claude or approved HC enterprise tools instead.

**Status:** Not approved (no pending reassessment)

---

## GitHub & Version Control

### GitHub (Private Repo — HC Organization) — ✅ APPROVED

**Overview:**
- Service: GitHub.com (private repository under HC/PHAC organization)
- Vendor: GitHub/Microsoft
- Data Residency: US (Microsoft cloud, but private repo)
- Retention: Indefinite (version control)

**Approved Classification Levels:**
- Level 1 (Unclassified): ✅ Yes
- Level 2 (Internal Use): ✅ Yes
- Level 3 (Protected B): ⚠️ Only if redacted, with clear access controls

**Conditions:**
- Must be private repo within HC/PHAC organization (not public)
- Access limited to authorized HC/PHAC team members
- Protected B content must be redacted or clearly flagged [CONFIDENTIAL]
- Commit messages must not reveal workload names or stakeholder details
- Code review process in place (at least one other reviewer)

**Data Handling Agreement:** Yes (GitHub Enterprise terms)  
**Last Security Review:** [INSERT DATE]

**Example Approved Content:**
```
✅ Design system configurations (Level 1)
✅ Template structures and generic governance code (Level 1)
✅ Internal architecture ADRs with redacted workload names (Level 2)
✅ Architecture diagrams and specifications (Level 2)

❌ Do not commit: Full stakeholder names, specific timelines, 
   Protected B workload details without redaction
```

**Approval Date:** [INSERT DATE]  
**Next Review:** [INSERT DATE + 3 months]

---

### GitHub Copilot — ⚠️ CONDITIONAL

**Overview:**
- Service: GitHub Copilot (AI code completion)
- Vendor: GitHub/Microsoft
- Data Usage: Code snippets used for model training (confirmed)
- Retention: Training data

**Approved Classification Levels:**
- Level 1 (Unclassified): ✅ Yes
- Level 2 (Internal Use): ❌ No
- Level 3 (Protected B): ❌ No

**Conditions:**
- Level 1 content ONLY (completely unclassified, generic code)
- DO NOT use for code containing Protected B details, workload names, or HC-specific logic
- Disable telemetry/training data sharing if possible
- Code generated by Copilot must be reviewed for Protected B leakage

**Why Conditional?**
- Copilot explicitly trains on code provided to it
- Any Protected B details in prompts or generated code will enter Microsoft/OpenAI training pipeline
- Level 2 or 3 content will be exposed to external training

**If You Need Code Generation for Level 2/3:**
- Use Claude instead (no training on user queries)
- Or use generic code generators without ML training

**Approval Date:** [INSERT DATE]  
**Next Review:** [INSERT DATE + quarterly]

---

## Microsoft Services

### Microsoft 365 (Teams, SharePoint, Word, Excel) — ✅ APPROVED

**Overview:**
- Service: Microsoft 365 (enterprise)
- Vendor: Microsoft (US-based, Canada operations)
- Data Residency: Canada (by default for HC)
- Retention: Indefinite (managed by HC)

**Approved Classification Levels:**
- Level 1 (Unclassified): ✅ Yes
- Level 2 (Internal Use): ✅ Yes
- Level 3 (Protected B): ⚠️ SharePoint only (not Teams public channels)

**Conditions:**
- SharePoint: ✅ OK for Level 2 and Level 3 (with access controls)
- Teams: ✅ OK for Level 2 (not Level 3 in public channels)
- Teams DMs: ✅ OK for Level 2 and Level 3 (encrypted)
- Word/Excel: ✅ OK for Level 2 and Level 3 (with HC managed classification)

**Data Handling Agreement:** Yes (Enterprise Services Agreement)  
**Last Security Review:** [INSERT DATE]

**Best Practices:**
- Store Level 3 content in SharePoint with restricted access
- Do not discuss Level 3 details in public Teams channels
- Use Teams DMs for Level 2 or 3 conversations
- Classify documents with HC sensitivity labels

**Approval Date:** [INSERT DATE]  
**Next Review:** [INSERT DATE + annual]

---

### Azure Cloud Services — ✅ APPROVED

**Overview:**
- Service: Microsoft Azure (HC/PHAC subscriptions)
- Vendor: Microsoft (US-based, Canada operations)
- Data Residency: Canada (by HC policy)
- Retention: Indefinite (managed by HC)

**Approved Classification Levels:**
- Level 1 (Unclassified): ✅ Yes
- Level 2 (Internal Use): ✅ Yes
- Level 3 (Protected B): ✅ Yes (with governance controls)

**Conditions:**
- Only HC/PHAC Azure subscriptions (not personal or third-party)
- RBAC enforced (access limited to authorized users)
- Encryption enabled (data at rest and in transit)
- Logging and auditing enabled

**Data Handling Agreement:** Yes (Azure Enterprise Agreement)  
**Last Security Review:** [INSERT DATE]

**Approval Date:** [INSERT DATE]  
**Next Review:** [INSERT DATE + annual]

---

## External Services & Prohibited Tools

### Dropbox — ❌ NOT APPROVED

**Overview:**
- Service: Dropbox (cloud storage)
- Vendor: Dropbox (US-based)
- Data Residency: US
- Retention: Dropbox retains deleted data for certain period

**Approved Classification Levels:**
- All levels: ❌ Not approved for HC/PHAC content

**Reason:**
- HC has Microsoft 365 / SharePoint for cloud storage (approved alternative)
- Dropbox US residency does not meet HC data residency requirements
- Dropbox personal accounts create security and access control risks

**Alternative:** Use SharePoint (Microsoft 365) instead.

---

### Google Drive / Google Workspace — ❌ NOT APPROVED

**Overview:**
- Service: Google Drive (cloud storage)
- Vendor: Google (US-based)
- Data Residency: US
- Retention: Unclear (Google may use data for analytics)

**Approved Classification Levels:**
- All levels: ❌ Not approved for HC/PHAC content

**Reason:**
- HC has Microsoft 365 / SharePoint for cloud storage
- Google Drive US residency does not meet HC data residency policy
- Personal Google accounts create security risks

**Alternative:** Use SharePoint (Microsoft 365) instead.

---

### Slack — ⚠️ CONDITIONAL

**Overview:**
- Service: Slack (team messaging)
- Vendor: Slack (US-based, acquired by Salesforce)
- Data Residency: US (Slack has not committed to Canada residency)
- Retention: Slack retains message history indefinitely

**Approved Classification Levels:**
- Level 1 (Unclassified): ✅ Yes
- Level 2 (Internal Use): ⚠️ Only for ephemeral discussions, not archival
- Level 3 (Protected B): ❌ No

**Conditions:**
- Level 1: Use without restriction
- Level 2: Use only for temporary discussions; do not post sensitive details that need archival
- Level 3: Do not use (escalate to Teams DM instead)
- Do not enable Slack apps that sync to external services (e.g., GitHub integration without review)

**Data Handling Agreement:** Not fully signed; pending review  
**Last Security Review:** [INSERT DATE]

**Why Conditional?**
- US-based data residency (unclear if Slack has Canada option)
- No explicit Data Processing Agreement for Protected B
- Use is tolerated for Level 1 and limited Level 2 (not archival)
- Preferred tool for Teams DMs instead (Microsoft 365 approved)

**Status:** Conditional (reassess as business alternatives emerge)  
**Next Review:** [INSERT DATE + quarterly]

---

### Reddit, Stack Overflow, Public Forums — ❌ NOT APPROVED

**Overview:**
- Service: Public forums (Reddit, Stack Overflow, etc.)
- Data Residency: Global (public internet)
- Retention: Indefinite (public content)

**Approved Classification Levels:**
- All levels: ❌ Not approved for any HC/PHAC content

**Reason:**
- Public forums are world-accessible; content cannot be unshared
- No data control or deletion option once posted
- Any HC/PHAC information is exposed permanently

**Alternative:** Use approved internal tools (SharePoint, Teams) for discussions.

---

## Skill Provider Assessment Status

### Custom Skills (Claude Code, GitHub Actions, Azure Pipelines)

| Skill Name | Purpose | Classification Approval | Status | Approval Date | Next Review |
|---|---|---|---|---|---|
| **simplify** | Code review & optimization | Level 2 (with flag) | ✅ Approved | [DATE] | [DATE + 3m] |
| **[Custom CI/CD Script]** | Automation in spec/ | Level 1 only | 🔄 Pending | [DATE] | [DATE + 2w] |
| **[Linting Tool]** | Code quality checks | Level 1 only | ✅ Approved | [DATE] | [DATE + 3m] |

---

## How to Request a New Skill / Tool

**To get a new tool approved, submit:**

1. **Tool/Skill Name & Purpose**
2. **Vendor & Data Residency**
3. **Maximum Classification Level Needed** (Level 1, 2, or 3)
4. **Data Handling Questions:**
   - Where is data stored?
   - How long is it retained?
   - Is it used for training or analytics?
   - Is data shared with third parties?
5. **Risk Assessment:**
   - What could go wrong?
   - How would we detect it?
   - What's the mitigation plan?

**Submit to:** EA Lead

**Timeline:**
- Routine assessment: 2 weeks
- Escalation to CDO: 3–4 weeks
- Legal review (if needed): 4+ weeks

---

## Annual Compliance Review Checklist

**Every 12 months, EA Team shall:**

- [ ] Review this list and update approval status
- [ ] Re-verify Data Handling Agreements with vendors
- [ ] Assess any security incidents or policy changes (vendor-side)
- [ ] Audit usage logs (did team use tools within approved scope?)
- [ ] Update next review dates
- [ ] Report to CDO on compliance status

---

**Document Control:**

- **Version:** 1.0
- **Last Updated:** [INSERT DATE]
- **Next Review:** [INSERT DATE + 12 months]
- **Owner:** EA Team
- **Approver:** CDO

---

*This list is maintained as a living document. Check back quarterly for updates.*

*Classification: Unclassified / For Internal Use*
