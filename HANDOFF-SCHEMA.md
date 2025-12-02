# Handoff Schema
## Shared Format Definitions for Pipeline Stages

---

# PURPOSE

This schema defines the standardized format for passing data between pipeline stages. Each stage outputs a HANDOFF PACKAGE that the next stage consumes as input.

**Key Principle**: Information should flow through the pipeline without loss. Metadata established in Stage 1 (Q-IDs, confidence levels, source tiers) must be preserved and accessible through Stage 5.

**Pipeline Structure**: 5 stages with 4 handoffs + 1 final deliverable package

```
P1 ──STAGE_1_HANDOFF──▶ P2 ──STAGE_2_HANDOFF──▶ P3 ──STAGE_3_HANDOFF──▶ P4 ──STAGE_4_HANDOFF──▶ P5 ──FINAL_DELIVERABLES
```

---

# STAGE 1 HANDOFF PACKAGE

Output by: `Prompt 1 - Deep Research`
Consumed by: `Prompt 2 - Executive Summary Creation`

```markdown
<<<STAGE_1_HANDOFF>>>

## Pipeline Metadata
| Field | Value |
|-------|-------|
| Stage | 1 - Deep Research |
| Executed | [Date/Time] |
| Research Depth | [Brief / Standard / Comprehensive] |
| Data Freshness | [Date of most recent source] |

## Research Brief (Original)
[Verbatim copy of user's original research brief]

## Research Questions Index
| Q-ID | Question | Status | Confidence |
|------|----------|--------|------------|
| Q1 | [Question] | ✅/⚠️/❌ | High/Med/Low |
| Q1.1 | [Sub-question] | ✅/⚠️/❌ | High/Med/Low |
| Q2 | [Question] | ✅/⚠️/❌ | High/Med/Low |

## Findings Summary
| F-ID | Finding Title | Q-Ref | Confidence | Tier |
|------|---------------|-------|------------|------|
| F1 | [Title] | Q1 | High | 1 |
| F2 | [Title] | Q1.2 | Medium | 2 |
| F3 | [Title] | Q2 | Low | 3 |

## Source Tier Summary
| Tier | Count | Key Sources |
|------|-------|-------------|
| Tier 1 | [#] | [Names] |
| Tier 2 | [#] | [Names] |
| Tier 3 | [#] | [Names] |
| Tier 4 | [#] | [Names] |

## Abbreviation Seed Table
| Full Name | Suggested Abbrev |
|-----------|------------------|
| [Source name] | [Abbrev] |

## Key Statistics
| Statistic | Value | Source | Tier |
|-----------|-------|--------|------|
| [Stat] | [Value] | [Source] | [1-4] |

## Named Entities
| Entity | Type | Relevance |
|--------|------|-----------|
| [Name] | Regulator/Company/Framework | [Role in research] |

## Conflicts Identified
| Topic | Source A vs Source B | Nature | Resolved? |
|-------|---------------------|--------|-----------|
| [Topic] | [A] vs [B] | [Type] | Yes/No |

*If none: "No material conflicts identified."*

## Gaps & Limitations
| Gap ID | Q-Ref | Description | Impact |
|--------|-------|-------------|--------|
| G1 | [Q-ID] | [Gap description] | [Impact on conclusions] |

## Flags for Next Stage
- [ ] [Any warnings, e.g., "Q3 has only Tier 4 sources"]
- [ ] [Any recommendations, e.g., "Consider emphasizing F2 - strongest evidence"]

## Full Research Document
[Complete Stage 1 deliverable — all sections and appendices]

<<<END_STAGE_1_HANDOFF>>>
```

---

# STAGE 2 HANDOFF PACKAGE

Output by: `Prompt 2 - Executive Summary Creation`
Consumed by: `Prompt 3 - Slide Presentation Outline`

