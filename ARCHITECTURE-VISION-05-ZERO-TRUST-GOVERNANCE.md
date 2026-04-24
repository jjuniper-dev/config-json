# Architectural Vision: Zero Trust Governance Framework
## Data & Service Security for EA Work

**Status:** Working Document / Framework Design  
**Classification:** Unclassified / For Internal Use  
**Date:** April 24, 2026

---

## 1. Zero Trust Philosophy

**Core Principle:** Never assume trust. Verify every interaction. Design for breach.

**Current Preference:**
- Always classify data (Level 1-3) before any action
- Always authenticate external service requests with explicit approval (not implicit)
- Always redact Protected B before external sharing
- Always log Level 2+ interactions for audit
- Assume breach: Design so Protected B exposure is contained and detectable
- Verify every tool/service before use (check approval matrix)
- Assume Claude context is not private — design as if conversation could be exposed

**Why It Matters:**
- Shifts security from "prevent all breaches" (impossible) to "detect and contain quickly"
- Makes data handling visible (not implicit)
- Enables compliance audits with clear evidence (audit trail)
- Reduces insider threat surface
- Meets Treasury Board, PIPEDA, and Directive on Automated Decision-Making requirements

**Open Questions:**
- How do we balance zero trust rigor with development velocity? (Is every single interaction too much logging?)
- What's acceptable latency for approval workflows? (Should data governance slow decision-making?)
- How granular should audit logging be? (Every query vs. summary? Every tool invocation vs. significant actions?)
- How do we prevent approval workflows from becoming theater (rubber-stamping)?

**Alternative Approaches:**
- Trust-first (faster, riskier, fails spectacularly)
- Implicit approval for known services (efficient, compliance risk)
- Manual approval for everything (slow, exhausting, not scalable)
- Separate security review phase (cleaner, but misses issues in context)

---

## 2. Classification Framework (Operationalized)

### Level 1: Public / Unclassified

**Definition:** Content suitable for sharing with anyone (inside or outside HC/PHAC) without control or audit

**Characteristics:**
- No organizational references (can remove HC/PHAC and still meaningful)
- No timeline information (when things happen)
- No stakeholder names or roles
- No financial impact data
- No constraints specific to our architecture

**Examples (GO/NOT GO):**
- ✅ "Well-Architected Framework assessment" (generic methodology)
- ✅ "Risk register template with 5 risk categories" (structure without content)
- ✅ "Data governance classification policy" (process, not protected data)
- ❌ "Scenario A timeline: Q3 2026 ATO" (timeline = Level 2)
- ❌ "Kirk (Security Lead) approved ADR-002" (names = Level 2/3)

**Sharing:** Share with anyone, anywhere. No logging required.

**Service Approval:** Level 1 content approved for all services (Claude, ChatGPT, GitHub Copilot, Slack, etc.)

---

### Level 2: Internal Use Only

**Definition:** Content for HC/PHAC internal use; can be shared with approved internal services and external AI services (with caution)

**Characteristics:**
- May include organizational context (HC/PHAC) without sensitivity
- May include timelines if generic ("Q3 2026" not specific date)
- May include generic roles ("Security Lead", "Cloud Operations") not names
- May include strategic decisions not yet public
- May include process/governance details
- May include financial ranges (not specific costs)

**Examples (GO/NOT GO):**
- ✅ "ADR-002: Protected B hosting decision (Azure.us vs. Commercial Azure)" (decision framework)
- ✅ "Three convergence scenarios with generic tradeoff analysis" (structure + reasoning)
- ✅ "Risk register with mitigation strategies" (operational content)
- ✅ "Meeting notes on stakeholder concerns about FinOps" (internal feedback)
- ❌ "Kirk specifically approved Scenario A (specific stakeholder + preference)" (Level 3)
- ❌ "PMRA/FluWatch workload names in scenario analysis" (Level 3)

**Sharing:** Share with approved services and people. Requires approval + flag when sharing with external AI services.

**Service Approval:**
- ✅ Claude (approved, with Level 2 flag in prompt)
- ✅ Microsoft 365 (approved)
- ✅ GitHub private (approved)
- ✅ Azure (approved)
- ⚠️ ChatGPT (requires CDO approval)
- ⚠️ GitHub Copilot (requires CDO approval)
- ⚠️ Slack (requires CDO approval for workplace sharing)
- ❌ Dropbox, Google Drive, Notion, public forums

