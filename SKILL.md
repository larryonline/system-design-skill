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

**Logic block gates:**

Logic blocks must not be skipped or merged without user confirmation. Between each block, execute a mandatory gate before proceeding:

| Gate | Trigger | Required Action |
|------|---------|-----------------|
| **Boundary stability gate** | After completing Block 1 (Scenario → Boundary), before entering Block 2 | For each core/external responsibility, output a Semantic Attribution table: concept → Core or External → justification. Ask user: "Are the boundaries stable? Can we proceed to core abstraction?" Do NOT propose core concepts until the user confirms. |
| **Block transition gate** | After completing any logic block, before entering the next | Execute coverage check against all UC-IDs. Output: "X/Y use cases covered. Uncovered: [list]." Ask user: "Continue to next block?" |

**Design baseline write rule:**

- Write to the design baseline ONLY after the user confirms the logic block's decisions
- If a concept previously written to the baseline is later proven wrong, revert it and record the correction in the version history
- Never write unconfirmed concepts to the baseline—it is cheaper to delay writing than to correct already-written content

**Block 1 special requirements: extension scenario classification**

When the system supports extensions (plugins, DLC, MOD, add-ons), scenario collection MUST cover the full extension lifecycle with structured classification, not as scattered afterthoughts:

| Extension Dimension | Typical Scenarios | Description |
|---------------------|-------------------|-------------|
| New content registration | New definitions, new configurations, new profiles via extension | Extensions introduce content that does not exist in the base system |
| Content override | Extensions modifying or replacing existing content | Extensions change what the base system defined |
| Conflict detection | Detecting and reporting conflicts between sources | Multiple extensions claim the same content or contradict each other |
| Uninstall and rollback | Removing extension content and restoring prior state | Extension is removed and the system must return to a consistent state |

A system claiming to support extensions must cover the complete chain in use cases: register → load → instantiate → conflict resolve → uninstall.

**Logic block breakdown:**

| Logic Block | Layers Included | Gate Before Proceeding |
|-------------|----------------|----------------------|
| Scenario → Boundary | Scenario Collection → Commonality Extraction → System Positioning → Semantic Attribution and Boundary Governance | Boundary stability gate: output Semantic Attribution table, user confirms boundaries are stable |
| Abstraction → Failure | Core Abstraction Design → Interface Contract → Runtime Semantics → Failure Model | Coverage check against all UC-IDs, user confirms |
| Engineering → Versioning | Engineering Constraint Verification → Role Workflow → Extension and Governance → Versioning Solidification | Coverage check, user confirms |

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
4. **Native capabilities of the target platform** (e.g., Godot Resource/Signal/Expression/@export/@onready, React Context/useReducer/Portal, Unreal GameplayAbility/DataAsset). Actively consult platform-specific references before proposing mechanisms that the platform already provides. Failure to check platform primitives leads to designs that reinvent built-in capabilities (e.g., designing a custom expression evaluator when Godot provides `Expression`, building a custom event bus when React provides Context + useReducer).
5. Best practices corresponding to the technology stack
6. Reference suggestions from common industry practices

### Per-Layer Processing Approach

1. Read the reference content for the corresponding layer from `references/`
2. Present the core question for that layer
3. Derive candidate answers based on available information
4. User confirms or revises
5. Record the decision in the design baseline, referencing relevant UC-IDs of use cases (e.g., `Related use cases: UC-03, UC-07`)
6. Provide a 1-2 sentence summary

### Concept Self-Check (Mandatory for Core Abstraction Design)

Before proposing any new core concept in Layer 5, execute this judgment chain and output the result to the user:

```
Can existing concepts express this?
  → Yes: use existing concepts. Stop here.
  → No: continue.

Can existing mechanisms compose this?
  → Yes: compose; do not add new concepts. Stop here.
  → No: continue.

Is it merely a configuration difference?
  → Yes: use configuration, not new concepts. Stop here.
  → No: continue.

Is it merely an external interpretation difference?
  → Yes: leave to external systems. Stop here.
  → No: continue.

Has a genuinely new stable core semantics emerged?
  → Only now is introducing a new concept justified.
```

This prevents three common failure patterns:
- **Implementation details elevated to core concepts**: e.g., a DependencyGraph that is purely a derived index of formula expressions, not a standalone concept
- **Configuration options turned into concepts**: e.g., a configurable CalculationPipeline when a hardcoded calculation order suffices
- **Naming conventions replacing mechanisms**: e.g., a SourceRegistry when fact_id prefix matching already handles source tracking

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
- **Incremental persistence**: append to the design baseline ONLY after the logic block's decisions are confirmed by the user. Do not write unconfirmed concepts to the baseline—it is cheaper to delay writing than to correct already-written content
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
- **Boundary stability gate**: before entering core abstraction design, output a Semantic Attribution table and get user confirmation. Do not skip this gate even if the user seems satisfied with scenario collection
- **Concept self-check**: before proposing any new core concept, execute the judgment chain (existing concepts? → existing mechanisms? → configuration difference? → external interpretation? → genuinely new semantics?). Output the result
- **Design baseline write discipline**: write to the baseline only after the user confirms the logic block. Never write unconfirmed concepts
- Pause after completing each logic block and ask the user whether to continue