```markdown
<<<STAGE_2_HANDOFF>>>

## Pipeline Metadata
| Field | Value |
|-------|-------|
| Stage | 2 - Executive Summary |
| Executed | [Date/Time] |
| Summary Density | [Sparse / Moderate / Rich] |
| Word Count | [#] |
| Sufficiency | [Sufficient / Marginal / Insufficient] |

## Inherited from Stage 1
| Field | Value |
|-------|-------|
| Research Depth | [from Stage 1] |
| Data Freshness | [from Stage 1] |
| Research Date | [from Stage 1] |

## Research Brief (Original)
[Carried forward from Stage 1]

## Findings Carried Forward
| F-ID | Finding | Q-Ref | Confidence | Used in Summary? | Summary Location |
|------|---------|-------|------------|------------------|------------------|
| F1 | [Title] | Q1 | High | ✅ | [Section/paragraph] |
| F2 | [Title] | Q1.2 | Medium | ✅ | [Section/paragraph] |
| F3 | [Title] | Q2 | Low | ⚠️ (flagged) | [Section/paragraph] |

## Branded Concepts
| Concept | Source Evidence | Definition |
|---------|-----------------|------------|
| [Concept name] | [F-ID or data point] | [Brief definition] |

## Narrative Elements
| Element | Content |
|---------|---------|
| Core Thesis | [One sentence] |
| Opening Strategy | [Strategy name]: [First line of opening] |
| Narrative Arc | [Pattern used: Transformation/Collision/Hidden/Countdown/Mosaic] |
| Key Tension | [Primary conflict or "so what"] |
| Closing Strategy | [Strategy name]: [Key closing statement] |

## Citation Abbreviation Table
| Abbreviation | Full Name | Tier | First Used |
|--------------|-----------|------|------------|
| [Abbrev] | [Full source name] | [1-4] | [Section] |

## Stakeholder Implications
| Stakeholder | Key Implication | Urgency | Action Required |
|-------------|-----------------|---------|-----------------|
| [Group] | [Implication] | High/Med/Low | [What they should do] |

## Statistics Highlighted
| Statistic | Value | Context | Visual Potential |
|-----------|-------|---------|------------------|
| [Description] | [Number] | [Why it matters] | [Chart type suggestion] |

## Confidence Inheritance
| Claim Category | Confidence | Notes |
|----------------|------------|-------|
| Regulatory status | [H/M/L] | [Any caveats] |
| Market data | [H/M/L] | [Any caveats] |
| Projections | [H/M/L] | [Any caveats] |

## Source Conflicts (Carried Forward)
[From Stage 1, plus any new conflicts identified during synthesis]

## Gaps Acknowledged
[From Stage 1, noting which were addressed vs. remain open]

## Complexity Indicator for Stage 3
| Factor | Assessment |
|--------|------------|
| Distinct findings synthesized | [#] |
| Stakeholder groups addressed | [#] |
| Geographic scope | Single / Multi-jurisdiction |
| Recommended presentation complexity | Low / Medium / High |
| Suggested slide count | [8-10 / 10-12 / 12-15] |

## Flags for Next Stage
- [ ] [Presentation-relevant notes, e.g., "Strong visual opportunity: market share data"]
- [ ] [Warnings, e.g., "Closing requires callback to opening statistic"]

## Full Executive Summary
[Complete Stage 2 deliverable — summary + process notes]

<<<END_STAGE_2_HANDOFF>>>
```

---

# STAGE 3 HANDOFF PACKAGE

Output by: `Prompt 3 - Slide Presentation Outline`
Consumed by: `Prompt 4 - Slide Design Specification`