**Logging:** Every Level 2 sharing event logged (what, when, to whom, approval status)

---

### Level 3: Protected B / Confidential

**Definition:** Sensitive information protected under Treasury Board (Protected B) classification

**Characteristics:**
- Specific workload names (PMRA, FluWatch, etc.)
- Specific stakeholder names + preferences (Kirk prefers A, Jason concerned about FinOps)
- Specific timelines (exact dates, milestones)
- Specific financial figures or FinOps models
- Specific data residency or compliance constraints
- Any combination of above (even innocuous combinations become sensitive in context)

**Examples (GO/NOT GO):**
- ❌ "Kirk (Security Lead) prefers Scenario A because of Protected B handling" (Level 3 — name + preference)
- ❌ "PMRA's FluWatch workload requires Azure.us; timeline Q3 2026" (Level 3 — workload + timeline)
- ❌ "FinOps model: $X per GB, Y per API call, Z per AI call" (Level 3 — specific financial data)
- ✅ (Nothing explicit; must be redacted)

**Sharing:** Never share externally without explicit CDO approval. Never share with unapproved external services.

**Service Approval:**
- ✅ Claude (only with redaction + CDO approval + mandatory flag)
- ✅ Microsoft 365 (approved for internal use)
- ✅ GitHub private (approved if repos private + redacted)
- ✅ Azure (approved, internal use)
- ❌ ChatGPT, GitHub Copilot, Slack, Dropbox, Google Drive, public forums

**Logging:** Every Level 3 interaction logged (what, when, to whom, approval, redaction status, CDO sign-off)

---

## 3. Approval Matrix (Service-by-Level)

| Service | Level 1 | Level 2 | Level 3 | Notes |
|---|---|---|---|---|
| **Claude** | ✅ Yes | ✅ Yes (flag) | ⚠️ CDO approval + redact | Approved for EA analysis |
| **ChatGPT** | ✅ Yes | ⚠️ CDO approval | ❌ No | External service; higher risk |
| **GitHub Copilot** | ✅ Yes | ⚠️ CDO approval | ❌ No | Code analysis; external |
| **Microsoft 365** | ✅ Yes | ✅ Yes | ✅ Yes (internal only) | Approved for internal use |
| **Azure** | ✅ Yes | ✅ Yes | ✅ Yes (internal) | Infrastructure; trusted |
| **GitHub private** | ✅ Yes | ✅ Yes (redact) | ⚠️ Redact + CDO approval | Depends on repo access |
| **Slack** | ✅ Yes | ⚠️ CDO approval | ❌ No | Workplace chat; audit trail weak |
| **Dropbox** | ❌ No | ❌ No | ❌ No | Uncontrolled sharing |
| **Google Drive** | ❌ No | ❌ No | ❌ No | Uncontrolled sharing |
| **Notion** | ❌ No | ❌ No | ❌ No | Uncontrolled sharing |
| **Public Forums** | ❌ No | ❌ No | ❌ No | Public exposure |

**Updating the Matrix:**
- Quarterly review with EA Lead + CDO
- New service request: Submit to CDO with risk assessment
- Service compromise: Immediately revoke approval, notify users

---

## 4. Operational Procedures

### Before Sharing Content Anywhere

**5-Step Verification:**

1. **Classify:** Run /classify-data. What level is this?
   - If uncertain: Treat as higher level (default to protective)
   - If Level 3: Stop. Escalate.

2. **Check Approval:** Run /approve-sharing with Level + target service
   - If Conditional: Get explicit approval first
   - If Escalate: Contact EA Lead or CDO

3. **Add Flag (if Level 2):** Include `[Level 2: Internal Use Only]` in any external sharing (Claude, ChatGPT, etc.)
   - Flag tells recipient to handle carefully
   - Flag acknowledges governance constraint

4. **Redact (if Level 3):** Run /redact-protected-b
   - Remove workload names
   - Remove stakeholder names + positions
   - Generalize timelines
   - Abstract capability descriptions
   - Verify redaction removes all Protected B markers

5. **Log (if Level 2 or 3):** Run /log-sharing with approval details
   - What was shared
   - When
   - To whom
   - Why
   - Approval status
   - Redaction status (if applied)

