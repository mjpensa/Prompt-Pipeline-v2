# Handoff Schema
## Shared Format Definitions for Pipeline Stages

---

# PURPOSE

This schema defines the standardized format for passing data between pipeline stages. Each stage outputs a HANDOFF PACKAGE that the next stage consumes as input.

**Key Principle**: Information should flow through the pipeline without loss. Metadata established in Stage 1 (Q-IDs, confidence levels, source tiers) must be preserved and accessible in Stage 3.

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
| F-ID | Finding | Q-Ref | Confidence | Used in Summary? |
|------|---------|-------|------------|------------------|
| F1 | [Title] | Q1 | High | ✅ |
| F2 | [Title] | Q1.2 | Medium | ✅ |
| F3 | [Title] | Q2 | Low | ⚠️ (flagged) |

## Branded Concepts
| Concept | Source Evidence | Definition |
|---------|-----------------|------------|
| [Concept name] | [F-ID or data point] | [Brief definition] |

## Narrative Elements
| Element | Content |
|---------|---------|
| Core Thesis | [One sentence] |
| Opening Hook | [Strategy used + content] |
| Narrative Arc | [Pattern used: Transformation/Collision/etc.] |
| Closing | [Strategy used + content] |
| Key Tension | [Primary conflict or "so what"] |

## Citation Abbreviation Table
| Abbreviation | Full Name | Tier |
|--------------|-----------|------|
| [Abbrev] | [Full source name] | [1-4] |

## Stakeholder Implications
| Stakeholder | Key Implication | Urgency |
|-------------|-----------------|---------|
| [Group] | [Implication] | High/Med/Low |

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

## Flags for Next Stage
- [ ] [Presentation-relevant notes, e.g., "Strong visual opportunity: market share data"]
- [ ] [Warnings, e.g., "Closing requires callback to opening statistic"]
- [ ] [Complexity indicator for slide count targeting]

## Full Executive Summary
[Complete Stage 2 deliverable — summary + process notes]

<<<END_STAGE_2_HANDOFF>>>
```

---

# FINAL DELIVERABLES PACKAGE

Output by: `Prompt 3 - Slide Presentation Outline`
This is the terminal output — no further handoff needed.

```markdown
<<<FINAL_DELIVERABLES>>>

## Pipeline Execution Summary
| Stage | Status | Key Metrics |
|-------|--------|-------------|
| 1 - Research | ✅ Complete | [X] findings, [Y] sources |
| 2 - Summary | ✅ Complete | [X] words, [Density] |
| 3 - Presentation | ✅ Complete | [X] slides + [Y] appendix |

## Research Brief (Original)
[Carried through entire pipeline]

## Cumulative Metadata
| Field | Value |
|-------|-------|
| Research Depth | [Brief/Standard/Comprehensive] |
| Summary Density | [Sparse/Moderate/Rich] |
| Presentation Complexity | [Low/Medium/High] |
| Total Findings | [#] |
| Total Sources | [#] by tier |
| Data Freshness | [Date] |
| Pipeline Executed | [Date] |

---

## DELIVERABLE 1: Raw Research

[Full Stage 1 output]

---

## DELIVERABLE 2: Executive Summary

[Full Stage 2 output — summary only, process notes optional]

---

## DELIVERABLE 3: Slide Presentation Outline

[Full Stage 3 output — all slides + appendix + headline sequence]

---

## Master Source List
| Abbrev | Full Name | Tier | Used In |
|--------|-----------|------|---------|
| [Abbrev] | [Name] | [1-4] | P1, P2, P3 |

## Q-ID to Slide Traceability
| Q-ID | Finding | Summary Section | Slide # |
|------|---------|-----------------|---------|
| Q1 | F1 | [Section] | 3, 4 |
| Q1.2 | F2 | [Section] | 5 |

<<<END_FINAL_DELIVERABLES>>>
```

---

# CROSS-STAGE FIELD MAPPINGS

## Consistent Terminology

| Concept | Stage 1 Term | Stage 2 Term | Stage 3 Term |
|---------|--------------|--------------|--------------|
| Research questions | Q-ID (Q1, Q1.1) | Q-Ref | Q-Ref |
| Findings | F[#] | F[#] | F[#] |
| Confidence | High/Medium/Low/Speculative | High/Med/Low | High/Med/Low |
| Source authority | Tier 1-5 | Tier 1-4 | Tier (in footnotes) |
| Inference marker | `[INFERENCE]` | `[INFERENCE]` | `[INFERENCE]` in speaker notes |
| Gaps | Appendix C | Gaps Acknowledged | Appendix slides |

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

## In-Text Citations

All stages use: `[Abbreviation, location]`

| Example | When to Use |
|---------|-------------|
| `[BIS 2024, p.12]` | Page number available |
| `[Research Report, F3]` | Referencing pipeline research |
| `[McKinsey, Ex.2]` | Exhibit reference |

## Footnotes (Stage 3 Only)

Slide footnotes use: `Source: [Abbreviation, location]`

Example: `Source: BIS 2024, p.34; McKinsey GPR, Ex.2`

## Traceability Chain

For maximum traceability, Stage 3 can reference the full chain:

`Source: [Research Report, F3 ← Q1.2] via [BIS 2024, p.12]`

This shows: Slide claim ← Summary finding ← Research question ← Original source

---

# VALIDATION RULES

## Stage 1 → Stage 2 Validation

Before executing Stage 2, verify:
- [ ] STAGE_1_HANDOFF package is present
- [ ] At least 3 findings (F-IDs) exist
- [ ] Source tier summary is populated
- [ ] Research questions index is complete

If validation fails: Produce Research Gap Assessment instead of Executive Summary

## Stage 2 → Stage 3 Validation

Before executing Stage 3, verify:
- [ ] STAGE_2_HANDOFF package is present
- [ ] Executive Summary exists (not Gap Assessment)
- [ ] At least 3 synthesized claims with citations
- [ ] Narrative elements are defined

If validation fails: Alert user that summary is insufficient for presentation

---

# HANDOFF INTEGRITY CHECKS

## What Must Never Be Lost

| Data | Created In | Must Appear In |
|------|------------|----------------|
| Q-IDs | Stage 1 | Stage 2, Stage 3 (traceability) |
| Confidence levels | Stage 1 | Stage 2, Stage 3 (speaker notes) |
| Source tiers | Stage 1 | Stage 2, Stage 3 (footnotes) |
| Conflicts | Stage 1 | Stage 2, Stage 3 (acknowledged) |
| Gaps | Stage 1 | Stage 2, Stage 3 (flagged) |
| Data freshness date | Stage 1 | Stage 2, Stage 3 (footnote) |

## Degradation Warnings

If any required field is missing in a handoff:
1. Note the gap explicitly in the next stage's output
2. Lower confidence for affected claims
3. Flag in Process Notes / Flags for Next Stage