```markdown
<<<STAGE_3_HANDOFF>>>

## Pipeline Metadata
| Field | Value |
|-------|-------|
| Stage | 3 - Presentation Outline |
| Executed | [Date/Time] |
| Presentation Complexity | [Low / Medium / High] |
| Main Slides | [#] |
| Appendix Slides | [#] |
| Framework | [Pyramid / SCR / Transformation / Countdown / Evidence Cascade] |
| Duration | [15 / 20 / 30 min] |

## Inherited from Previous Stages
| Field | Value | Source |
|-------|-------|--------|
| Research Depth | [Brief/Standard/Comprehensive] | Stage 1 |
| Data Freshness | [Date] | Stage 1 |
| Summary Density | [Sparse/Moderate/Rich] | Stage 2 |
| Core Thesis | [One sentence] | Stage 2 |

## Research Brief (Original)
[Carried forward from Stage 1]

## Governing Thought
> "[Single sentence ≤25 words capturing entire argument]"

## Headline Sequence
| Slide # | Title (Assertion) | Type | F-Refs |
|---------|-------------------|------|--------|
| 1 | [Title] | Setup | — |
| 2 | [Title] | Evidence | F1 |
| 3 | [Title] | Evidence | F2, F3 |
| ... | ... | ... | ... |

## Slide Inventory
| Slide # | Title | Type | Content Summary | Visual Type | Speaker Note Summary |
|---------|-------|------|-----------------|-------------|---------------------|
| 1 | [Title] | Setup | [2-3 bullets summary] | [Chart/Image/Text] | [Key speaking points] |
| 2 | [Title] | Evidence | [2-3 bullets summary] | [Chart type] | [Key speaking points] |
| ... | ... | ... | ... | ... | ... |

## Visual Elements Specified
| Slide # | Visual Type | Data Points | Recommended Chart |
|---------|-------------|-------------|-------------------|
| 3 | Data visualization | [Stats used] | Bar chart |
| 5 | Comparison | [Entities compared] | Table |
| 7 | Timeline | [Events] | Gantt/Timeline |

## Appendix Slides
| ID | Title | Trigger Question | Content Summary |
|----|-------|------------------|-----------------|
| A1 | [Title] | "[Question]" | [Summary] |
| A2 | [Title] | "[Question]" | [Summary] |

## Branded Concepts (Carried Forward)
| Concept | Used in Slide # | As |
|---------|-----------------|-----|
| [Concept] | 4, 7 | Section header |

## Confidence by Slide
| Slide # | Claims | Confidence | Speaker Note Flag |
|---------|--------|------------|-------------------|
| 3 | [Claim summary] | High | None |
| 5 | [Claim summary] | Low | [CONFIDENCE: LOW] |

## Citation Abbreviation Table (Carried Forward)
| Abbreviation | Full Name | Tier | Used in Slides |
|--------------|-----------|------|----------------|
| [Abbrev] | [Full name] | [1-4] | 2, 4, 7 |

## Traceability Summary
| Q-ID | F-ID | Summary Section | Slide # |
|------|------|-----------------|---------|
| Q1 | F1 | [Section] | 2, 3 |
| Q1.2 | F2 | [Section] | 4 |

## Flags for Stage 4
[Recommendations for JSON specification and slide design]
- [ ] [e.g., "Slide 3 needs bar chart with 4 data points"]
- [ ] [e.g., "Slide 7 timeline spans 2020-2025"]
- [ ] [e.g., "Consider dark theme for executive audience"]
- [ ] [e.g., "Appendix A1 likely to be triggered - prepare detailed version"]

## Full Presentation Outline
[Complete Stage 3 deliverable — all slides with full content, speaker notes, and process notes]

<<<END_STAGE_3_HANDOFF>>>
```

---

# STAGE 4 HANDOFF PACKAGE

Output by: `Prompt 4 - Slide Design Specification`
Consumed by: `Prompt 5 - Slide Generation (React Artifact)`

