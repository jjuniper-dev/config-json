# Graphics Agent Instruction Set
## HC/PHAC AI Capability Tags — Refreshed Slide Set
### Version 1.0 | April 2026 | EA/TPO Working Reference

---

## Purpose

Redraw the three-slide HC/PHAC AI Capability Tags deck with all identified issues resolved.
The output must be executive-ready, ARB-defensible, and DA11y-compliant.
Do not change any substantive content — only structure, visual treatment, and labeling.

---

## Issues to Resolve (Complete List)

### All Slides

**Issue 1 — Unresolved slide number placeholder**
The breadcrumb bar reads `Slide # · [Context]`. The `#` token was never replaced.
Fix: Replace with the actual slide number. Slide 1 = `1`, Slide 2 = `2`, Slide 3 = `3`.

**Issue 2 — Em dashes throughout**
The design system prohibits em dashes (`—`). They appear in slide titles, column headers,
and body text throughout all three slides.
Fix: Replace every `—` with a colon (`:`) or plain hyphen (`-`) as context requires.
Examples:
- `Health Canada — Regulatory Mandate` → `Health Canada: Regulatory Mandate`
- `LabScan — HAIL Platform` → `LabScan: HAIL Platform`
- `HAIL — Epi Pipelines` → `HAIL: Epi Pipelines`
- `Cluster 8 — Reserved / To Be Confirmed` → `Cluster 8: Reserved / To Be Confirmed`
- `Regulatory service delivery improvement —` (body text lead-in) → use a line break, not em dash

**Issue 3 — Governance tags use wrong color**
The governance tags at the bottom of slides 1 and 2 (Protected B, Canadian data residency,
AIA compliance, PIA compliance, Governed access, Human oversight, Audit trail) are styled
identically to the capability tags. They must be visually distinct.
Fix: Style governance tags using `ENABLEMENT_GREY` (`#8A8FA3`) fill with white text.
Capability tags keep `TEAL_600` (`#5E9EA3`). The governance row must read as a separate layer.

**Issue 4 — HC AI Strategy focus area not labeled**
The slides have no link to the HC AI Strategy priority focus areas. The design system requires
all AI visuals to align to the strategy.
Fix: Add a single strategy alignment label to the header band area of each slide.
- Slide 1 (HC Regulatory Mandate): `HC AI Strategy: Enhance Regulatory Processes and Services`
- Slide 2 (PHAC Surveillance Mandate): `HC AI Strategy: Scale and Strengthen Surveillance`
- Slide 3 (Clusters 8 and 9): No strategy label — omit for this slide.
Style: Small text, `TEXT_SECONDARY` (`#6D6E71`), right-aligned, in the sub-header band.

---

### Slides 1 and 2

**Issue 5 — Uneven tag zone (ragged bottom)**
Columns have different numbers of capability tags. Columns with fewer tags leave large empty
whitespace before the governance footer, creating visual imbalance.
- Slide 1 column counts: PMRA = 4, HPFB = 3, ROEB = 3, HAIL Doc = 3, CANChat = 3
- Slide 2 column counts: FluWatch = 3, LabScan = 3, HAIL Epi = 3, IRIDA = 4, GeoAI = 4
Fix: Set the tag zone to a fixed height. Top-align tags within the zone. Do not stretch tags
to fill space. Let the empty space sit at the bottom of the zone — this is preferable to
misaligned stretching. Add a light `TEAL_200` (`#CDE3E5`) horizontal rule or thin border
below the tag zone to visually close it before the governance footer.

**Issue 6 — Column 4 title wraps to three lines (Slide 1 only)**
"Document classification and triage" wraps to three lines in column 4 of Slide 1 while all
other column titles wrap to two lines. This causes misalignment in the title row.
Fix: Reduce font size in the title zone by 1pt uniformly across all five columns, or reword
to: `Document classification and triage` with forced line break after `classification` to
normalize wrapping.

**Issue 7 — Mixed hyphen style in column headers**
Column 4 Slide 1 uses a plain hyphen (`HAIL - Document Processing`) while all other columns
use em dashes (`LabScan — HAIL Platform`). Per Issue 2, all em dashes must be replaced with
hyphens or colons. After fixing Issue 2, confirm that column 4 Slide 1 is consistent with the
others: use `HAIL: Document Processing` to match the colon convention.