**Example: Safe Claude Query (Level 2)**
```
[Level 2: Internal Use Only]

I'm analyzing three platform convergence scenarios. 
Can you help me strengthen the tradeoff analysis between option A (longer timeline, unified governance) and option B (faster delivery, dual platforms)?

Omit any organizational references or specific stakeholder names.
```

**Example: Protected B Escalation (Level 3)**
```
I have convergence analysis that includes:
- Specific workload names (PMRA, FluWatch)
- Stakeholder names + their preferences
- Exact timelines (Q3 2026 ATO)

This is Level 3 (Protected B). I need CDO approval before sharing anywhere.
Action: Escalate to EA Lead + CDO for approval.
```

---

## 5. Audit Logging (Compliance)

### What Gets Logged?

**Mandatory Logging (All Level 2 interactions):**
- Content ID or brief description
- Timestamp (when shared)
- Target (to whom, which service)
- Approval status (approved, conditional, escalated)
- Redaction applied? (yes/no)
- Reason (why shared)
- User/role (who made the decision)

**Example Audit Entry:**
```
[2026-04-25 14:32]
Content: ADR-002 (Protected B hosting decision)
Classification: Level 2
Target: Claude (internal analysis)
Approval: Yes (approved for Level 2 + flag)
Redaction: None (no Protected B markers)
Flag Applied: [Level 2: Internal Use Only]
Reason: Architectural analysis and tradeoff review
User: EA Analyst (Claude session)
Redacted: Stakeholder names NOT included
```

**Mandatory Logging (All Level 3 interactions):**
- Same as above, plus:
- Pre-redaction content summary
- Post-redaction content verification
- CDO approval sign-off
- Time redaction verified

**Example Level 3 Audit Entry:**
```
[2026-04-26 10:15]
Content: Risk Register with stakeholder positions
Classification: Level 3
Target: Claude (for external presentation prep)
Approval: Yes (CDO approved 2026-04-26 09:45)
Redaction: Yes (stakeholder names, timelines, financial data removed)
Pre-Redaction Content: Specific stakeholder names + concerns, Q3 2026 timelines, $XXX cost estimates
Post-Redaction Content: Generic roles, generalized timelines, budget ranges
Redaction Verified: EA Lead sign-off
Flag Applied: [Level 2: Redacted] (after redaction, downgraded from Level 3)
Reason: External briefing preparation
User: EA Analyst (approved by CDO)
```

### Audit Log Access

**Who can read:**
- EA Lead (full access)
- CDO (full access)
- Audit team (read-only, summary format)
- Individual who made the sharing decision (own entries only)

**Who cannot read:**
- Team members (privacy protected)
- External services (audit log not shared)

**Audit Trail Retention:**
- 7 years (Treasury Board requirement)
- Quarterly review for compliance
- Annual report to CDO summarizing Level 2/3 sharing

---

## 6. Escalation Procedure

### When to Escalate (Stop and notify immediately)