```markdown
<<<STAGE_4_HANDOFF>>>

## Pipeline Metadata
| Field | Value |
|-------|-------|
| Stage | 4 - Slide Design Specification |
| Executed | [Date/Time] |
| JSON Schema Version | 1.0 |
| Total Slides | [#] main + [#] appendix |
| Design System | [Theme name] |

## Inherited from Previous Stages
| Field | Value | Source |
|-------|-------|--------|
| Research Depth | [Brief/Standard/Comprehensive] | Stage 1 |
| Data Freshness | [Date] | Stage 1 |
| Summary Density | [Sparse/Moderate/Rich] | Stage 2 |
| Presentation Complexity | [Low/Medium/High] | Stage 3 |
| Framework | [Framework name] | Stage 3 |
| Governing Thought | [One sentence] | Stage 3 |

## Research Brief (Original)
[Carried forward from Stage 1]

## Design System Summary
| Element | Specification |
|---------|---------------|
| Primary Color | [Hex code] |
| Secondary Color | [Hex code] |
| Accent Color | [Hex code] |
| Title Font | [Font name, size] |
| Body Font | [Font name, size] |
| Layout Grid | [12-column / other] |

## Content Density Versions
[Created via Chain of Density process]
| Slide # | Verbose | Standard | Dense |
|---------|---------|----------|-------|
| 2 | [Full text] | [Condensed] | [Minimal] |
| 3 | [Full text] | [Condensed] | [Minimal] |

## Layout Template Assignments
| Slide # | Template | Rationale (CoT) |
|---------|----------|-----------------|
| 1 | title_centered | Opening slide, single focus |
| 2 | content_visual_split | Data point with chart |
| 3 | chart_focus | Complex data, needs space |

## Chart Specifications
| Slide # | Chart Type | Data Series | Labels | Colors |
|---------|------------|-------------|--------|--------|
| 3 | Bar (horizontal) | [Series names] | [X/Y labels] | [Color assignments] |
| 5 | Line (multi) | [Series names] | [X/Y labels] | [Color assignments] |

## JSON Specification
[Complete JSON structure — see full format below]

## Validation Results
| Check | Status |
|-------|--------|
| Schema compliance | ✅ Pass |
| Color accessibility | ✅ Pass |
| Content density | ✅ Pass |
| Chart data completeness | ✅ Pass |
| Traceability preserved | ✅ Pass |

## Flags for Stage 5
- [ ] [e.g., "PowerPoint: use SmartArt for slide 4"]
- [ ] [e.g., "Google Slides: custom color theme needed"]
- [ ] [e.g., "Keynote: magic move transition for slide 6-7"]
- [ ] [e.g., "Animation: build bullets sequentially on slide 8"]

## Full JSON Specification
```json
{
  "presentation": { ... }
}
```
[Complete JSON output]

<<<END_STAGE_4_HANDOFF>>>
```

---

# FINAL DELIVERABLES PACKAGE

Output by: `Prompt 5 - Slide Generation (React Artifact)`
This is the terminal output — no further handoff needed.

**New in v2.1**: Stage 5 now outputs a React artifact that provides:
- Live slide preview in Claude.ai browser
- Download button generating real .pptx file via PptxGenJS
- Entirely client-side — no Python, no local setup required

