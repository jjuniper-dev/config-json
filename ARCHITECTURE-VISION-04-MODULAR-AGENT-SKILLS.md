# Architectural Vision: Modular Agent & Skill Components
## Building Composable Capabilities

**Status:** Working Document / Component Design  
**Classification:** Unclassified / For Internal Use  
**Date:** April 24, 2026

---

## 1. Philosophy: Skills as Building Blocks

**Current Preference:**
- Skills (Claude Code slash commands) are small, focused capabilities (5–10 lines core logic)
- Skills are stateless by default; stateful behavior belongs in MCP servers or persistent stores
- Skills combine via Claude's reasoning and user orchestration, not hardcoded chains
- Skills leverage Claude's multi-turn context to discover and chain capabilities
- Agent is the orchestrator that deploys skills, not a monolithic tool

**Why This Matters:**
- Keeps Claude in control of workflow decisions (not rigid automation)
- Easier to understand, test, modify, and share individual skills
- Reduces risk of skill dependencies breaking workflows
- Enables discovery: new skills can be invented mid-conversation
- Skills can be versioned and evolved independently

**Open Questions:**
- How do we discover available skills without hardcoding a registry?
- When should skill composition be explicit (user chooses chain) vs. implicit (Claude decides)?
- How do we prevent skill bloat (100+ skills becoming unmaintainable)?
- What's the skill discovery mechanism in large skill libraries?

**Alternative Approaches:**
- Monolithic multi-function skills (easier to deploy, harder to reuse, harder to modify)
- Full orchestration via MCP (more control, more complexity, less Claude agency)
- No skills, direct API calls (simpler for one-off use, not reusable, visible to user)
- Hardcoded skill chains (predictable, brittle, inflexible)

---

## 2. Core Skills for EA Platform Convergence

### Data Governance Skills

**`/classify-data`**
- Input: Content snippet (text, question, or deliverable draft)
- Output: Classification (Level 1/2/3) + confidence + reasoning
- Core Logic: Decision tree based on content patterns (workload names, stakeholder names, timelines, capability descriptions, financial data)
- Stateless: No persistence needed
- Example: `/classify-data "Scenario A timeline: Q3 2026 (ATO), Q1 2027 (first Protected B workload)"` → Level 2 (Internal Use)

**`/approve-sharing`**
- Input: Data classification + target service/person
- Output: Approved / Conditional / Escalate + reasoning
- Core Logic: Lookup approval matrix (from persistent governance rules), return status
- Stateless: Reads from governance state, doesn't write
- Example: `/approve-sharing Level 2 to ChatGPT` → Conditional (CDO approval required)

**`/redact-protected-b`**
- Input: Protected B content
- Output: Redacted version (workload/stakeholder names removed, timelines generalized, capability descriptions abstracted)
- Core Logic: Apply redaction rules from governance framework
- Stateless: No persistence
- Example: `/redact-protected-b "Kirk (Security Lead) concerned about R-003 (FinOps) in Scenario A (Q3 2026)"` → "Security stakeholder concerned about cost model risk in Scenario A (near term)"

**`/log-sharing`**
- Input: What shared, when, to whom, why, with what approval status
- Output: Audit record created + confirmation
- Stateful: Writes to audit log (persistent)
- Core Logic: Format and append to audit log
- Example: `/log-sharing content=ADR-002 target=Claude approved=yes reason="GAT analysis with Level 2 flag"`

**`/escalate-protection`**
- Input: Suspected Protected B exposure or policy violation
- Output: Alert + escalation path
- Stateless: Reads governance rules
- Example: `/escalate-protection "Workload names (PMRA) mentioned to external service"` → Alert Kirk (Security Lead) + EA Lead

### Analysis & Knowledge Skills

**`/query-scenarios`**
- Input: Natural language question about convergence scenarios
- Output: Answer from knowledge graph
- Stateless: Reads from MCP-connected Neo4j
- Core Logic: Translate question to graph query, format results
- Example: `/query-scenarios "What risks does Scenario A leave open?"` → "Scenario A leaves R-001 (ATO path blocked) open unless SoS completed"

