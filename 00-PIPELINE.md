# Financial Services Research Pipeline
## Prompt Orchestrator v2.0

---

# PIPELINE OVERVIEW

This pipeline transforms a research topic into five polished deliverables through sequential prompt execution. No code required — Claude executes each stage and maintains state between stages.

```
┌─────────────┐    ┌─────────────┐    ┌─────────────┐    ┌─────────────┐    ┌─────────────┐
│   STAGE 1   │───▶│   STAGE 2   │───▶│   STAGE 3   │───▶│   STAGE 4   │───▶│   STAGE 5   │
│   Research  │    │   Summary   │    │   Outline   │    │  JSON Spec  │    │   Slides    │
└─────────────┘    └─────────────┘    └─────────────┘    └─────────────┘    └─────────────┘
      │                  │                  │                  │                  │
      ▼                  ▼                  ▼                  ▼                  ▼
 Raw Research      Executive         Presentation       Slide Design        Final Slide
 (15-30 pages)   Summary (2-4p)    Outline (8-15)     JSON Structure      Presentation
```

---

# USER COMMANDS

| Command | Action |
|---------|--------|
| `Start pipeline: [RESEARCH_BRIEF]` | Begin Stage 1 with your research topic |
| `Proceed to P2` | Execute Stage 2 using Stage 1 output |
| `Proceed to P3` | Execute Stage 3 using Stage 2 output |
| `Proceed to P4` | Execute Stage 4 using Stage 3 output |
| `Proceed to P5` | Execute Stage 5 using Stage 4 output |
| `Show deliverables` | Display all five final artifacts |
| `Show [stage] output` | Display specific stage output |

---

# PIPELINE RULES

## For Claude

1. **Read prompts from this folder** — Each stage has its own prompt file
2. **Maintain full context** — Keep all stage outputs in memory throughout the session
3. **Use handoff packages** — Each stage outputs a structured handoff for the next stage
4. **Preserve metadata** — Confidence levels, source tiers, and Q-IDs flow through the pipeline
5. **Wait for user command** — Do not proceed to next stage without explicit "Proceed to P[X]" command

## Stage Execution Protocol

When executing a stage:

1. **Announce stage start**: "Executing Stage [X]: [Name]..."
2. **Read the stage prompt file** from this folder
3. **Execute the full prompt** per its instructions
4. **Output the deliverable** in full
5. **Output the handoff package** (formatted per HANDOFF-SCHEMA.md)
6. **Announce completion**: "✓ Stage [X] Complete. Ready for next stage."

---

# FILE REFERENCES

| File | Purpose |
|------|---------|
| `00-PIPELINE.md` | This orchestrator (read first) |
| `HANDOFF-SCHEMA.md` | Shared format definitions for stage handoffs |
| `Prompt 1 - Deep Research` | Stage 1: Comprehensive research |
| `Prompt 2 - Executive Summary Creation` | Stage 2: Synthesis into executive summary |
| `Prompt 3 - Slide Presentation Outline` | Stage 3: Transform into presentation outline |
| `Prompt 4 - Slide Design Specification` | Stage 4: Generate JSON slide specifications |
| `Prompt 5 - Slide Generation` | Stage 5: Create final slide presentation |

---

# STAGE DETAILS

## Stage 1: Deep Research

**File**: `Prompt 1 - Deep Research`

**Input**: Research brief from user (topic, scope, constraints)

**Process**: Multi-pass research (Phases 0-5) with web search, source verification, and structured analysis

**Output**:
- Full research document (15-30 pages equivalent)
- Appendices A-D (sources, conflicts, gaps, disconfirmation)
- STAGE_1_HANDOFF package

**Key Artifacts Passed Forward**:
- Research Questions (Q-IDs)
- Findings with confidence levels (F1, F2, F3...)
- Source tier classifications
- Identified gaps and conflicts

---

## Stage 2: Executive Summary

**File**: `Prompt 2 - Executive Summary Creation`

**Input**: STAGE_1_HANDOFF package (research document + metadata)

**Process**: Multi-pass synthesis (Passes 1-7) with narrative strategy and quality testing

**Output**:
- Executive Summary (900-2,000 words) OR Research Gap Assessment
- Process Notes
- STAGE_2_HANDOFF package

**Key Artifacts Passed Forward**:
- Synthesized findings with citations
- Branded concepts
- Narrative arc elements
- Abbreviation table

---

## Stage 3: Presentation Outline

**File**: `Prompt 3 - Slide Presentation Outline`

**Input**: STAGE_2_HANDOFF package (executive summary + metadata)

**Process**: Multi-pass presentation design (Passes 1-7) with framework selection and quality testing

**Output**:
- Slide-by-slide outline (8-15 slides)
- Appendix slides with triggers
- Headline sequence
- Process Notes
- STAGE_3_HANDOFF package

**Key Artifacts Passed Forward**:
- Complete slide specifications (titles, content, visuals)
- Governing thought
- Framework selection
- Speaker notes

---

## Stage 4: Slide Design Specification

**File**: `Prompt 4 - Slide Design Specification`

**Input**: STAGE_3_HANDOFF package (presentation outline + metadata)

**Process**: Multi-pass design specification (Passes 1-7) with Chain of Thought reasoning, Chain of Density optimization, and JSON generation

**Output**:
- Complete JSON specification for all slides
- Design system definition (colors, typography, layouts)
- Visual element specifications
- STAGE_4_HANDOFF package

**Key Artifacts Passed Forward**:
- Machine-readable JSON slide specification
- Layout templates per slide
- Chart/visual specifications
- Platform-agnostic design tokens

