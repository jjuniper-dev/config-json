# Architectural Vision: EA Platform & Knowledge Systems
## Core Principles & Philosophy

**Status:** Working Document / Emergent Vision  
**Classification:** Unclassified / For Internal Use  
**Date:** April 24, 2026  
**Note:** This vision reflects *current preference* in areas marked. All approaches remain open to evolution based on organizational learning.

---

## 1. Core Principles (Current Preference)

### 1.1 Modularity First
**Philosophy:** Build composable, independently testable, reusable components rather than monolithic systems.

**Current Preference:**
- Organize around logical domains (governance, analysis, knowledge representation) not technical layers
- Each module has clear input/output contracts
- Minimal coupling between modules
- Modules can be deployed/upgraded independently

**Why It Matters:**
- Enables reuse across different EA decisions (not just PATH/HAIL)
- Reduces risk of changes cascading
- Allows teams to own specific modules
- Supports rapid iteration without full system rebuild

**Open Questions:**
- How granular should modules be? (Function? Class? Service?)
- What's the "right" size for a reusable agent module?
- How do we prevent modules from fragmenting into unmaintainable pieces?

**Alternative Approaches:**
- Monolithic agents (faster to deploy, harder to reuse, brittle)
- Microservices architecture (more modular, higher operational overhead)

---

### 1.2 Thoughtful MCP Usage
**Philosophy:** Model Context Protocol (MCP) is a tool for specific problems, not a default. Use it when context window efficiency or tool composition matters.

**Current Preference:**
- Use MCP for: Persistent state (knowledge graphs), Tool orchestration (multiple skills), Complex multi-step workflows
- Don't use MCP for: Simple one-off queries, prototypes, throwaway analysis
- Design MCP servers as domain models, not generic wrappers

**Why It Matters:**
- MCP adds complexity; only justify when benefit is clear
- Domain-specific MCP servers (Neo4j for knowledge graphs) are more valuable than generic tooling
- Enables Claude to reason over persistent data structures

**Open Questions:**
- When does prototype complexity justify moving to MCP?
- How do we avoid MCP becoming "yet another interface" overhead?
- What's the threshold for moving analysis work from session-based to persistent?

**Alternative Approaches:**
- Session-based analysis (stateless, simple, no persistence)
- Traditional APIs (explicit, but not Claude-native)
- Direct database access (fast, but no abstraction layer)

---

### 1.3 Skills as Composable Capabilities
**Philosophy:** Skills (Claude Code slash commands) are building blocks for workflows, not monolithic tools.

**Current Preference:**
- Small, focused skills (5–10 lines of core logic)
- Skills combine via user prompts and context, not hardcoded orchestration
- Skills leverage Claude's reasoning to decide when/how to invoke other skills
- Skills are stateless by default; stateful behavior goes in MCP servers

**Why It Matters:**
- Keeps Claude in control of workflows (not rigid automation)
- Easier to understand, test, and modify individual skills
- Reduces risk of skill dependencies breaking workflows

**Open Questions:**
- How do we discover and chain skills without hardcoding orchestration?
- When should skill composition be explicit (user chooses chain) vs. implicit (Claude decides)?
- What's the skill discovery mechanism in large skill libraries?

**Alternative Approaches:**
- Monolithic multi-function skills (easier to deploy, harder to reuse)
- Full orchestration via MCP (more control, more complexity)
- No skills, direct API calls (less Claude-native)

---

### 1.4 Zero Trust Architecture
**Philosophy:** Never assume trust. Verify every interaction. Design for breach.

**Current Preference (Data & Services):**
- **Always classify data** (Level 1-3) before any action
- **Always authenticate** external service requests with explicit approval (not implicit)
- **Always redact** Protected B before external sharing
- **Always log** Level 2+ interactions for audit
- **Assume breach:** Design so Protected B exposure is contained and detectable
- **Verify every tool/service** before use (check approval matrix)
- **Assume Claude context is not private** — design as if conversation could be exposed

**Why It Matters:**
- Shifts security from "prevent all breaches" (impossible) to "detect and contain quickly"
- Makes data handling visible (not implicit)
- Enables compliance audits with clear evidence
- Reduces insider threat surface

**Open Questions:**
- How do we balance zero trust rigor with development velocity?
- What's acceptable latency for approval workflows (should data governance slow decision-making)?
- How granular should audit logging be (every query vs. summary)?

**Alternative Approaches:**
- Trust-first (faster, riskier)
- Implicit approval for known services (efficient, compliance risk)
- Manual approval for everything (slow, exhausting)

---