```markdown
<<<FINAL_DELIVERABLES>>>

# PIPELINE COMPLETE

## Research Topic
[Original research brief - carried through all stages]

## Pipeline Execution Summary
| Stage | Status | Key Metrics |
|-------|--------|-------------|
| 1 - Deep Research | ✅ Complete | [X] findings, [Y] sources across [Z] tiers |
| 2 - Executive Summary | ✅ Complete | [X] words, [Density] density |
| 3 - Presentation Outline | ✅ Complete | [X] main slides + [Y] appendix |
| 4 - Slide Design Spec | ✅ Complete | JSON v1.0, [X] layouts |
| 5 - React Artifact | ✅ Complete | Preview + PPTX export ready |

## Cumulative Metadata
| Field | Value |
|-------|-------|
| Research Depth | [Brief/Standard/Comprehensive] |
| Summary Density | [Sparse/Moderate/Rich] |
| Presentation Complexity | [Low/Medium/High] |
| Total Research Questions | [#] |
| Total Findings | [#] |
| Total Sources | [#] by tier: T1=[#], T2=[#], T3=[#], T4=[#] |
| Data Freshness | [Date of most recent source] |
| JSON Schema Version | 1.0 |
| Pipeline Executed | [Date] |

---

## DELIVERABLE 1: Raw Research
**Location**: See Stage 1 output above (not duplicated to conserve context)

**Key Sections**:
- Executive Summary: Section 1
- Research Questions: Section 3A
- Detailed Findings: Section 4
- Source Documentation: Appendix A

---

## DELIVERABLE 2: Executive Summary
**Location**: See Stage 2 output above (not duplicated to conserve context)

**Key Elements**:
- Core Thesis: [Single sentence]
- Narrative Arc: [Pattern used]
- Word Count: [#]

---

## DELIVERABLE 3: Presentation Outline
**Location**: See Stage 3 output above (not duplicated to conserve context)

**Key Elements**:
- Governing Thought: [Single sentence]
- Framework: [Pattern used]
- Slide Count: [#] main + [#] appendix

---

## DELIVERABLE 4: JSON Slide Specification
**Location**: See Stage 4 output above (not duplicated to conserve context)

**Key Elements**:
- Schema Version: 1.0
- Design System: [Theme summary]
- Layout Templates: [Count]

---

## DELIVERABLE 5: React Artifact
**The artifact code IS Deliverable 5**

**Features**:
- ✅ Live slide preview in browser
- ✅ Navigation controls (prev/next, slide counter)
- ✅ Download button generating real .pptx file
- ✅ Design system faithfully rendered
- ✅ Charts rendered (SVG preview, native PPTX charts)
- ✅ Speaker notes included in export

**Usage Instructions**:
1. The artifact renders automatically in Claude.ai
2. Use arrow buttons or keyboard to navigate slides
3. Click "Download PPTX" to save presentation
4. Open .pptx in PowerPoint, Keynote, or Google Slides

---

## APPENDIX: Master Source List

**Tier 1 (Regulatory/Official)**:
| Abbreviation | Full Name | Used In Stages |
|--------------|-----------|----------------|
| [Abbrev] | [Full name] | 1, 2, 3, 4, 5 |

**Tier 2-4**: [Similar format]

---

## APPENDIX: Full Traceability Matrix

| Q-ID | F-ID | Confidence | Summary Section | Slide # | JSON Element |
|------|------|------------|-----------------|---------|--------------|
| Q1 | F1 | High | [Section] | 3 | slides[2] |
| Q1.1 | F2 | Medium | [Section] | 4, 5 | slides[3], slides[4] |
| Q1.2 | F3 | Low | [Section] | 6 | slides[5] |
| Q2 | F4 | High | [Section] | 7 | slides[6] |

---

## USAGE NOTES

### For Raw Research (Deliverable 1)
- Complete reference document with full source citations
- Use for due diligence, detailed questions, or audit trail

### For Executive Summary (Deliverable 2)
- Standalone 2-4 page document for distribution
- Can be shared without presentation

### For Presentation Outline (Deliverable 3)
- Detailed slide-by-slide guide with speaker notes
- Use for presentation preparation and rehearsal

### For JSON Specification (Deliverable 4)
- Machine-readable format for slide generation tools
- Can be imported into: Gamma, Beautiful.ai, custom tools

### For React Artifact (Deliverable 5)
- **Preview**: Artifact auto-renders in Claude.ai conversation
- **Navigate**: Click arrows or use keyboard (←/→)
- **Download**: Click button to generate .pptx
- **Edit**: Copy artifact code to modify styling
- **Compatibility**: .pptx works in PowerPoint 2016+, Keynote, Google Slides

**Troubleshooting**:
- If download fails, try refreshing the artifact
- Charts may render slightly differently in PowerPoint vs preview
- For custom fonts, install fonts on local system before opening .pptx

## Data Freshness Warning
*Research conducted [date]. Data current as of [data freshness date]. For rapidly evolving topics, validate key statistics before presentation.*

<<<END_FINAL_DELIVERABLES>>>
```

---

# CROSS-STAGE FIELD MAPPINGS

## Consistent Terminology

