---
name: system-design
description: >
  Scenario-driven system abstraction and boundary governance methodology.
  Use this skill when users discuss system design, architecture design,
  boundary governance, abstraction design, module partitioning, interface design,
  technical proposal review, or system refactoring. Trigger signals include:
  "design a system", "how to architect", "how to partition modules",
  "where is the boundary", "is the abstraction reasonable", "how to define interfaces",
  "review a proposal", "system refactoring".
  Not applicable to pure code implementation, bug fixes, or simple feature additions.
---

# Scenario-Driven System Abstraction and Boundary Governance Methodology

Extract stable abstractions from real-world scenarios, control complexity through semantic attribution and boundary governance, and ultimately form a reviewable design baseline.

## 1. Mode Determination

Infer the mode from user input and announce it at the beginning of the first response:

| Signal | Mode |
|--------|------|
| User describes a new system to design, "help me design", "how to architect", "how to partition modules" | **Interactive Guidance** |
| User already has a design document or description, "review", "spot issues", "is it reasonable", "check" | **Automated Analysis & Review** |
| User only focuses on a specific layer, "just look at the boundary", "check abstraction", "interface definition" | **Focused Analysis** |

Format for notification: `Using XXX mode. Reason: XXX. Can switch at any time.`

## 2. Process Orchestration

The 12-layer methodology serves as a flexible toolkit. First read `references/methodology-full.md` to understand the big picture, then determine which layers are applicable based on the scenario.

**Layer selection rules:**

1. Select applicable layers based on the user's scenario; execution of all layers in order is not required
2. For inapplicable layers, explain why in one sentence and skip
3. Leapfrogging and recombination are allowed; the user may request deeper exploration of any layer at any time
4. Upon completing each logic block, incrementally append to the design baseline file

**Logic block breakdown:**

| Logic Block | Layers Included | After Completion |
|-------------|----------------|------------------|
| Scenario → Boundary | Scenario Collection → Commonality Extraction → System Positioning → Semantic Attribution and Boundary Governance | Generate use case table file + design baseline scenario analysis section, execute coverage check |
| Abstraction → Failure | Core Abstraction Design → Interface Contract → Runtime Semantics → Failure Model | Append to design baseline, execute coverage check |
| Engineering → Versioning | Engineering Constraint Verification → Role Workflow → Extension and Governance → Versioning Solidification | Append to design baseline, execute coverage check |

## 3. Interactive Guidance Rules

### Core Principles

- **One question at a time**: Ask only one core question per round
- **Derive before asking**: Actively infer candidate answers from context, providing 2-4 options with reasoning
- **User confirmation**: The user may select an option, provide custom input, or request re-derivation
- **Proactive filling**: Do not assume the user will provide all information; actively derive from available information

### Information Derivation Priority

1. Information explicitly provided by the user
2. Information readable from the project codebase/documentation
3. Information reasonably inferable from other decisions within the same layer
4. Best practices corresponding to the technology stack
5. Reference suggestions from common industry practices

### Per-Layer Processing Approach

1. Read the reference content for the corresponding layer from `references/`
2. Present the core question for that layer
3. Derive candidate answers based on available information
4. User confirms or revises
5. Record the decision in the design baseline, referencing relevant UC-IDs of use cases (e.g., `Related use cases: UC-03, UC-07`)
6. Provide a 1-2 sentence summary

## 4. Automated Analysis & Review Rules

When the user has an existing design to examine:

1. First understand the full picture of the user's design (read the provided documents/code)
2. Read `references/checklist.md` and review against the checklist item by item
3. Output structure:
   - **Alignments**: Which design decisions are consistent with this methodology
   - **Risks**: Where issues exist such as unclear boundaries, responsibility bloat, semantic pollution, concept overlap
   - **Suggestions**: Specific improvement directions for each risk point
4. Focus on the most prominent issues; comprehensive coverage of all layers is not required

## 5. Output and File Persistence

### In-Chat Output

- Use structured Markdown: tables, lists, decision trees
- Highlight key decisions with `> blockquotes`
- Provide a summary after each layer is completed

### Design Baseline Files

- Design baseline path: `docs/<system-name>-system-design.md`
- Use case table path: `docs/<system-name>-use-cases.md`
- **Inform the user of both file paths at the start of the conversation; the user may change them**
- After the scenario collection layer is completed, generate both files simultaneously
- Incremental persistence: append to the design baseline after each logic block is completed
- Confirm the path exists before writing; create it if it does not

**Design Baseline File Template:**

```markdown
# <System Name> Design Baseline

> Generated based on the Scenario-Driven System Abstraction and Boundary Governance methodology
> Input baseline: [Full Use Case Table](./<system-name>-use-cases.md) (independently maintained; changes require regression review of the design baseline)

## Version History
| Version | Date | Changes |
|---------|------|---------|

## 1. Scenario Analysis
(Commonality extraction, stable concepts, points of differentiation; do not embed the full use case table, reference specific use cases via UC-ID)

## 2. System Positioning and Boundaries
...

## 3. Core Abstraction
...

## 4. Interface Contract
...

## 5. Runtime Semantics and Failure Model
...

## 6. Engineering Constraints and Roles
...

## 7. Extension Governance and Versioning
...

## Pending Issues
...
```

**Use Case Table File Template:**

```markdown
# <System Name> Full Use Case Table

> Input baseline for system design. After use case changes, each section of the design baseline must be reviewed for regression to ensure continued coverage of all use cases.

| UC-ID | Scenario Name | Trigger | Input | System Behavior | Output | Consumer | Path Type | Frequency |
|-------|--------------|---------|-------|-----------------|--------|----------|-----------|-----------|
| UC-01 | ...          | ...     | ...   | ...             | ...    | ...      | Normal    | High      |
```

- UC-ID format: `UC-{sequence number}`, unique identifier; each section of the design baseline references use cases via UC-ID
- Path type: Normal / Boundary / Exception
- Frequency: High Frequency / Low Frequency Critical / Future Extension

## 6. Use Case Coverage and Regression

The use case table is the input baseline for system design. See `references/coverage-regression.md` for details on the coverage verification mechanism; read on demand.

Core principles:
- Upon completing each logic block, verify that decisions cover all use cases
- When the use case table changes, perform regression review across each section of the design baseline
- Record uncovered gaps in pending issues; directly update items that can be auto-repaired

## 7. Self-Constraints

- SKILL.md serves only as the application skeleton; methodology details are read from `references/` on demand
- The 12 layers are not mandatory to execute in full; leapfrogging and recombination are allowed
- The user may switch modes, skip layers, or dive deeper into any layer at any time
- Pause after completing each logic block and ask the user whether to continue
