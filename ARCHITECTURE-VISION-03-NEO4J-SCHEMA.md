# Architectural Vision: Neo4j Knowledge Graph Schema
## EA Work as a Queryable Graph

**Status:** Working Document / Current Schema Design  
**Classification:** Unclassified / For Internal Use  
**Date:** April 24, 2026

---

## 1. Why Neo4j? (Current Preference)

**Problem:** Complex EA decisions have hidden relationships.
- What risks affect Scenario A?
- Which stakeholders are concerned about FinOps?
- What's the dependency chain from current state to Protected B capability?
- Did we make this decision before? What did we learn?

**Solution:** Graph database makes relationships first-class.
- Nodes: Scenarios, Risks, Decisions, Stakeholders, Components
- Edges: "affects", "mitigates", "concerns", "depends_on", "approves"
- Queries: Natural questions, not SQL

**Current Preference:**
- Neo4j is system of record for EA knowledge (not just documentation)
- MCP server abstracts complexity (Claude doesn't write Cypher)
- Populated automatically from decisions, logs, stakeholder feedback
- Queries enable discovery ("What haven't we thought about?")

---

## 2. Core Entities & Relationships

### Entities (Node Types)

**SCENARIO**
- Properties: id (A/B/C), name, description, timeline, operationalComplexity
- Examples: "Scenario A: Single Governed Platform", "Scenario B: Co-Equal Platforms"
- Created: Week 1 (initial ideas)
- Updated: Week 2–3 (stakeholder feedback)

**RISK**
- Properties: id (R-001 to R-005), statement, probability, impact, currentMitigation, residualRisk
- Examples: "R-002: Shadow AI — Protected B workloads route to ungoverned platforms"
- Created: Week 1 (identified from current state)
- Updated: Week 3 (after stakeholder validation)

**DECISION** (Architecture Decision Record)
- Properties: id (ADR-002), title, decision, context, consequence, status (Draft/Accepted/Deprecated)
- Examples: "ADR-002: Protected B Hosting (Azure.us vs. Commercial Azure)"
- Created: Week 2
- Updated: Week 3 (stakeholder approval)

**STAKEHOLDER**
- Properties: name, role, organization, email, expertise
- Examples: "Kirk (Security Lead)", "Jason (Cloud Operations)", "Sam (PMRA)"
- Attributes: Who approved what? Who was concerned about what?
- Created: Week 1
- Updated: Ongoing (as stakeholders engage)

**COMPONENT** (Technology/Architecture Element)
- Properties: id, name, type (platform, service, pattern), description, owner
- Examples: "PATH (HC governance control plane)", "HAIL (PHAC operational runtime)"
- Relationships: "PATH depends_on Azure AI Foundry"
- Created: Week 1 (current state)
- Updated: As new components discovered

**CAPABILITY** (Feature/Function)
- Properties: id, name, category (governance, operations, data), priority
- Examples: "Protected B audit trail", "FinOps cost attribution", "Self-service deployment"
- Relationships: "Scenario A enables Protected B audit trail by Q3 2026"
- Created: Week 1
- Updated: As scenarios refined

**TRADEOFF**
- Properties: id, dimension (timeline, cost, governance, operations), description
- Examples: "Scenario A longer timeline but unified governance", "Scenario B faster near-term but operational overhead"
- Relationships: Links scenarios to tradeoff dimensions
- Created: Week 2
- Updated: Week 3 (refine based on WAF assessment)

---

### Relationships (Edge Types)

| Edge | From → To | Meaning | Example |
|---|---|---|---|
| **MITIGATES** | Scenario → Risk | Scenario reduces risk | "Scenario A MITIGATES R-002 (Shadow AI)" |
| **LEAVES_OPEN** | Scenario → Risk | Risk not mitigated in scenario | "Scenario C LEAVES_OPEN R-004 (Governance deferred)" |
| **AFFECTS** | Risk → Scenario | Risk impacts scenario | "R-003 (FinOps) AFFECTS all scenarios" |
| **DEPENDS_ON** | Component → Component | Component dependency | "PATH DEPENDS_ON Azure AI Foundry" |
| **INVOLVES** | Stakeholder → Decision | Stakeholder part of decision | "Kirk INVOLVES ADR-002 (approves/reviews)" |
| **CONCERNED_ABOUT** | Stakeholder → Risk | Stakeholder worried about risk | "Jason CONCERNED_ABOUT R-003 (FinOps)" |
| **PREFERS** | Stakeholder → Scenario | Stakeholder's preference | "Kirk PREFERS Scenario A (higher assurance)" |
| **ENABLES** | Scenario → Capability | Scenario delivers capability | "Scenario A ENABLES Protected B audit trail (Q3 2026)" |
| **HAS_TRADEOFF** | Scenario → Tradeoff | Tradeoff in scenario | "Scenario A HAS_TRADEOFF (longer timeline, unified governance)" |
| **ADDRESSES** | Decision → Risk | ADR mitigates risk | "ADR-002 ADDRESSES data residency constraint" |
| **REFERENCES** | Document → Node | Document discusses node | "P1 (Convergence Framing) REFERENCES Scenario A/B/C" |

---

## 3. Concrete Schema (PATH/HAIL Convergence)

### Nodes (Example Data)

```cypher
// Scenarios
CREATE (scenarioA:SCENARIO {
  id: "A",
  name: "Single Governed Platform (Converge)",
  timeline: "Q3 2026 (ATO), Q1 2027 (first Protected B workload)",
  operationalComplexity: "HIGH (upfront integration cost)",
  description: "HAIL runtime + PATH governance layer unified"
})

CREATE (scenarioB:SCENARIO {
  id: "B",
  name: "Co-Equal Platforms with Integration Points",
  timeline: "Q1 2026 (HAIL production), Q3 2026 (both platforms mature)",
  operationalComplexity: "VERY_HIGH (two platforms, coordination overhead)",
  description: "PATH and HAIL remain separate with governance integration"
})

CREATE (scenarioC:SCENARIO {
  id: "C",
  name: "PHAC-Led Single Platform (Defer PATH)",
  timeline: "Q1 2026 (HAIL production, governance deferred), Q2–Q3 2026 (governance post-production)",
  operationalComplexity: "MEDIUM (single platform, but governance immature)",
  description: "HAIL as sole enterprise platform, PATH governance incorporated post-ATO"
})

// Risks
CREATE (riskShadowAI:RISK {
  id: "R-002",
  statement: "Shadow AI: Protected B workloads route to ungoverned platforms",
  probability: "MEDIUM-HIGH (if convergence delayed)",
  impact: "HIGH (regulatory exposure, audit trail gaps)",
  residualRisk: "MEDIUM-HIGH"
})

CREATE (riskFinOps:RISK {
  id: "R-003",
  statement: "FinOps complexity: Separate cost models if platforms don't converge",
  probability: "MEDIUM",
  impact: "MEDIUM (affects budget planning, client billing)",
  residualRisk: "HIGH"
})

// Stakeholders
CREATE (kirk:STAKEHOLDER {
  name: "Kirk",
  role: "Security Lead",
  organization: "HC Security",
  expertise: "ATO, data residency, Protected B requirements"
})

CREATE (jason:STAKEHOLDER {
  name: "Jason",
  role: "Cloud Operations Lead",
  organization: "HC Cloud Operations",
  expertise: "Azure, FinOps, operational support"
})

// Components
CREATE (path:COMPONENT {
  id: "PATH",
  name: "PATH (HC AI Governance Control Plane)",
  type: "PLATFORM",
  owner: "HC DTB"
})

CREATE (hail:COMPONENT {
  id: "HAIL",
  name: "HAIL (PHAC Operational AI Runtime)",
  type: "PLATFORM",
  owner: "PHAC"
})

CREATE (foundry:COMPONENT {
  id: "Azure_AI_Foundry",
  name: "Azure AI Foundry",
  type: "SERVICE",
  owner: "Microsoft"
})

// Capabilities
CREATE (protectedBAudit:CAPABILITY {
  id: "protected-b-audit",
  name: "Protected B with Audit Trail",
  category: "GOVERNANCE",
  priority: "P1"
})

CREATE (finopsAttribution:CAPABILITY {
  id: "finops-attribution",
  name: "Per-Workload Cost Attribution",
  category: "OPERATIONS",
  priority: "P1"
})
```

### Relationships (Example Data)

```cypher
// Scenario A mitigates Shadow AI risk
MATCH (scenarioA:SCENARIO {id: "A"}), (riskShadowAI:RISK {id: "R-002"})
CREATE (scenarioA)-[:MITIGATES {strength: "HIGH", timeline: "Q3 2026"}]->(riskShadowAI)

// Scenario C leaves Shadow AI risk open
MATCH (scenarioC:SCENARIO {id: "C"}), (riskShadowAI:RISK {id: "R-002"})
CREATE (scenarioC)-[:LEAVES_OPEN {reason: "Governance deferred to post-production"}]->(riskShadowAI)

// FinOps risk affects all scenarios differently
MATCH (scenarioA:SCENARIO {id: "A"}), (riskFinOps:RISK {id: "R-003"})
CREATE (riskFinOps)-[:AFFECTS {severity: "LOW", mitigation: "Unified FinOps model"}]->(scenarioA)

MATCH (scenarioB:SCENARIO {id: "B"}), (riskFinOps:RISK {id: "R-003"})
CREATE (riskFinOps)-[:AFFECTS {severity: "HIGH", mitigation: "Separate cost models"}]->(scenarioB)

// Stakeholder concerns
MATCH (jason:STAKEHOLDER), (riskFinOps:RISK {id: "R-003"})
CREATE (jason)-[:CONCERNED_ABOUT {reason: "FinOps model directly affects client onboarding"}]->(riskFinOps)

// PATH depends on Azure AI Foundry
MATCH (path:COMPONENT {id: "PATH"}), (foundry:COMPONENT {id: "Azure_AI_Foundry"})
CREATE (path)-[:DEPENDS_ON {constraint: "Availability of Foundry features"}]->(foundry)

// Scenario A enables Protected B audit capability
MATCH (scenarioA:SCENARIO {id: "A"}), (protectedBAudit:CAPABILITY {id: "protected-b-audit"})
CREATE (scenarioA)-[:ENABLES {timeline: "Q3 2026 (ATO)"}]->(protectedBAudit)

// Scenario C leaves Protected B deferred
MATCH (scenarioC:SCENARIO {id: "C"}), (protectedBAudit:CAPABILITY {id: "protected-b-audit"})
CREATE (scenarioC)-[:ENABLES {timeline: "Q3-Q4 2026 (post-production governance)"}]->(protectedBAudit)
```

---

## 4. Example Queries (Claude via MCP)

**Claude asks the graph:**

```
Query: "What risks does Scenario A leave open?"
MATCH (scenarioA:SCENARIO {id: "A"})-[:LEAVES_OPEN]->(risks)
RETURN risks
Result: [] (none — Scenario A mitigates all P1 risks)

---

Query: "Which stakeholders are concerned about FinOps?"
MATCH (stakeholder:STAKEHOLDER)-[:CONCERNED_ABOUT]->(risk:RISK {id: "R-003"})
RETURN stakeholder.name, stakeholder.role
Result: Jason (Cloud Operations), Finance VP

---

Query: "What's the shortest path from current state to Protected B capability?"
MATCH path = (scenarioC)-[:ENABLES]->(protectedBAudit)
WHERE protectedBAudit.id = "protected-b-audit"
RETURN path, length(path) as hops
Result: Scenario C → Protected B audit (1 hop, fastest)

---

Query: "Which components does PATH depend on that might not be available?"
MATCH (path:COMPONENT {id: "PATH"})-[:DEPENDS_ON]->(dependency)
OPTIONAL MATCH (dependency)-[:UNAVAILABLE_IN]->(cloudPlatform)
RETURN dependency, cloudPlatform
Result: PATH depends on Azure AI Foundry (not available in Azure.us without workaround)
```

**Claude synthesizes query results into analysis:**

"Scenario A enables Protected B audit trail by Q3 2026 (highest assurance). However, PATH depends on Azure AI Foundry availability. If we choose Scenario A on Azure.us, Foundry unavailability becomes a critical constraint. Jason (Cloud Ops) is concerned about R-003 (FinOps). In Scenario A, FinOps is resolved (unified model); in Scenario B, FinOps complexity increases. This aligns with Jason's preference for Scenario A."

---

## 5. Population Strategy (How Data Gets In)

**Week 1: Initial Population**
- Scenarios A/B/C created manually
- 5 key risks identified from current state docs
- Stakeholders identified
- Components (PATH, HAIL, Azure) added

**Week 2–3: Stakeholder Feedback**
- After Kirk meeting: Update his preferences, add his concerns
- After Jason meeting: Update his FinOps concerns, operational constraints
- After PMRA meeting: Add use cases, dependencies
- Relationships updated as feedback arrives

**Week 4: Decision Finalization**
- ADRs added (ADR-002 created with decision + rationale)
- Stakeholder approvals recorded
- Timeline estimates updated
- Risk mitigations finalized

**Ongoing (Post-Convergence Decision):**
- ARB decision recorded (which scenario was chosen)
- Execution risks tracked (as project progresses)
- Lessons learned added
- Future projects reference this graph ("What did we learn about FinOps from PATH/HAIL?")

---

## 6. MCP Server Interface (What Claude Sees)

**MCP Server Abstracts Complexity**

Claude doesn't write Cypher. Claude asks natural questions:

```
User: "What risks affect Scenario A?"
MCP Handler:
  1. Parse user query → identify entity (Scenario A) and relation (risks)
  2. Execute: MATCH (s:SCENARIO {id: "A"})-[rel]->(risk) RETURN risk
  3. Format results as human-readable text
  4. Return to Claude

Claude receives: "Scenario A leaves open R-001 (ATO path blocked). All other P1 risks mitigated."
```

**No Cypher Exposure**

Claude never sees or writes Cypher. MCP server translates:
- Natural questions → Graph queries
- Graph results → Readable summaries
- Relationship changes → Graph mutations

---

## 7. Current Preference vs. Alternatives

| Aspect | Current Preference | Alternative | Tradeoff |
|---|---|---|---|
| **Database** | Neo4j (relationships first-class) | Relational DB (simpler) | Complexity vs. expressiveness |
| **Population** | Manual (controlled, auditable) | Automatic (faster, stale?) | Accuracy vs. effort |
| **Claude Access** | MCP abstraction (natural queries) | Direct Cypher (powerful, complex) | Simplicity vs. power |
| **Scope** | Entity relationship graph (focused) | Whole organization graph (comprehensive, messy) | Clarity vs. completeness |
| **Refresh** | Quarterly (capture learning) | Real-time (always current, overhead) | Insights vs. operational burden |

---

## 8. Open Questions & Future Iterations

1. **Scale:** This schema works for PATH/HAIL. What breaks at 10 convergence decisions? 50?
2. **Automation:** Can we auto-populate from audit logs, ADRs, meeting notes?
3. **Discovery:** How do new team members find relevant nodes ("What decisions involve security?")
4. **Versioning:** When a scenario changes, do we fork or mutate? (Current: mutate + log history)
5. **Privacy:** Do we include stakeholder political positions? (Current preference: yes, with access controls)

---

## 9. Governance & Zero Trust for the Graph

**Who can query?**
- EA team: All queries
- Stakeholders: Queries relevant to them (own positions, decisions affecting them)
- Others: Approved queries only

**Who can write?**
- EA Lead + CDO: Scenario/decision updates
- Automated: Audit logs + approvals recorded
- Stakeholders: Update own positions

**Audit Trail:**
- All mutations logged (what changed, when, who, why)
- Queries logged (who asked what, when)
- Level 2+ content flagged in graph (Protected B decisions tracked carefully)

---

## 10. Success Metrics

✅ **Graph is valuable when:**
- Claude can answer architecture questions from the graph
- We reference prior decisions ("Didn't we decide this for PATH?")
- New team members onboard faster (read graph, not 50 documents)
- We spot patterns ("Why do we always struggle with FinOps?")
- Risk interdependencies become visible

❌ **Graph is overhead when:**
- We spend more time maintaining graph than gaining insights
- Queries return stale information
- No one asks questions the graph can answer

---

## Navigation

This is Part 3 of 7. Read in order:

1. Core Principles & Philosophy
2. Reference Architecture: EA Platform Convergence
3. **Neo4j Knowledge Graph Schema** ← You are here
4. Modular Agent & Skill Components
5. Zero Trust Governance Framework
6. Modularity & Reuse Patterns
7. Architectural Vision Synthesis

**Next Document:** Modular Agent & Skill Components

*Classification: Unclassified / For Internal Use*