| Concept | Stage 1 | Stage 2 | Stage 3 | Stage 4 | Stage 5 |
|---------|---------|---------|---------|---------|---------|
| Research questions | Q-ID | Q-Ref | Q-Ref | Q-Ref | Q-Ref |
| Findings | F[#] | F[#] | F-Refs | F-Refs | F-Refs |
| Confidence | High/Med/Low/Spec | High/Med/Low | High/Med/Low | Preserved | Preserved |
| Source authority | Tier 1-5 | Tier 1-4 | Footnotes | JSON field | Footnotes |
| Inference marker | `[INFERENCE]` | `[INFERENCE]` | Speaker notes | JSON field | Slide notes |

## Confidence Level Definitions (Universal)

| Level | Definition | Evidence Standard |
|-------|------------|-------------------|
| **High** | Well-established fact | 2+ Tier 1-2 sources OR 1 unambiguous Tier 1 |
| **Medium** | Likely accurate, some uncertainty | 1 Tier 1-2 OR multiple Tier 3 in agreement |
| **Low** | Plausible, significant uncertainty | Tier 3-4 only, limited corroboration |
| **Speculative** | Cannot reliably assess | Noted but not asserted as fact |

## Source Tier Definitions (Universal)

| Tier | Source Type | Examples |
|------|-------------|----------|
| **1** | Laws, regulations, central banks | Fed, SEC, ECB, BIS, FSB |
| **2** | International orgs, Big 4, major FMIs | IMF, Deloitte, SWIFT, DTCC |
| **3** | Industry reports, think tanks, academic | Celent, Gartner, SIFMA |
| **4** | Quality financial media | FT, WSJ, Reuters, Bloomberg |

---

# CITATION FORMAT (Universal)

## In-Text Citations (Stages 1-2)

`[Abbreviation, location]`

| Example | When to Use |
|---------|-------------|
| `[BIS 2024, p.12]` | Page number available |
| `[Research Report, F3]` | Referencing pipeline research |
| `[McKinsey, Ex.2]` | Exhibit reference |

## Slide Footnotes (Stages 3-5)

`Source: [Abbreviation, location]`

Example: `Source: BIS 2024, p.34; McKinsey GPR, Ex.2`

## Full Traceability Chain

`Source: [Research Report, F3 ← Q1.2] via [BIS 2024, p.12]`

Shows: Slide claim ← Summary finding ← Research question ← Original source

---

# VALIDATION RULES

## Stage 1 → Stage 2

- [ ] STAGE_1_HANDOFF package is present
- [ ] At least 3 findings (F-IDs) exist
- [ ] Source tier summary is populated
- [ ] Research questions index is complete

**If fails**: Produce Research Gap Assessment instead of Executive Summary

## Stage 2 → Stage 3

- [ ] STAGE_2_HANDOFF package is present
- [ ] Executive Summary exists (not Gap Assessment)
- [ ] At least 3 synthesized claims with citations
- [ ] Narrative elements are defined

**If fails**: Alert user that summary is insufficient for presentation

## Stage 3 → Stage 4

- [ ] STAGE_3_HANDOFF package is present
- [ ] At least 5 slides in outline
- [ ] Headline sequence complete
- [ ] Visual types specified for data slides
- [ ] Speaker notes present

**If fails**: Alert user; may need more content development in Stage 3

## Stage 4 → Stage 5

- [ ] STAGE_4_HANDOFF package is present
- [ ] JSON schema is valid
- [ ] All slides have layout assignments
- [ ] Design system is complete
- [ ] Content density versions available

**If fails**: Alert user; return to Stage 4 for JSON correction

---

# HANDOFF INTEGRITY CHECKS

## What Must Never Be Lost

| Data | Created In | Must Appear Through |
|------|------------|---------------------|
| Q-IDs | Stage 1 | Stages 2, 3, 4, 5 (traceability) |
| Confidence levels | Stage 1 | Stages 2, 3, 4, 5 |
| Source tiers | Stage 1 | Stages 2, 3, 4, 5 |
| Conflicts | Stage 1 | Stages 2, 3 (acknowledged) |
| Gaps | Stage 1 | Stages 2, 3 (flagged) |
| Data freshness | Stage 1 | Stages 2, 3, 4, 5 (footnotes) |
| Governing thought | Stage 3 | Stages 4, 5 |
| JSON specification | Stage 4 | Stage 5 (embedded in React artifact) |

## Degradation Warnings

If any required field is missing in a handoff:
1. Note the gap explicitly in the next stage's output
2. Lower confidence for affected claims
3. Flag in Process Notes / Flags for Next Stage
