# Financial Services Research Pipeline
## Prompt Orchestrator v1.0

---

# PIPELINE OVERVIEW

This pipeline transforms a research topic into three polished deliverables through sequential prompt execution. No code required — Claude executes each stage and maintains state between stages.

```
┌─────────────┐    ┌─────────────┐    ┌─────────────┐
│   STAGE 1   │───▶│   STAGE 2   │───▶│   STAGE 3   │
│   Research  │    │   Summary   │    │ Presentation│
└─────────────┘    └─────────────┘    └─────────────┘
      │                  │                  │
      ▼                  ▼                  ▼
 Raw Research      Executive         Slide Deck
 (15-30 pages)   Summary (2-4p)    Outline (8-15)
```

---

# USER COMMANDS

| Command | Action |
|---------|--------|
| `Start pipeline: [RESEARCH_BRIEF]` | Begin Stage 1 with your research topic |
| `Proceed to P2` | Execute Stage 2 using Stage 1 output |
| `Proceed to P3` | Execute Stage 3 using Stage 2 output |
| `Show deliverables` | Display all three final artifacts |
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
| `Prompt 3 - Slide Presentation Outline` | Stage 3: Transform into presentation |

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

**Final Deliverable**: Complete presentation outline ready for slide creation

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
5. Compile and display FINAL_DELIVERABLES summary

---

# FINAL DELIVERABLES FORMAT

After Stage 3 completes, present all artifacts:

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

---

## Deliverable 1: Raw Research
[Full Stage 1 output — can be collapsed/expanded]

---

## Deliverable 2: Executive Summary
[Full Stage 2 output]

---

## Deliverable 3: Slide Presentation Outline
[Full Stage 3 output]

---

## Appendix: Source Master List
[Consolidated sources from all stages with tier classifications]
```

---

# ERROR HANDLING

## If Stage Input is Insufficient

| Stage | Condition | Action |
|-------|-----------|--------|
| P1 | Research brief unclear | Ask user for clarification before proceeding |
| P2 | Research has <3 findings | Produce Research Gap Assessment instead of Summary |
| P3 | Summary has <3 claims | Alert user; suggest returning to P2 with more research |

## If User Skips a Stage

If user says "Proceed to P3" without completing P2:
- Alert: "Stage 2 (Executive Summary) has not been executed. The presentation requires a summary as input. Please say 'Proceed to P2' first, or provide an executive summary directly."

---

# CONTEXT MANAGEMENT

## What to Maintain in Context

Throughout the pipeline session, maintain:

1. **Original research brief** — Reference for all stages
2. **All stage outputs** — Full deliverables, not just handoffs
3. **Cumulative metadata** — Q-IDs, confidence levels, source tiers
4. **Abbreviation table** — Created in P2, used in P3
5. **Flags and warnings** — From any stage

## Context Limits

If context becomes too long:
1. Prioritize: Current stage input > Previous handoff packages > Full previous outputs
2. Summarize earlier outputs if needed, but preserve all handoff package data
3. Never discard: Q-ID mappings, confidence levels, source tier classifications

---

# BEGIN

Read this orchestrator, then wait for user command.

When user provides a research brief with "Start pipeline:", execute Stage 1.