**Advanced Techniques**:
- **Chain of Thought (CoT)**: Explicit reasoning for visual hierarchy, chart selection, layout decisions
- **Chain of Density (CoD)**: 3-pass content compression (verbose → standard → dense)
- **Multi-pass validation**: Schema compliance, consistency checks

---

## Stage 5: Slide Generation

**File**: `Prompt 5 - Slide Generation`

**Input**: STAGE_4_HANDOFF package (JSON specification + metadata)

**Process**: Transform JSON into final slide content with platform-specific guidance

**Output**:
- Final slide presentation content
- Platform-specific instructions (PowerPoint/Keynote/Google Slides)
- FINAL_DELIVERABLES package (compiles all 5 stages)

**Final Deliverables**:
1. Raw Research Document
2. Executive Summary
3. Presentation Outline
4. JSON Slide Specification
5. Final Slide Presentation

---

# EXECUTION INSTRUCTIONS

## Starting the Pipeline

When user says "Start pipeline: [RESEARCH_BRIEF]":

1. Read this file (00-PIPELINE.md) to understand the workflow
2. Read HANDOFF-SCHEMA.md to understand the handoff format
3. Read "Prompt 1 - Deep Research"
4. Execute Stage 1 with the user's research brief
5. Output the full research deliverable
6. Output the STAGE_1_HANDOFF package
7. Wait for user command

## Proceeding to Stage 2

When user says "Proceed to P2":

1. Read "Prompt 2 - Executive Summary Creation"
2. Use STAGE_1_HANDOFF as the input (already in context)
3. Execute Stage 2
4. Output the executive summary deliverable
5. Output the STAGE_2_HANDOFF package
6. Wait for user command

## Proceeding to Stage 3

When user says "Proceed to P3":

1. Read "Prompt 3 - Slide Presentation Outline"
2. Use STAGE_2_HANDOFF as the input (already in context)
3. Execute Stage 3
4. Output the presentation outline deliverable
5. Output the STAGE_3_HANDOFF package
6. Wait for user command

## Proceeding to Stage 4

When user says "Proceed to P4":

1. Read "Prompt 4 - Slide Design Specification"
2. Use STAGE_3_HANDOFF as the input (already in context)
3. Execute Stage 4 with CoT/CoD techniques
4. Output the JSON slide specification
5. Output the STAGE_4_HANDOFF package
6. Wait for user command

## Proceeding to Stage 5

When user says "Proceed to P5":

1. Read "Prompt 5 - Slide Generation"
2. Use STAGE_4_HANDOFF as the input (already in context)
3. Execute Stage 5
4. Output the final slide presentation
5. Compile and display FINAL_DELIVERABLES summary

---

# FINAL DELIVERABLES FORMAT

After Stage 5 completes, present all artifacts:

```markdown
# PIPELINE COMPLETE

## Research Topic
[Original research brief]

## Pipeline Metadata
| Field | Value |
|-------|-------|
| Executed | [Date] |
| Research Depth | [Brief/Standard/Comprehensive] |
| Summary Density | [Sparse/Moderate/Rich] |
| Presentation Complexity | [Low/Medium/High] |
| Total Slides | [#] |
| JSON Schema Version | [1.0] |

---

## Deliverable 1: Raw Research
**Location**: See Stage 1 output above

## Deliverable 2: Executive Summary
**Location**: See Stage 2 output above

## Deliverable 3: Presentation Outline
**Location**: See Stage 3 output above

## Deliverable 4: JSON Slide Specification
**Location**: See Stage 4 output above

## Deliverable 5: Final Slide Presentation
[Full Stage 5 output]

---

## Appendix: Source Master List
[Consolidated sources from all stages with tier classifications]

## Appendix: Traceability Matrix
[Q-ID → Finding → Summary → Slide → JSON Element mapping]
```

---

# ERROR HANDLING

## If Stage Input is Insufficient

| Stage | Condition | Action |
|-------|-----------|--------|
| P1 | Research brief unclear | Ask user for clarification before proceeding |
| P2 | Research has <3 findings | Produce Research Gap Assessment instead of Summary |
| P3 | Summary has <3 claims | Alert user; suggest returning to P2 with more research |
| P4 | Outline has <5 slides | Alert user; may need more content in P3 |
| P5 | JSON invalid or incomplete | Alert user; return to P4 for correction |

## If User Skips a Stage

If user attempts to skip stages (e.g., "Proceed to P4" without completing P3):
- Alert: "Stage [X] has not been executed. Stage [Y] requires [X]'s output as input. Please complete stages in order."

---

# CONTEXT MANAGEMENT

## What to Maintain in Context

Throughout the pipeline session, maintain:

1. **Original research brief** — Reference for all stages
2. **All stage outputs** — Full deliverables, not just handoffs
3. **Cumulative metadata** — Q-IDs, confidence levels, source tiers
4. **Abbreviation table** — Created in P2, used in P3-P5
5. **JSON specification** — From P4, used in P5
6. **Flags and warnings** — From any stage

## Context Priority (if approaching limits)

1. Current stage prompt instructions (NON-NEGOTIABLE)
2. Most recent handoff package metadata tables
3. JSON specification (for P5)
4. Previous stage's full output
5. Earlier stages' outputs (summarize if needed)

Never discard: Q-ID mappings, confidence levels, source tier classifications, JSON schema

---

# BEGIN

Read this orchestrator, then wait for user command.

When user provides a research brief with "Start pipeline:", execute Stage 1.