**Scenario 1: Classification Uncertainty**
- Content fits multiple levels
- Risk assessment unclear
- Escalate to: EA Lead
- Timeline: Same day (don't proceed until clarified)

**Scenario 2: Service Not in Approval Matrix**
- New service (e.g., "Can we use OpenAI GPT-4?")
- Service status unknown
- Escalate to: EA Lead + CDO
- Timeline: <48 hours (evaluate service + update matrix)

**Scenario 3: Protected B Accidental Exposure**
- Level 3 content shared without approval/redaction
- Workload names, stakeholder names, or specific timelines leaked
- Escalate to: Security Lead (Kirk) + EA Lead + CDO immediately
- Timeline: <1 hour (containment)
- Action: Assess exposure scope, notify affected parties, update audit log, lessons learned

**Scenario 4: Approval Denied**
- Requested Level 2/3 sharing rejected by approval matrix
- Cannot proceed with current approach
- Escalate to: EA Lead (discuss alternative approaches)
- Timeline: Same day (explore redaction, alternative services, timeline delay)

**Scenario 5: Audit Discrepancy**
- Sharing happened without audit log entry
- /log-sharing failed or skipped
- Escalate to: EA Lead + CDO
- Timeline: <24 hours (retroactive audit, identify process gap)

---

## 7. Service Provider Assessment (How We Evaluate New Services)

**Checklist for CDO Review:**

1. **Data Handling:**
   - Does service store data at rest? Where?
   - Does service transmit data securely? (TLS 1.2+)
   - Does service retain data after use? How long?
   - Does service share data with third parties? Under what conditions?

2. **Access Control:**
   - Who can access customer data? (employees, third parties, government agencies)
   - Can users delete data? When?
   - Does service comply with PIPEDA? ATIP? Directive on Automated Decision-Making?

3. **Audit & Transparency:**
   - Does service log interactions? Can customers access logs?
   - Does service publish security assessments? (SOC 2, ISO 27001)
   - Does service notify on breaches? Timeline?
   - Can service be audited by our security team?

4. **Jurisdiction & Legal:**
   - Where is data stored physically? (Canada? US? International?)
   - What law governs? (Can Canadian government demand data under US law?)
   - Does service follow Treasury Board, PIPEDA, Directive requirements?

5. **Incident Response:**
   - Does service have public incident history?
   - How does service respond to breaches? (Notification? Remediation?)
   - Does service have breach insurance/liability?

**Risk Rating:**
- **Green (✅):** Meets all criteria; approved for all levels
- **Yellow (⚠️):** Meets most criteria; conditional approval (specific levels, specific use cases)
- **Red (❌):** Fails key criteria; not approved; escalate for exception

---

## 8. Internal Governance (Who Decides What)

### Decision Authority

| Decision Type | Authority | Consultation | Timeline |
|---|---|---|---|
| **Classification (Level 1/2/3)** | EA Analyst (with /classify-data tool) | If uncertain: EA Lead | <1 hour |
| **Service Approval (within matrix)** | EA Analyst | None (matrix is authority) | <5 min |
| **Conditional Approval** | EA Lead | CDO if escalated | <1 day |
| **Level 2/3 CDO Approval** | CDO | EA Lead (context) | <1 day |
| **New Service Assessment** | CDO | EA Lead + Security Lead | <1 week |
| **Policy Update** | CDO | EA Lead + Security Lead | <1 week (urgent), <1 month (routine) |
| **Breach Response** | Security Lead (Kirk) | CDO, EA Lead | Immediate (<1 hour) |

### Zero Trust for Internal Teams

Even team members must follow governance:
- No "internal exception" sharing without approval log
- Stakeholders can't see each other's positions without explicit sharing
- All Level 2+ sharing is logged, regardless of recipient
- Monthly governance review catches unapproved sharing

---

## 9. Tensions & Tradeoffs

| Principle | Tension | Current Preference | Alternative |
|---|---|---|---|
| **Rigor** | Every sharing logged = overhead | Classify, approve, log (all Level 2+) | Implicit trust (faster, risky) |
| **Latency** | Approval workflows slow decisions | Async approval (log + review later) | Synchronous (slower decisions) |
| **Automation** | Too much manual approval = theater | Use /classify-data + approval matrix (mostly automated) | Manual review each time (slow) |
| **Redaction** | Aggressive redaction = information loss | Remove sensitive markers; preserve evidence | Light redaction (more useful, riskier) |
| **Scope** | Log everything = data explosion | Log Level 2+ only; summary logs for Level 1 | Log everything (audit trail, noise) |
| **Scale** | Governance rules get complex | Quarterly review + update matrix | Static rules (stale, doesn't adapt) |
| **User Friction** | "Just share it internally" is tempting | But all internal sharing is logged | No logging (faster, no audit trail) |

---

## 10. Success Metrics (How We Know This Works)

✅ **Zero Protected B leaks** (or immediate detection and containment)

✅ **100% of Level 2+ sharing logged** (audit trail is complete)

✅ **Stakeholders feel safe with governance** (not overly restrictive, but trustworthy)

✅ **Approval workflows have <24-hour latency** (fast enough to not block work)

✅ **New team members understand rules within 1 week** (governance is learnable, not complex)

✅ **No governance violations discovered after 6 months** (rules are clear, followed, enforced)

❌ **Governance overhead > actual EA analysis time** (framework becomes theater)

---

## Navigation

This is Part 5 of 7. Read in this order:

1. Core Principles & Philosophy
2. Reference Architecture: EA Platform Convergence
3. Neo4j Knowledge Graph Schema
4. Modular Agent & Skill Components
5. **Zero Trust Governance Framework** ← You are here
6. Modularity & Reuse Patterns
7. Architectural Vision Synthesis

**Next Document:** Modularity & Reuse Patterns

*Classification: Unclassified / For Internal Use*