**Issue 8 — No cluster affiliation label**
The slides show program areas (PMRA, HPFB, ROEB, etc.) but do not indicate which capability
cluster each column maps to. This weakens ARB traceability.
Fix: Add a cluster anchor badge to each column header.
- Slide 1: All five columns map to Cluster 1 (Regulatory Intake) or Cluster 6 (Enterprise
  Service Platforms) as noted below. Add a small label beneath the project name in each column:
  - PMRA Active Lifecycle Tool: `Cluster 1`
  - HPFB eSubmission Gateway: `Cluster 1`
  - ROEB Inspection Program: `Cluster 1`
  - HAIL: Document Processing: `Cluster 7`
  - CANChat / M365 Copilot: `Cluster 6`
- Slide 2:
  - FluWatch / Syndromic Surveillance: `Cluster 2`
  - LabScan: HAIL Platform: `Cluster 2`
  - HAIL: Epi Pipelines: `Cluster 3`
  - IRIDA: Genomics Platform: `Cluster 4`
  - HAIL: GeoAI / Climate Intel: `Cluster 2`
Style: Small label, `TEXT_SECONDARY` (`#6D6E71`), italic, below the project name, above the
capability title. Example: `Cluster 1  |  Regulatory Intake`

**Issue 9 — Governance tags overflow in one row**
The seven governance tags (Shared governance, Protected B, Canadian data residency, AIA
compliance, PIA compliance, Governed access, Human oversight, Audit trail) are squeezed into
one horizontal row. At reduced slide widths or lower resolution, this line risks crowding or
overflow.
Fix: Allow the governance tag row to wrap into two rows if needed. The governance footer zone
should have a fixed minimum height of two tag rows. Tags stay left-aligned. Use
`ENABLEMENT_GREY` fill per Issue 3. Remove "Shared governance" as a tag and instead use it
as a section label to the left of the tags — it reads as a category, not a tag value.
Revised structure:
```
[Shared governance]   [Protected B]  [Canadian data residency]  [AIA compliance]  [PIA compliance]
                      [Governed access]  [Human oversight]  [Audit trail]
```
Where `[Shared governance]` is a plain text label, not a pill.

---

### Slide 3

**Issue 10 — "CAPABILITIES IN 3a / 3b" label references internal shorthand**
The section heading "CAPABILITIES IN 3a / 3b THAT MAY DEPEND ON THIS CLUSTER" uses internal
shorthand (`3a / 3b`) that is not self-explanatory to an external ARB audience.
Fix: Replace with: `CANDIDATE DEPENDENCIES FROM HC AND PHAC MANDATE SLIDES`

**Issue 11 — Em dashes in bullet lead-ins**
Bullet items on Slide 3 use em dashes to introduce the explanation:
`Regulatory service delivery improvement — External stakeholder-facing...`
Fix: Replace em dash with period and line break, or reformat as:
**Regulatory service delivery improvement.** External stakeholder-facing capabilities...
Do not use em dashes.

**Issue 12 — Cluster status bar overflow**
The nine cluster pills at the bottom of Slide 3 are too tight. "6 Enterprise Svc" breaks
across two lines because the pill is too narrow.
Fix: Reduce font size inside pills to 10pt. Expand pill widths proportionally. Abbreviate
as needed:
- `1 Reg. Intake` stays
- `6 Enterprise Svc` → `6 Ent. Services`
Ensure all nine pills fit in one row without line breaks inside any pill.

**Issue 13 — Open question boxes use dashed borders without accessible label**
The dashed-border boxes for open questions are visually distinct but rely on the dashed border
alone to signal "this is a question" — meaning is conveyed by style, not label.
Fix: Add a bold label `Open question:` as the first element inside each box. The dashed border
may remain as secondary visual reinforcement, but the label must carry the meaning.
This is already partially done in the current version (`Open question` appears as inline text),
but confirm it is present as a labeled element, not just styled body text.

