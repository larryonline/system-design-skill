# Logic Block 1: Scenario → Boundary

> Corresponds to Methodology Sections 5-8

## Section 5: Scenario Collection

### Objective
Collect the usage patterns, input sources, processing paths, output consumers, and exceptional cases the system may encounter. This phase emphasizes divergence; do not rush to abstract or judge boundaries.

### Core Questions

- In what real-world scenarios is the system used?
- Who triggers the system?
- What are the inputs?
- What does the system need to do?
- Who consumes the outputs?
- What are the normal paths, boundary paths, and exceptional paths?
- What are the high-frequency scenarios, low-frequency critical scenarios, and future extension scenarios?

### Deliverables
- Scenario inventory
- Use case inventory
- Normal, boundary, and exceptional path descriptions
- External system actor inventory
- Preliminary input/output descriptions

---

## Section 6: Commonality Extraction

### Objective
Strip business vocabulary from concrete scenarios, identifying structural actions, stable concepts, and mechanisms that can be expressed uniformly.

### Core Questions

- Which actions recur?
- Which concepts remain stable across scenarios?
- Which concepts are merely current business jargon?
- Which differences can be handled via configuration, rules, extensions, or left to external interpretation?
- Which capabilities can be expressed through a unified mechanism?

### Common Structure Reference

```
External Trigger
  → Input Collection
  → State Read
  → Condition Evaluation
  → Rule Matching
  → Computation / Decision / Transformation
  → Result Generation
  → State Update
  → Output Distribution
  → Tracing Record
```

This structure is only a template for extraction; not all systems are required to conform exactly.

### Deliverables
- Common action list
- Stable concept candidates
- List of scenario differences
- List of mechanisms that can be expressed uniformly
- List of content requiring preserved external differences

---

## Section 7: System Positioning

### Objective
Clarify the system's tier within the overall architecture, its essential responsibility, upstream/downstream relationships, and dependency direction.

A system may be infrastructure, a rules layer, an interpretation layer, a configuration layer, a runtime, an orchestration layer, an execution layer, a presentation layer, a business system, a platform system, or a tool system. Positioning determines boundaries and abstractions.

### Core Questions

- What is the system's essential responsibility?
- Is it a business system or a business-agnostic foundational capability?
- Does it define, execute, judge, present, generate results, or consume results?
- Who should depend on it?
- Who should it depend on?
- What are its upstream and downstream?

### Deliverables
- System positioning statement
- System goals and non-goals
- Upstream/downstream relationships
- Dependency direction statement
- System tier definition

### Judgment Principles
System positioning should be as stable as possible. Unclear positioning will lead to persistent confusion in subsequent boundary governance, core abstraction, interface design, and component design.

---

## Section 8: Semantic Attribution and Boundary Governance

### Objective
Determine which semantics, responsibilities, and capabilities belong to the core system and which belong to external systems, preventing responsibility bloat and business contamination of the core system.

### Basic Judgment

Boundary governance first judges semantic attribution, then judges capability attribution.

```
Semantic Attribution: Who has the right of interpretation.
Capability Attribution: Who should be responsible for implementation or commitment.
Interface Attribution: How the outside depends on core capabilities.
```

### Semantic Attribution Model

Semantic attribution is classified not by literal wording, but by the object of interpretation.

Simplest judgment:

> Semantics that define the core system's own establishment, operation, commitment, debugging, governance, and evolution belong to the core system.
> Semantics that define how core capabilities are used, presented, consumed, and validated in external business, processes, presentation, context, and product experience belong to external systems.

### Semantic Classification

| Tier 1 Classification | Tier 2 Classification | Meaning | Enters Core? |
| --- | --- | --- | --- |
| Core System Semantics | Core Ontology Semantics | Defines the core system's own objects, concepts, relationships, and constraints | Should enter |
| Core System Semantics | Core Runtime Semantics | Defines rules for lifecycle, execution, state, dependencies, conflicts, errors, rollback, etc. | Should enter |
| Core System Semantics | Core Interface Semantics | Defines external inputs, outputs, errors, invocation timing, and stability commitments | Should enter |
| Core System Semantics | Core Tooling Semantics | Defines tool behaviors such as configuration validation, debugging, tracing, diagnostics, preview, replay, etc. | Should enter |
| Core System Semantics | Core Governance Semantics | Defines rules for extensions, namespaces, permissions, overriding, versioning, migration, deprecation, etc. | Should enter |
| External Domain Semantics | External Business Semantics | Defines the meaning, judgment, and actions of core results in specific business contexts | Does not enter core |
| External Domain Semantics | External Process Semantics | Defines how external systems organize and drive business processes | Does not enter core |
| External Domain Semantics | External Presentation Semantics | Defines UI, animation, sound, prompts, page state, and other presentation methods | Does not enter core |
| External Domain Semantics | External Context Semantics | Defines external business, product, user, and scenario context | Does not enter core |
| External Domain Semantics | Product Experience Semantics | Defines whether the final product is effective, trustworthy, and usable | Does not enter core |

### Criteria for Whether a Capability Enters the Core

```
1. Does it align with the system positioning?
2. Does it belong to the core system's external commitment?
3. Is it used to define the core system's own establishment, operation, interface, debugging, governance, or evolution?
4. Does it exist stably across multiple scenarios?
5. Is it the consistency foundation for other capabilities?
6. Would it be difficult for external systems to accomplish independently while maintaining consistency?
7. Can it be expressed through a more fundamental general mechanism?
8. Does entering the core make the system more stable, rather than more complex?
```

### Deliverables
- Core responsibility inventory
- External responsibility inventory
- Semantic attribution judgment table
- Boundary judgment rules
- Boundary violation use case inventory