**`/scenario-tradeoff`**
- Input: Two scenarios to compare
- Output: Structured comparison (timeline, cost, governance, operations, risk profile)
- Stateless: Reads from knowledge graph
- Core Logic: Match scenarios, extract tradeoff dimensions, format as table
- Example: `/scenario-tradeoff A vs B` → Table showing Scenario A (slower, unified, lower shadow AI risk) vs B (faster, split, higher operational overhead)

**`/stakeholder-position`**
- Input: Stakeholder name + optional topic
- Output: Known positions, concerns, preferences
- Stateless: Reads from knowledge graph
- Core Logic: Query stakeholder node + relationships
- Example: `/stakeholder-position Kirk security` → "Kirk prefers single ATO path; concerned about data residency; requires Protected B handling compliance"

**`/risk-scenario-impact`**
- Input: Risk ID
- Output: How scenario A/B/C affects that risk
- Stateless: Reads from knowledge graph
- Core Logic: Match risk, find scenario relationships, summarize impact
- Example: `/risk-scenario-impact R-003` → "R-003 (FinOps): LOW impact in A (unified model), HIGH impact in B (separate models), MEDIUM in C (deferred)"

### Deliverable Support Skills

**`/validate-deliverable`**
- Input: Deliverable draft + deliverable type (P1/P2/P3/P4/P5)
- Output: Validation report (completeness, evidence quality, decision readiness)
- Stateless: Pattern matching against deliverable template
- Core Logic: Check sections complete, evidence cited, no unjustified claims
- Example: `/validate-deliverable 001-convergence-framing.md P1` → "P1 complete: 3 scenarios defined, tradeoff table present, EA recommendation stated, quality gate passed"

**`/evidence-check`**
- Input: Claim + supporting evidence references
- Output: Evidence quality assessment (sourced, recent, credible, sufficient)
- Stateless: Pattern matching
- Core Logic: Verify evidence cited, check recency (source date), assess sufficiency for claim weight
- Example: `/evidence-check "Scenario A reduces Shadow AI risk" sources=["ADR-002", "Risk Register", "WAF Assessment"]` → "Evidence sufficient: 3 sources, current, interdependent"

---

## 3. Skill Discovery & Composition

### Current Approach: Claude-Orchestrated

**How It Works:**
1. User invokes Claude with a task ("Draft convergence framing with data governance checks")
2. Claude recognizes the task requires multiple skills
3. Claude invokes skills in sequence based on reasoning:
   - `/classify-data` on initial content
   - `/validate-deliverable` as draft progresses
   - `/evidence-check` before finalizing
   - `/log-sharing` if content gets shared externally
4. Claude learns from each skill result and adjusts next steps
5. Claude explicitly tells user which skills are being used and why

**Advantage:** Claude stays in control; skills can be chained dynamically; new skills can be discovered and used without predefined chains

**Limitation:** Requires Claude to know skill names and signatures; "discovery" is implicit in training data, not explicit discovery mechanism

### Skill Registry (Simple Approach)

**In Repo Root: SKILLS-AVAILABLE.md**

```
# Available Skills for EA Platform Convergence

## Data Governance
- /classify-data — Determine Level 1/2/3 classification
- /approve-sharing — Check service approval status
- /redact-protected-b — Remove Protected B identifiers
- /log-sharing — Record Level 2+ sharing to audit log
- /escalate-protection — Alert on suspected violations

## Analysis & Knowledge
- /query-scenarios — Ask knowledge graph questions
- /scenario-tradeoff — Compare two scenarios
- /stakeholder-position — Get known stakeholder positions
- /risk-scenario-impact — Analyze how risk affects scenarios

## Deliverable Support
- /validate-deliverable — Check deliverable completeness
- /evidence-check — Assess evidence quality and sufficiency

## Invocation Pattern
/skill-name input [options]

Example: /classify-data "Scenario A timeline Q3 2026"
```

**When to Use Registry:**
- Onboarding new team members (visible list of capabilities)
- Skill discoverability in large libraries (100+ skills)
- Documentation of available capabilities

**Alternative: Implicit Discovery**
- No registry; skills discoverable only through experience or documentation
- Simpler to maintain; less overhead
- Works well for small skill libraries (<20 skills)