**Issue 14 — "Definition pending" repeated identically in both columns**
Both cluster columns display the identical heading "Definition pending" with no differentiation.
This reads like a copy error.
Fix: Retain "Definition pending" but add a disambiguation sub-label:
- Cluster 8: `Definition pending — HC scope under review`
- Cluster 9: `Definition pending — PHAC science mandate under review`
Style: Subtitle font, `TEXT_SECONDARY`, below the main heading.

---

## Design System Reference

Apply the following tokens exactly. No substitutions.

| Token | Hex | Application |
|---|---|---|
| TEAL_900 | `#2F6F73` | Header band background, column dividers |
| TEAL_600 | `#5E9EA3` | Capability tag pills |
| TEAL_200 | `#CDE3E5` | Section container backgrounds |
| ENABLEMENT_GREY | `#8A8FA3` | Governance tag pills, open question boxes |
| BACKGROUND | `#F5F7F7` | Slide background |
| TEXT_PRIMARY | `#4A4A4A` | Body text, descriptions |
| TEXT_SECONDARY | `#6D6E71` | Project name labels, cluster badges, footers |
| AI_GREEN | `#A6CE39` | AI capability tag border accent only — not fill |
| WHITE | `#FFFFFF` | Text on TEAL_900 and ENABLEMENT_GREY fills |

**Color rules to enforce:**
- Maximum 2 teal tones per slide
- Governance elements (ENABLEMENT_GREY) must be visually isolated from capability elements (TEAL_600)
- AI_GREEN may be used as a border or left-edge accent on capability tag pills only — never as fill
- Do not use AI_GREEN on any structural or governance element

---

## Typography

| Element | Font | Size | Weight | Color |
|---|---|---|---|---|
| Slide title | Arial or Calibri | 28pt | Bold | WHITE on TEAL_900 |
| Sub-title (mandate description) | Arial or Calibri | 14pt | Regular | WHITE |
| Disclaimer italic line | Arial or Calibri | 11pt | Italic | TEAL_200 |
| Breadcrumb label | Arial or Calibri | 10pt | Regular | TEAL_200 |
| Column project name | Arial or Calibri | 11pt | Regular | TEXT_SECONDARY |
| Cluster badge | Arial or Calibri | 10pt | Italic | TEXT_SECONDARY |
| Column capability title | Arial or Calibri | 18pt | Bold | TEXT_PRIMARY |
| Column description | Arial or Calibri | 12pt | Regular | TEXT_PRIMARY |
| Capability tag pill text | Arial or Calibri | 11pt | Semi-bold | WHITE |
| Governance tag pill text | Arial or Calibri | 11pt | Regular | WHITE |
| Section label (CANDIDATE DEPENDENCIES) | Arial or Calibri | 10pt | Bold | TEXT_SECONDARY |
| Bullet body text (Slide 3) | Arial or Calibri | 12pt | Regular | TEXT_PRIMARY |
| Cluster status pill text | Arial or Calibri | 10pt | Regular | WHITE |
| Footer text | Arial or Calibri | 11pt | Regular | TEXT_SECONDARY |
| HC AI Strategy label | Arial or Calibri | 10pt | Regular | TEXT_SECONDARY |

**Minimum body text: 18pt for all primary content zones. Supporting labels minimum 10pt.**

---

## Layout

### Slides 1 and 2 (five-column program area template)

```
+------------------------------------------------------------------+
| BREADCRUMB: [Slide N] · [Organization]      [Classification]     |  ← TEAL_900, 10pt
+------------------------------------------------------------------+
| TITLE: [Organization]: [Mandate]            [HC AI Strategy label]|  ← TEAL_900
| SUBTITLE: AI capability tags by program area...                  |
| ITALIC DISCLAIMER: [Tags drawn from / Includes draft...]         |
+--+----+----+----+----+----+--------------------------------------+
|  | C1 | C2 | C3 | C4 | C5 |                                      |
|  +----+----+----+----+----+                                      |
|  | Project name (TEXT_SECONDARY)                                 |
|  | Cluster badge (italic, TEXT_SECONDARY)                        |  ← per column
|  | Capability title (bold, 18pt)                                 |
|  +----+----+----+----+----+                                      |
|  | Description text (12pt, TEXT_PRIMARY)                         |
|  +----+----+----+----+----+                                      |
|  | Capability tag zone (fixed height, top-aligned)               |
|  | [Tag 1] [Tag 2] [Tag 3] [Tag 4]  ← TEAL_600 pills            |
|  +----+----+----+----+----+                                      |
|  ← thin TEAL_200 horizontal rule closing tag zone →              |
+--+----+----+----+----+----+--------------------------------------+
| Shared governance   [Protected B] [Canadian data residency]       |  ← ENABLEMENT_GREY
|                     [AIA compliance] [PIA compliance]             |
|                     [Governed access] [Human oversight]           |
|                     [Audit trail]                                 |
+------------------------------------------------------------------+
| Unclassified / Non classifié    EA/TPO interpretation · DTB      |  ← footer
+------------------------------------------------------------------+
```