### 1.5 Working Prototypes Over Perfect Plans
**Philosophy:** Build, test, learn. Don't plan beyond 2 weeks.

**Current Preference:**
- Prototype convergence analysis (P1–P5 deliverables) with real data early
- Test with actual stakeholders (Kirk, Jason, PMRA) by Week 2
- Iterate based on feedback; revise plans weekly
- Accept that initial templates won't be final

**Why It Matters:**
- Reveals hidden assumptions early (not Week 4 when it's "done")
- Stakeholder feedback shapes direction, not abstract planning
- Reduces rework by catching misalignment early
- Builds confidence in deliverables

**Open Questions:**
- How "rough" can a prototype be before it's unusable?
- When does prototyping become procrastination (endless iteration)?
- How do we know when to stop prototyping and finalize?

**Alternative Approaches:**
- Waterfall planning (clear timeline, risky misalignment)
- Continuous evolution (no end state, hard to know when to stop)
- Agile sprints (structured, may over-engineer for EA work)

---

### 1.6 Reference Architectures, Not Blueprints
**Philosophy:** Show how *we* solve problems, not prescribe how *you* must. Design for our context.

**Current Preference:**
- Reference architectures are templates, not mandates
- Each architecture includes: Problem statement, Our solution, Tradeoffs, Alternatives, When to use
- Architectures evolve as we learn; old versions stay available
- New projects use reference architecture as starting point, then adapt

**Why It Matters:**
- Avoids "architecture theater" (rules no one follows)
- Enables learning from past work without cargo-cult implementation
- Builds institutional knowledge over time
- Allows healthy disagreement ("why did we choose this way?")

**Open Questions:**
- How many reference architectures can we maintain without becoming a burden?
- When should a reference architecture be updated vs. deprecated?
- How do we prevent reference architectures from becoming cargo cult?

**Alternative Approaches:**
- Strict blueprints (consistency, but brittle)
- No guidance, each project invents (learning, but chaotic)
- Best practices from outside orgs (proven, but not our context)

---

### 1.7 Neo4j & Knowledge Graphs
**Philosophy:** Make relationships explicit. Use knowledge graphs to reason over complex EA domains.

**Current Preference:**
- Neo4j as system of record for EA knowledge (not just documentation)
- Design schemas around EA concepts: Components, Decisions, Risks, Stakeholders, Tradeoffs
- Enable graph queries to answer questions: "What risks affect this decision?", "Which components depend on this architecture?", "Who approved this?"
- MCP server as Claude's interface to the graph (not direct SQL)

**Why It Matters:**
- Captures relationships that tables hide
- Enables reasoning over dependencies and tradeoffs
- Makes implicit knowledge explicit (governance decisions, stakeholder positions)
- Supports queries no one anticipated (graph allows exploration)

**Open Questions:**
- What entities and relationships are essential vs. nice-to-have in EA schema?
- How do we keep the graph accurate (stale data is worse than no data)?
- How do we query the graph without Neo4j expertise required?

**Alternative Approaches:**
- Relational database (simpler, harder to query relationships)
- Document store (flexible schema, no built-in relationships)
- Spreadsheets (accessible, doesn't scale, relationships implicit)

---

## 2. Architectural Principles (Derived from Above)

1. **Design for composition** — Modules, skills, components are pluggable
2. **Make decisions explicit** — ADRs, graphs, logs capture why, not just what
3. **Verify before trusting** — Zero trust data, zero trust services
4. **Iterate with stakeholders** — Prototypes by Week 2, feedback by Week 3
5. **Learn from patterns** — Reference architectures capture institutional knowledge
6. **Make relationships visible** — Knowledge graphs surface dependencies
7. **Keep options open** — Preferences are current, not permanent; alternatives documented

---

## 3. How This Vision Applies (Concrete Example: PATH/HAIL Convergence)

**Modularity:**
- Governance module (data classification, approval rules)
- Analysis module (convergence framing, risk assessment)
- Knowledge graph module (scenario relationships, tradeoff dependencies)
- Skills module (redaction, classification, audit logging)

**MCP:**
- Neo4j MCP server (Claude queries convergence scenarios, risks, stakeholder positions)
- Not used for: Single ARB briefing, simple data sharing

**Skills:**
- /classify-data — Determine Level 1-3
- /redact-protected-b — Remove workload/stakeholder names
- /log-sharing — Record Level 2+ interactions
- /query-scenarios — Ask graph questions about convergence

**Zero Trust:**
- Every external service request requires classification + approval
- All stakeholder interactions logged
- Assume PMRA/security team reads our analysis

**Working Prototype:**
- Week 1: Rough P1 draft with initial scenarios
- Feedback from Kirk, Jason, Chad by end of Week 1
- Week 2: Revised P1 based on feedback; add P2 & P3

**Reference Architecture:**
- This convergence analysis becomes template for future platform decisions
- Other teams can adapt: "We used this for PATH/HAIL, you might adapt it for X"

**Knowledge Graph:**
- Nodes: PATH, HAIL, Scenario A/B/C, Risk-001 through Risk-005, Stakeholder positions
- Edges: "Scenario A mitigates Risk-002", "Risk-003 affects FinOps", "Kirk approved ADR-002"
- Queries: "What risks does Scenario A leave open?", "Which stakeholders are concerned about FinOps?"

---

## 4. Current State vs. Emergent State

**Current State (April 2026):**
- ✅ Modularity: Data governance (4 files), Agent (9 files) are separate
- ⚠️ MCP: Not yet implemented; would enhance Neo4j integration
- ✅ Skills: Skeleton in place (/classify, /redact, /log); could expand
- ✅ Zero Trust: Data governance framework covers this
- ✅ Prototyping: Architecture designed for Week 1-2 drafts + feedback
- ✅ Reference Architecture: Convergence agent is a template for future work
- 🔲 Knowledge Graph: Schema designed, not yet populated

**Emergent State (Next 6–12 Months):**
- All modules published and documented
- MCP server running against Neo4j for EA graph queries
- Skill library expanded to 10+ reusable capabilities
- Knowledge graph populated with historical decisions, risks, scenarios
- Multiple convergence analyses completed using reference architecture
- Institutional knowledge codified in graph (easier to onboard new team members)

---

## 5. Tensions & Tradeoffs (Honest Assessment)

| Principle | Tension | Current Preference | Alternative |
|---|---|---|---|
| Modularity | More modules = more coordination overhead | Start modular, consolidate if needed | Build monolithic, refactor later |
| MCP Usage | MCP adds complexity; justification unclear early | Use for Neo4j only; reconsider quarterly | No MCP; keep everything session-based |
| Skills | Small skills require Claude orchestration (less predictable) | Let Claude decide; log and learn | Large predetermined skill chains |
| Zero Trust | Approval workflows slow decisions | Async approval (log + review later) | Implicit trust for known services |
| Prototypes | Messy; stakeholders may confuse prototype with plan | Label clearly as prototype; iterate quickly | Perfect plans before showing anything |
| Reference Arch | Old architectures become tech debt | Version them; deprecate explicitly | New reference architecture each time |
| Knowledge Graph | Requires discipline to keep current | Automate population from logs/decisions | Manual updates (stale data risk) |

---

## 6. Decision: Current Preference vs. Open Options

**This is our current preference based on HC/PHAC context:**
- Small modular components (not monolithic)
- MCP for Neo4j only (not overused)
- Claude-orchestrated skills (not hardcoded chains)
- Zero trust for all data (not implicit trust)
- Working prototypes with real stakeholders (not abstract plans)
- Reference architectures as guides (not mandates)
- Knowledge graphs to make relationships visible (not optional)

**But we remain open to:**
- Learning this is wrong and course-correcting
- Different approaches for different contexts
- Hybrid strategies (e.g., MCP for some use cases, not others)
- Emergent practices we haven't anticipated

**The measure of success:** Does this architecture enable the work we're trying to do (ARB convergence analysis) and make it easier to do similar work in the future?

---

## 7. How to Use This Vision Document

**For new projects:**
- Start here to understand principles
- Review specific reference architectures (next document)
- Adapt, don't copy; optimize for your context

**For design decisions:**
- Check which principle applies
- Review current preference and alternatives
- Decide if alternative is better for your case
- Document your decision (why you diverged)

**For quarterly reviews:**
- Re-read this document
- Ask: Which principles paid off? Which created friction?
- Update preferences based on learning
- Share updates with team

---

## 8. Navigation

This vision document is Part 1 of 7. Read in this order:

1. **Core Principles & Philosophy** ← You are here
2. **Reference Architecture: EA Platform Convergence** — How principles apply to PATH/HAIL
3. **Neo4j Knowledge Graph Schema** — Structure for EA work
4. **Modular Agent & Skill Components** — Reusable pieces
5. **Zero Trust Governance Framework** — Data & service security
6. **Modularity & Reuse Patterns** — How to build for reuse
7. **Architectural Vision Synthesis** — Tie it all together

---

**Next Document:** Reference Architecture: EA Platform Convergence

*Classification: Unclassified / For Internal Use*
