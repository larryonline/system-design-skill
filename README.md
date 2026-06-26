[:cn: 中文版本](README_CN.md)

# Scenario-Driven System Abstraction and Boundary Governance Methodology

> Discover problems through real-world scenarios, extract abstractions through commonality analysis, clarify interpretive authority through semantic attribution, and control complexity through boundary governance — ultimately forming a stable, clear, and reviewable design baseline.

A system design methodology delivered as a Claude Code Skill. Designed for early-to-mid stage complex system design — where scenarios are complex, requirements come from diverse sources, feature creep and responsibility bloat are common, and stable abstractions need to be extracted from a large number of use cases.

## Installation

### Option 1: Clone to local skills directory

```bash
mkdir -p ~/.claude/skills
git clone https://github.com/larryonline/system-design-skill.git ~/.claude/skills/system-design
```

### Option 2: Let Claude Code install it for you

Ask Claude Code:

```
Please install the system-design skill by cloning https://github.com/larryonline/system-design-skill to my local skills directory
```

## Triggering

The skill activates automatically when discussing:

- System design, architecture design, module partitioning
- Boundary governance, abstraction design, interface definition
- Technical proposal review, system refactoring

Not applicable to pure code implementation, bug fixes, or simple feature additions.

## Directory Structure

```
├── SKILL.md                        # Skill application skeleton
├── references/                     # Methodology details, loaded on demand
│   ├── methodology-full.md         # Complete 12-layer methodology
│   ├── layers-1-4.md               # Scenario → Boundary
│   ├── layers-5-8.md               # Abstraction → Failure
│   ├── layers-9-12.md              # Engineering → Versioning
│   ├── checklist.md                # General design checklist
│   ├── aesthetics.md               # Design aesthetic preferences
│   └── coverage-regression.md      # Use case coverage and regression mechanism
```

## Three Working Modes

| Mode | Signal | Behavior |
|------|--------|----------|
| Interactive Guidance | Designing a new system from scratch | Layer-by-layer guidance through scenario collection, boundary governance, and abstraction design; generates use case table + design baseline |
| Automated Analysis & Review | Reviewing an existing design | Outputs alignment points, risks, and suggestions against the checklist |
| Focused Analysis | Examining a specific layer | Deep-dives into a particular dimension (boundary/abstraction/interface) without full coverage |

## Outputs

Interactive guidance mode produces two files:

- `docs/<system-name>-use-cases.md` — Full use case table, the design input baseline. 9-column format (UC-ID, Scenario Name, Trigger, Input, System Behavior, Output, Consumer, Path Type, Frequency)
- `docs/<system-name>-system-design.md` — Design baseline covering 7 design facets (Scenario Analysis → System Positioning & Boundaries → Core Abstractions → Interface Contracts → Runtime Semantics & Failure Model → Engineering Constraints & Roles → Extension Governance & Versioning)

When the use case table changes, regression review is automatically triggered across all chapters of the design baseline.