**Column separators:** Thin vertical line, TEAL_200 or TEAL_600, 1pt weight. Not a full
TEAL_900 band — that is for the header only.

### Slide 3 (two-column cluster placeholder template)

```
+------------------------------------------------------------------+
| BREADCRUMB: 3 · Capability Clusters 8 and 9   [Classification]  |
+------------------------------------------------------------------+
| TITLE: Two Clusters Remain. Their Dependencies Do Not.           |  ← TEAL_900
| SUBTITLE: Clusters 8 and 9 are reserved...                       |
| ITALIC DISCLAIMER: ...Dependencies below are EA interpretations. |
+--+---------------------------------+----------------------------++
|  | Cluster 8: Reserved / To Be    | Cluster 9: Reserved /       |
|  | Confirmed [pill]               | To Be Confirmed [pill]      |
|  |                                |                             |
|  | Definition pending             | Definition pending          |
|  | HC scope under review          | PHAC science mandate...     |
|  |                                |                             |
|  | Scope description (12pt)       | Scope description (12pt)    |
|  +--------------------------------+-----------------------------+
|  | CANDIDATE DEPENDENCIES...      | CANDIDATE DEPENDENCIES...   |
|  | Bold item. Description text.   | Bold item. Description text.|
|  | Bold item. Description text.   | Bold item. Description text.|
|  | Bold item. Description text.   | Bold item. Description text.|
|  +--------------------------------+-----------------------------+
|  | [Open question: dashed box]     | [Open question: dashed box]|
+--+--------------------------------+-----------------------------++
| Cluster map status:                                              |
| [1 Reg. Intake][2 Surveillance][3 Data Mgmt][4 Sci. Computing]  |
| [5 Cybersecurity][6 Ent. Services][7 Infrastructure]            |
| [8 Reserved][9 Reserved]                                        |
+------------------------------------------------------------------+
| Unclassified / Non classifié    EA/TPO interpretation · DTB      |
+------------------------------------------------------------------+
```

---

## Accessibility Checklist (DA11y)

Apply the following before declaring any slide complete:

- [ ] All tag pill text: minimum 4.5:1 contrast ratio against pill background
  - WHITE on TEAL_600 (#5E9EA3): verify passes 4.5:1
  - WHITE on ENABLEMENT_GREY (#8A8FA3): verify passes 4.5:1
- [ ] All body text: minimum 4.5:1 against slide background (#F5F7F7)
- [ ] TEXT_SECONDARY (#6D6E71) on BACKGROUND (#F5F7F7): verify passes 4.5:1
- [ ] No meaning conveyed by color alone — all tags labeled, all sections labeled
- [ ] Logical reading order: left to right, top to bottom in screen reader flow
- [ ] Alt text required on all non-text elements. Tag: source = AI-generated. Block delivery
  until human-reviewed flag is set.
- [ ] No merged table cells in any tabular element
- [ ] Cluster status pills (Slide 3): each pill text minimum 10pt, single line, no wrapping

### Contrast advisory (precomputed)

| Foreground | Background | Estimated ratio | Pass/Fail |
|---|---|---|---|
| WHITE `#FFFFFF` | TEAL_900 `#2F6F73` | ~6.8:1 | PASS |
| WHITE `#FFFFFF` | TEAL_600 `#5E9EA3` | ~3.2:1 | BORDERLINE — use bold text or adjust TEAL_600 |
| WHITE `#FFFFFF` | ENABLEMENT_GREY `#8A8FA3` | ~3.1:1 | BORDERLINE — use bold text |
| TEXT_PRIMARY `#4A4A4A` | BACKGROUND `#F5F7F7` | ~7.5:1 | PASS |
| TEXT_SECONDARY `#6D6E71` | BACKGROUND `#F5F7F7` | ~4.5:1 | MARGINAL — use only for non-critical labels |

**If TEAL_600 fails contrast at standard weight, either:**
(a) darken TEAL_600 to `#4E8A8F` for pill fills only, or
(b) use bold weight for all pill text.
Do not change the design token — adjust the text weight.

---

## Accessibility State Machine

Each slide must pass through these states before delivery. Do not advance without meeting
the stated condition.

| State | Condition |
|---|---|
| Draft | All content placed, structure complete |
| Validated | Color, contrast, and layout rules confirmed per checklist |
| Human reviewed | Alt text reviewed and approved by a human |
| Compliant | All DA11y requirements met |
| Delivered | Approved for distribution |

---

## Content Reference (Do Not Modify)

The following content is canonical. Copy exactly — do not paraphrase, reorder, or omit.

### Slide 1 — HC Regulatory Mandate (five columns)

| Column | Project | Capability Title | Description |
|---|---|---|---|
| 1 | PMRA Active Lifecycle Tool | Regulatory intelligence and case analysis | Extract entities and relationships from regulatory submissions to support case officer analysis and decision-making. |
| 2 | HPFB eSubmission Gateway | Drug submission and review processing | Automate intake validation, completeness checks, and routing of drug dossiers to reduce manual processing time. |
| 3 | ROEB Inspection Program | Inspection workflow automation | Route and prioritize inspection cases based on risk signals. Automate task assignment and SLA tracking. |
| 4 | HAIL: Document Processing | Document classification and triage | Automatically categorize documents by type and regulatory pathway. Surface key data for reviewers before manual review. |
| 5 | CANChat / M365 Copilot | Regulatory service delivery improvement | AI-assisted self-service and knowledge retrieval to improve response consistency for external stakeholders and staff. |

| Column | Capability Tags |
|---|---|
| 1 | Information Extraction, Named Entity Recognition, Risk Scoring, Decision Support |
| 2 | Document Classification, Intelligent Triage, Intelligent Automation |
| 3 | Intelligent Automation, Risk Scoring, Decision Support |
| 4 | Document Classification, Intelligent Triage, Text Summarisation |
| 5 | RAG, Virtual Assistant, Intelligent Automation |

Governance tags: Protected B, Canadian data residency, AIA compliance, PIA compliance, Governed access, Human oversight, Audit trail

### Slide 2 — PHAC Surveillance Mandate (five columns)

| Column | Project | Capability Title | Description |
|---|---|---|---|
| 1 | FluWatch / Syndromic Surveillance | Public health signal detection | Identify emerging signals from structured and unstructured sources including syndromic feeds, adverse event reports, and news. |
| 2 | LabScan: HAIL Platform | Outbreak detection and response analytics | Apply predictive models to detect outbreak conditions early. Generate scenario projections to support response decisions. |
| 3 | HAIL: Epi Pipelines | Epidemiological data pipeline processing | Automate ingestion, transformation, and quality checks for epidemiological datasets. Maintain lineage for audit. |
| 4 | IRIDA: Genomics Platform | Scientific research assistance | Support researchers with literature retrieval, synthesis, and model development for genomic and public health studies. |
| 5 | HAIL: GeoAI / Climate Intel | Real-time surveillance and GeoAI | Combine real-time streams with geospatial analysis to detect location-based signals and support outbreak mapping. |

| Column | Capability Tags |
|---|---|
| 1 | NLP Signal Extraction, Anomaly Detection, Named Entity Recognition |
| 2 | Predictive Analytics, Anomaly Detection, Forecasting |
| 3 | Automated Data Lineage, ML Model Training, Predictive Modelling |
| 4 | ML Model Training, Genomic Analysis, RAG |
| 5 | GeoAI, Anomaly Detection, Predictive Analytics, Forecasting |

Governance tags: Protected B, Canadian data residency, AIA compliance, PIA compliance, Governed access, Human oversight, Audit trail

### Slide 3 — Clusters 8 and 9

**Title:** Two Clusters Remain. Their Dependencies Do Not.

**Subtitle:** Clusters 8 and 9 are reserved pending confirmation from the v2.3 workbook.
Capabilities mapped in slides 1 and 2 already point to what these clusters will define.

**Disclaimer (italic):** Clusters 8 and 9 are placeholders. Do not assign AI capability tags
without confirming the source in the v2.3 workbook. Dependencies below are EA interpretations.

**Cluster 8 column:**
- Pill label: `Cluster 8: Reserved / To Be Confirmed`
- Heading: `Definition pending`
- Sub-heading: `HC scope under review`
- Scope text: Scope to be confirmed from the finalised Cluster Dictionary and v2.3 workbook.
  Candidate scope includes functions not yet covered by Clusters 1 through 7.
- Section label: `CANDIDATE DEPENDENCIES FROM HC AND PHAC MANDATE SLIDES`
- Items:
  1. **Regulatory service delivery improvement.** External stakeholder-facing capabilities may need a distinct cluster if citizen service delivery is scoped separately from enterprise service platforms.
  2. **Communications and public engagement.** Translation, accessibility, and public-facing AI may belong here if GC public communications is treated as a standalone cluster.
  3. **Legal and policy intelligence.** If policy advisory functions are treated as distinct from regulatory intake processing, this is the candidate home.
- Open question: Is Cluster 8 an HC-specific function not present in PHAC's mandate, or a shared enterprise capability not yet surfaced in the 63-proposal review?

**Cluster 9 column:**
- Pill label: `Cluster 9: Reserved / To Be Confirmed`
- Heading: `Definition pending`
- Sub-heading: `PHAC science mandate under review`
- Scope text: Scope to be confirmed from the finalised Cluster Dictionary and v2.3 workbook.
  Candidate scope may reflect PHAC's distinct science mandate not fully captured in Clusters 2 or 4.
- Section label: `CANDIDATE DEPENDENCIES FROM HC AND PHAC MANDATE SLIDES`
- Items:
  1. **Scientific research and genomics.** PHAC's science mandate may need a dedicated cluster if Scientific Computing is insufficiently granular for laboratory informatics and HPC workloads.
  2. **International health and border surveillance.** PHAC point-of-entry surveillance, quarantine, and international health data exchange may constitute a standalone cluster.
  3. **Indigenous health data sovereignty.** If HC/PHAC formalises First Nations, Inuit, and Metis health data governance as a distinct program area, this is the most likely home.
- Open question: Does Cluster 9 capture PHAC's science and epidemiology mandate that falls outside Cluster 2 (Surveillance) and Cluster 4 (Scientific Computing)?

**Cluster map status row (all nine clusters):**
1 Reg. Intake | 2 Surveillance | 3 Data Mgmt | 4 Sci. Computing | 5 Cybersecurity
| 6 Ent. Services | 7 Infrastructure | 8 Reserved | 9 Reserved

Clusters 8 and 9 pills: style with dashed or muted border to indicate placeholder status.
Clusters 1 through 7: solid TEAL_600 fill.

---

## Mandatory Footer (All Slides)

Left: `Unclassified / Non classifié` — minimum 11pt, TEXT_SECONDARY
Right: `EA/TPO interpretation  ·  Digital Transformation Branch` — minimum 11pt, TEXT_SECONDARY

This footer must appear on every slide. It is required by EA visual design standards.
The footer signals that this deck represents EA team working interpretation, not citeable GC policy.

---

## What to Preserve

- All five-column structure on slides 1 and 2
- All tag content — do not add or remove any tag
- Disclaimer italic lines — keep verbatim
- Cluster 8 and 9 placeholder language — do not speculate or fill in definitions
- Three-item candidate dependency lists — do not expand or reduce
- Open question wording — these are load-bearing governance questions, not decorative text

---

## What Not to Do

- Do not introduce icons — none appear in the current version; do not add them
- Do not add decorative borders or shadow effects
- Do not use AI_GREEN as a fill color on any element
- Do not conflate capability tags with governance tags — they are separate visual layers
- Do not populate Clusters 8 and 9 with definitions or AI capability tags
- Do not reorder capability tags within columns
- Do not change the slide count — three slides only

---

*This instruction set is an EA/TPO working reference.*
*Classification: Unclassified / Non classifié*