---

## 4. Skill Implementation Standards

### Signature & Documentation

```
/skill-name
Input: [What the skill accepts]
Output: [What the skill returns]
State: [Stateless / Reads from X / Writes to Y]
Error Handling: [How it fails safely]
Example: /skill-name "example input" → "example output"
```

### Execution Context

**Available to Skill:**
- Current user (from Claude session context)
- Current project/repository (if invoked in repository context)
- Access to MCP servers (Neo4j, governance rules)
- Read-only access to persistent governance rules

**Not Available to Skill:**
- Session-specific context from previous turns (skills are stateless)
- Other skills' outputs (unless Claude pipes them)
- Write access to sensitive logs (only `/log-sharing` writes audit)

### Error Cases

**Graceful Degradation:**
- Classification uncertain? Return both options with confidence scores
- Service approval not found? Escalate to EA Lead with reasoning
- Knowledge graph query fails? Return "Unable to access current data; refer to deliverable X"
- Protected B detected unexpectedly? Escalate immediately, don't proceed

**User Communication:**
- Errors are informative (why did it fail, what's next)
- Errors don't expose system details (no stack traces, no database queries)
- Errors include escalation path (who to contact)

---

## 5. Stateless Skills + Stateful MCP

### Division of Concern

**Skills are stateless by design:**
- No persistent side effects
- Input → output mapping
- Idempotent (same input always yields same output)
- Can be executed in any order
- Can be retried safely

**State lives in MCP servers:**
- Knowledge graph (Neo4j): Scenarios, risks, decisions, stakeholder positions
- Governance rules: Classification levels, service approvals, redaction rules
- Audit log: All Level 2+ sharing events
- Deliverable versioning: Historical versions of P1-P5

**Example Workflow:**
```
Claude task: "Check if we can share Scenario A analysis with ChatGPT"

Step 1: /classify-data "Scenario A analysis..." → Level 2
Step 2: /approve-sharing "Level 2" "ChatGPT" → Conditional (requires CDO approval)
Step 3: Claude asks user "This is Level 2 content. ChatGPT requires CDO approval. Should I proceed?"
Step 4: If approved, /log-sharing → Audit record created in MCP
Step 5: If denied, /redact-protected-b → Prepare sanitized version
```

In this workflow:
- Skills make decisions (classify, check approval)
- MCP records state (audit log)
- Claude orchestrates flow
- User makes governance decision (approval)

---

## 6. Skill Expansion Over Time

### Phase 1 (Now): Core 12 Skills
- 5 data governance skills
- 4 analysis/knowledge skills
- 2 deliverable support skills
- 1 utility skill

**Target:** Cover MVP for convergence analysis without overwhelming complexity

### Phase 2 (Month 2): Extended Skills
- **Stakeholder Management:** /schedule-meeting, /summarize-feedback, /validate-alignment
- **Document Management:** /version-deliverable, /diff-versions, /package-for-arb
- **Risk Management:** /risk-trend, /mitigation-update, /residual-assessment
- **Decision Support:** /compare-options, /build-case, /identify-gaps

### Phase 3 (Month 3+): Cross-Project Skills
- **Reference Architecture:** /find-similar-decision, /adapt-pattern, /document-learning
- **Skill Composition:** /auto-chain-skills, /skill-discovery, /create-workflow
- **Reusability:** /extract-pattern, /publish-template, /rate-reuse

**Growth Pattern:**
- Start focused (12 skills, high utility)
- Expand based on actual EA work (what do we ask Claude to do repeatedly?)
- Consolidate if library grows (are we building new skills instead of using existing ones?)

---

## 7. Skill Composition Patterns

### Pattern 1: Sequential Validation
```
User: "Draft P1 and validate it"
Claude:
  1. [Generate draft]
  2. /validate-deliverable P1 → Feedback
  3. [Revise based on feedback]
  4. /evidence-check → Sufficiency assessment
  5. [Strengthen weak evidence]
  6. /validate-deliverable P1 → Quality gate passed
```

### Pattern 2: Governance-First
```
User: "Share scenario analysis with PMRA"
Claude:
  1. /classify-data → Level 2
  2. /approve-sharing Level 2 PMRA → Approved
  3. [Share content]
  4. /log-sharing → Audit record
```

### Pattern 3: Knowledge Graph Query
```
User: "Which scenarios mitigate R-002?"
Claude:
  1. /query-scenarios "What scenarios mitigate R-002?" → Scenario A fully, B partially
  2. [Interpret results]
  3. /risk-scenario-impact R-002 → Impact breakdown
  4. [Compose answer with evidence]
```

### Pattern 4: Stakeholder Alignment
```
User: "Make sure analysis aligns with Kirk's concerns"
Claude:
  1. /stakeholder-position Kirk → Known positions
  2. [Review draft against Kirk's concerns]
  3. /evidence-check Kirk-relevant claims → Assessment
  4. [Strengthen alignment]
```

---

## 8. Open Challenges & Future Work

**Skill Discovery at Scale:**
- How does a new team member find "the skill for X"?
- Current: Ask Claude; Claude knows from training
- Future: Skill registry with full-text search?
- Risk: Skill library becomes "knowledge debt" if not maintained

**Skill Dependencies:**
- Some skills depend on MCP (knowledge graph, audit log)
- What happens if MCP is down?
- Current: Graceful degradation (return "data unavailable")
- Future: Offline skill mode?

**Skill Composition Optimization:**
- Should Claude always invoke /validate-deliverable before /evidence-check?
- Current: Claude decides based on reasoning
- Future: Learn patterns from experience (which skill chains are most effective)?

**Skill Naming & Discovery:**
- `/classify-data` vs. `/classify` vs. `/assess-classification`?
- Consistency matters for mental model
- Current: Verb-noun pattern (action-object)
- Future: Naming conventions enforced in skill registry?

---

## 9. How Agents Consume Skills

### Agent as Orchestrator

**EA Platform Convergence Agent uses skills:**
1. **Onboarding Phase:** `/validate-deliverable` templates to ensure team understands structure
2. **Stakeholder Feedback Phase:** `/stakeholder-position` to check alignment
3. **Draft Phase:** `/validate-deliverable` and `/evidence-check` on P1-P5
4. **Governance Phase:** `/classify-data` and `/log-sharing` for all sharing events
5. **Finalization Phase:** `/scenario-tradeoff` in executive summary, `/validate-deliverable` for ARB readiness

**Agent-Skill Relationship:**
- Agent doesn't define or build skills
- Agent assumes skills exist and are stable
- Agent orchestrates skill invocation based on workflow
- Agent logs all skill usage (what was called, when, result) for audit

### Future Agent Patterns

**Pattern 1: Custom Agent with Specialized Skills**
- Surveillance Platform Convergence Agent
- Reuses EA governance skills
- Adds Surveillance-specific skills (/threat-assessment, /legal-compliance, etc.)

**Pattern 2: Cross-Project Skill Library**
- All agents share core skills (/classify-data, /log-sharing, etc.)
- Project-specific skills live in project directories
- Governance skills versioned and managed centrally

---

## 10. Tension: Simplicity vs. Power

| Aspect | Current Preference | Tension | Alternative |
|---|---|---|---|
| **Skill Size** | 5–10 lines core logic | Smaller = easier to understand; larger = more useful | Monolithic 50-line skills |
| **Discovery** | Implicit (Claude knows) | Works now; breaks at scale | Explicit registry (governance overhead) |
| **Composition** | Claude decides | Flexible, learning; unpredictable | Hardcoded chains (predictable, brittle) |
| **State** | Stateless skills + MCP | Separation of concerns; more moving parts | Stateful skills (simpler, less composable) |
| **Error Handling** | Graceful degradation | Safe, but masks issues | Fail-fast (clear, but breaks workflows) |

---

## Navigation

This is Part 4 of 7. Read in this order:

1. Core Principles & Philosophy
2. Reference Architecture: EA Platform Convergence
3. Neo4j Knowledge Graph Schema
4. **Modular Agent & Skill Components** ← You are here
5. Zero Trust Governance Framework
6. Modularity & Reuse Patterns
7. Architectural Vision Synthesis

**Next Document:** Zero Trust Governance Framework

*Classification: Unclassified / For Internal Use*
