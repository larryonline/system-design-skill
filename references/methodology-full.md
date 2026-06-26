# Scenario-Driven System Abstraction and Boundary Governance Methodology

## Document Version: v1.1

## 1. Document Purpose

This document describes a methodology for the early and mid-stage design of complex systems, establishing a reviewable design closed loop across real-world scenarios, stable abstractions, system boundaries, runtime semantics, engineering constraints, role responsibilities, and long-term governance.

This methodology is particularly applicable in the following situations:

* Scenarios are complex, with diverse sources of requirements.
* There is a tendency toward feature stacking, responsibility bloat, or unclear boundaries.
* Stable abstractions need to be extracted from a large number of use cases.
* A distinction must be made between core system responsibilities and external system responsibilities.
* There is a need to balance abstraction correctness, engineering feasibility, user experience, and long-term evolution.
* Design consensus needs to be solidified through versioned documentation.

Core goal:

> Use real-world scenarios to expose problems, use commonality extraction to derive abstractions, use aesthetic preferences to constrain structural quality, use semantic attribution to clarify interpretive authority, use boundary governance to control complexity, use runtime semantics and engineering constraints to ensure implementability, use role workflows to verify usability, maintainability, and evolvability, and ultimately form a stable, clear, and reviewable design baseline.

---

## 2. Methodology Overview

This methodology can be summarized as:

> Scenario-driven, abstraction convergence, aesthetic calibration, semantic attribution, boundary governance, runtime validation, engineering implementation, role closed-loop, long-term evolution.

Full process:

```text
Scenario Collection
  → Commonality Extraction
  → System Positioning
  → Aesthetic Preferences Calibration
  → Semantic Attribution and Boundary Governance
  → Core Abstraction Design
  → Interface Contract
  → Runtime Semantics
  → Failure Model
  → Engineering Constraint Validation
  → Role Workflow and Responsibility Attribution
  → Extension and Governance
  → Versioning Solidification
```

Key dependency relationships:

```text
Scenarios serve as input pressure.
Commonality is the source of abstraction.
System positioning determines the boundary.
Aesthetic preferences constrain design trade-offs.
Semantic attribution determines interpretive authority.
Boundary governance determines responsibility attribution.
Core abstraction defines the system language.
Interface contract solidifies external dependencies.
Runtime semantics defines dynamic behavior.
Failure model defines exceptional behavior.
Engineering constraints verify implementability.
Role workflows verify usability.
Extension governance ensures long-term stability.
Versioned documentation solidifies design consensus.
```

---

## 3. Core Ideas

### 3.1 First Apply Pressure with Scenarios, Then Converge with Abstractions

System design should not start directly from modules, components, classes, or interfaces, but should begin with real-world scenarios.

Real-world scenarios are used to expose:

* How the system will be used.
* Whether critical paths are covered.
* Whether responsibility boundaries are clear.
* Whether abstractions are insufficient or excessive.
* Whether there are hidden exceptional paths and runtime complexity.

Scenarios are input, not the final design result. The ultimate goal is not to design separate functionality for each scenario, but to extract stable common structures from a large number of scenarios.

### 3.2 First Define What the System Is, Then Define What the System Does

Complex systems should not start directly from a feature list. A more stable order is:

```text
System Positioning → System Boundary → Core Abstraction → Components, Interfaces, and Runtime Mechanisms
```

Where:

* System positioning answers: what is this system in essence.
* System boundary answers: what it is responsible for and what it is not responsible for.
* Core abstraction answers: which stable concepts it uses to express responsibilities.
* Components, interfaces, and runtime mechanisms answer: how it is implemented, integrated, and used.

### 3.3 Determine Interpretive Authority by Semantic Attribution

The core system does not "refuse to interpret"; it only interprets semantics that align with its own positioning and boundaries. External systems are not "free to interpret anything either"; they interpret semantics that belong to external business, processes, presentation, context, and product experience.

The criterion is not "can the external system interpret it?" but:

```text
Does this semantics define the core system itself, or does it define the external use of core capabilities?
```

### 3.4 Roles Are Not Activities; Roles Are Subjects of Responsibility

Do not directly decompose testing, debugging, performance optimization, version governance, integration, configuration production, and other activities into separate roles. Distinguish between:

```text
Primary role: stable subject of responsibility
Responsibility domain: a category of responsibilities undertaken by a role
Activity: specific actions within a responsibility domain
```

This distinction avoids overly fine-grained roles, dispersed responsibilities, and unclear collaboration boundaries.

---

## 4. System Design Aesthetic Preferences

### 4.1 Definition

System design aesthetic preferences are quality orientations that run throughout scenario analysis, abstraction design, boundary governance, interface design, runtime semantics, engineering implementation, extension governance, and version evolution.

They are not local style choices, but fundamental criteria for design trade-offs.

### 4.2 Core Preferences

| Preference | Meaning | Key Evaluation Points |
| --- | --- | --- |
| Simple | Keep only necessary concepts and mechanisms | Can existing concepts express this; is an overly heavy structure introduced for a few special cases |
| Clear | Layers, responsibilities, boundaries, dependencies, and interfaces are explicit | Whether responsibility attribution is clear, what externals can depend on, what internals hide |
| Self-consistent | Concepts, boundaries, runtime semantics, and failure models do not contradict | Whether definitions, behaviors, interfaces, failures, and governance are consistent |
| Self-explanatory | Concepts, outputs, errors, and trace information can explain themselves | Whether result provenance, error causes, configuration impact, and interface promises are understandable |
| Conceptually orthogonal | Core concepts should not overlap as much as possible | Whether there is responsibility overlap; can it be expressed through composition |
| Composable | Combine new capabilities through existing mechanisms | Is a new requirement a new core semantics, or a combination of existing mechanisms |
| Well-layered | Each layer only handles its own problems | Does the lower layer understand high-level business; does the upper layer bypass lower-layer mechanisms |
| Single dependency direction | Dependency direction is stable and predictable | Are there reverse dependencies, circular dependencies, or bypassing interfaces |
| Semantically closed | Core promised semantics can be interpreted, executed, tracked, verified, and governed | Do all core definitions have runtime semantics and governance rules |
| Expressionally stable | Core language and mechanisms are stable over the long term | Is it merely a stage-specific business term; is it suitable as a core language |
| Predictable | Output is reproducible when input, state, and rules are clear | Whether execution order, conflict handling, and failure behavior are explicit |
| Traceable | Key results have sources, processes, and attribution | What was read, what was matched, why this result was obtained |
| Failures explicit | Failures are classified, exposed, and handled | How are missing, invalid, conflicting, and version-incompatible cases handled |
| Least surprise | Behavior aligns with user intuition | Whether default behavior is natural; whether exceptional behavior is clear |
| Open but controlled | Extensible, but constrained by boundaries, permissions, versions, and conflict rules | What can extensions do, what can they not do, how to roll back |
| Gradual complexity | Simple scenarios expressed simply, complex capabilities unfolded on demand | Whether the entry-level path and advanced path are clear |
| Locally understandable | Modifying a local part does not require understanding the entire system | Whether configurations, components, and extensions can be verified locally |
| Safe by default | Default paths are safe, stable, and controllable | Whether high-risk capabilities require explicit opt-in |
| Unified mechanism, diverse expression | Core mechanisms are unified, peripheral expression is flexible | Whether the core expands due to expression differences |

### 4.3 Summary

> A good system should use a small set of stable, orthogonal, composable core concepts to form a simple, clear, self-consistent, predictable, traceable, and evolvable structure; keep simple scenarios simple, allow controlled extension for complex capabilities, unify core mechanisms, and keep external expression flexible.

Shorter expression:

> Core simple and self-consistent, boundaries clear and stable, behavior predictable and traceable, extension open but controlled.

---

## 5. Layer 1: Scenario Collection

### 5.1 Goal

Collect the usage patterns, input sources, processing paths, output consumers, and exceptional situations the system may encounter. This phase emphasizes divergence; do not rush to abstract or judge boundaries.

### 5.2 Core Questions

```text
In what real-world scenarios is the system used?
Who triggers the system?
What is the input?
What does the system need to do?
Who consumes the output?
What are the normal paths, boundary paths, and exceptional paths?
What are the high-frequency scenarios, low-frequency critical scenarios, and future expansion scenarios?
```

### 5.3 Outputs

* Scenario inventory
* Use case inventory
* Descriptions of normal, boundary, and exceptional paths
* External system participant inventory
* Preliminary input/output descriptions

---

## 6. Layer 2: Commonality Extraction

### 6.1 Goal

Strip away business vocabulary from concrete scenarios to identify structural actions, stable concepts, and mechanisms that can be expressed uniformly.

### 6.2 Core Questions

```text
Which actions recur repeatedly?
Which concepts exist stably across scenarios?
Which concepts are merely current business terminology?
Which differences can be handled through configuration, rules, extensions, or left to external interpretation?
Which capabilities can be expressed through a unified mechanism?
```

### 6.3 Common Structure Reference

```text
External trigger
  → Input collection
  → State reading
  → Condition evaluation
  → Rule matching
  → Computation / Decision / Transformation
  → Result generation
  → State update
  → Output distribution
  → Trace recording
```

This structure is only a extraction template; not all systems are required to conform fully.

### 6.4 Outputs

* List of common actions
* Candidate stable concepts
* List of scenario differences
* List of mechanisms that can be expressed uniformly
* List of content that needs to retain external differentiation

---

## 7. Layer 3: System Positioning

### 7.1 Goal

Clarify the system's layer within the overall architecture, its essential responsibilities, upstream and downstream relationships, and dependency direction.

The system may be an infrastructure, rule layer, interpretation layer, configuration layer, runtime, orchestration layer, execution layer, presentation layer, business system, platform system, or tool system. Positioning determines both boundary and abstraction.

### 7.2 Core Questions

```text
What is the essential responsibility of the system?
Is it a business system, or a business-agnostic foundational capability?
Does it define, execute, evaluate, present, generate results, or consume results?
Who should depend on it?
Who should it depend on?
What are its upstream and downstream?
```

### 7.3 Outputs

* System positioning statement
* System goals and non-goals
* Upstream and downstream relationships
* Dependency direction description
* System layer definition

### 7.4 Guiding Principle

System positioning should be as stable as possible. Unclear positioning leads to persistent confusion in subsequent boundary governance, core abstraction, interface design, and component design.

---

## 8. Layer 4: Semantic Attribution and Boundary Governance

### 8.1 Goal

Clarify which semantics, responsibilities, and capabilities belong to the core system and which belong to external systems, preventing core system responsibility bloat and business contamination.

### 8.2 Basic Judgment

Boundary governance first judges semantic attribution, then judges capability attribution.

```text
Semantic attribution: who has interpretive authority.
Capability attribution: who should be responsible for implementation or commitment.
Interface attribution: how externals depend on core capabilities.
```

### 8.3 Semantic Attribution Model

Semantic attribution is not classified by the literal word, but by the object of interpretation. Do not assume that because a word sounds like "process," "presentation," "context," or "interaction," it automatically belongs to core or external. The core system may also have runtime processes, debug presentation, execution context, and tool interactions; external systems may also have business processes, product presentation, user context, and product interactions.

Simplest judgment:

```text
Semantics that define the core system's own establishment, operation, commitment, debugging, governance, and evolution belong to the core system.
Semantics that define how core capabilities are used, presented, consumed, and verified in external business, processes, presentation, context, and product experience belong to external systems.
```

### 8.4 Semantic Classification

| Level 1 Category | Level 2 Category | Meaning | Enters Core |
| --- | --- | --- | --- |
| Core system semantics | Core ontology semantics | Defines the core system's own objects, concepts, relationships, and constraints | Should enter |
| Core system semantics | Core runtime semantics | Defines rules for lifecycle, execution, state, dependencies, conflicts, errors, rollback, etc. | Should enter |
| Core system semantics | Core interface semantics | Defines external inputs, outputs, errors, invocation timing, and stability commitments | Should enter |
| Core system semantics | Core tool semantics | Defines tool behaviors such as configuration validation, debugging, tracing, diagnostics, preview, replay, etc. | Should enter |
| Core system semantics | Core governance semantics | Defines rules for extension, namespace, permissions, overriding, versioning, migration, deprecation, etc. | Should enter |
| External domain semantics | External business semantics | Defines the meaning, judgment, and action of core results in specific business contexts | Does not enter core |
| External domain semantics | External process semantics | Defines how external systems organize and advance business processes | Does not enter core |
| External domain semantics | External presentation semantics | Defines UI, animation, sound, prompts, page state, and other presentation methods | Does not enter core |
| External domain semantics | External context semantics | Defines external business, product, user, and scenario context | Does not enter core |
| External domain semantics | Product experience semantics | Defines whether the final product is effective, trustworthy, and usable | Does not enter core |

### 8.5 Criteria for Whether a Capability Enters the Core

Whether a capability enters the core system is determined by the following order:

```text
1. Does it align with the system positioning?
2. Is it part of the core system's external commitments?
3. Is it used to define the core system's own establishment, operation, interface, debugging, governance, or evolution?
4. Does it exist stably across multiple scenarios?
5. Is it a consistency foundation for other capabilities?
6. Is it difficult for external systems to accomplish independently while maintaining consistency?
7. Can it be expressed through a more fundamental common mechanism?
8. Does entering the core make the system more stable, rather than more complex?
```

### 8.6 Outputs

* Core responsibility inventory
* External responsibility inventory
* Semantic attribution judgment table
* Boundary judgment rules
* Boundary violation use case inventory

---

## 9. Layer 5: Core Abstraction Design

### 9.1 Goal

Cover as many scenarios as possible with as few, stable, and clear core concepts as possible. Core abstraction is not about decomposing modules; it is about defining the system's own language.

### 9.2 Core Questions

```text
What is the minimum set of core concepts the system needs?
What is the responsibility of each concept?
What are the relationships between concepts?
Which concepts belong to definition-time, runtime, input, output, process, or trace information?
Which concepts are merely external interpretations?
```

### 9.3 Abstraction Principles

| Principle | Meaning |
| --- | --- |
| Determine abstraction attribution by system positioning | Do not judge attribution by "who can also do it," but by "who should be responsible" |
| Determine interpretive authority by semantic attribution | Core interprets core system semantics; external interprets external domain semantics |
| Prefer structural concepts over business concepts | Prioritize cross-scenario concepts such as input, state, rule, condition, computation, result, event, dependency, conflict, priority, lifecycle, trace |
| Prefer unified mechanisms over scenario-specific expressions | Commonalities enter the mechanism; differences enter configuration, rules, extensions, or external interpretation |
| Core does not understand external business meaning, but understands its own runtime rules | Lifecycle, execution order, dependencies, conflicts, state consistency, errors, versions, tracing belong to core runtime semantics |
| External is responsible for using results; core is responsible for guaranteeing result semantics stability | External decides the purpose of results; core guarantees what the result is, how it is produced, whether it is valid, and whether it can be traced |
| Compose, do not bloat | New requirements should first be expressed by combining existing concepts and mechanisms; only introduce new concepts when a genuinely new stable core semantics emerges |
| Abstraction serves long-term stability | Abstraction must balance stability, understandability, implementability, extensibility, debuggability, maintainability, and usage cost |

### 9.4 Order of Judgment for Adding New Core Concepts

```text
Can existing concepts express it?
Can existing mechanisms compose it?
Is it merely a configuration difference?
Is it merely an external interpretation difference?
Has a genuinely new stable core semantics truly emerged?
```

### 9.5 Outputs

* Core concept model
* Concept relationship description
* Concept naming conventions
* Abstraction attribution judgment rules
* Classification of definition-time, runtime, input, output, and trace

---

## 10. Layer 6: Interface Contract

### 10.1 Goal

Transform system boundaries into executable, testable, dependable interface contracts.

```text
Boundary answers: who is responsible for what.
Interface answers: how they interact.
```

### 10.2 Core Questions

```text
What capabilities does the system expose externally?
What are the inputs, outputs, caller, and invocation timing?
Synchronous or asynchronous?
Is it idempotent?
How are failures expressed?
How are versions compatible?
What behaviors can external systems depend on?
What are merely internal implementation details?
```

### 10.3 Interface Contract Table

| Interface | Caller | Callee | Input | Output | Timing | Error Behavior | Stability |
| --- | --- | --- | --- | --- | --- | --- | --- |

### 10.4 Outputs

* External interface inventory
* Input/output model
* Invocation timing description
* Error contract
* Idempotency description
* Stability commitment
* Version compatibility rules

---

## 11. Layer 7: Runtime Semantics Design

### 11.1 Goal

Move from static architecture to dynamic runtime, clarifying how the system works along the temporal dimension. Many systems are not wrong in their architecture diagrams, but lack clear definitions of runtime semantics.

### 11.2 Core Questions

```text
When does the system initialize, load configuration, receive input, execute processing, update state, output results, and clean up resources?
Does it support pause, resume, rollback?
What happens when multiple inputs arrive simultaneously?
What happens when multiple rules match simultaneously?
What happens when multiple state updates occur simultaneously?
```

### 11.3 Common Runtime Semantics

| Semantics | Questions to Clarify |
| --- | --- |
| Lifecycle | Creation, initialization, execution, destruction |
| Execution order | Sequential relationship among multiple processing steps |
| State consistency | When to read, when to write, whether transactional |
| Dependency relationship | How dependencies are declared, resolved, and validated |
| Conflict handling | How to decide when multiple results conflict |
| Concurrency / Reentrancy | Whether the same object can be processed simultaneously |
| Rollback / Recovery | How state is handled after failure |
| Cache / Invalidation | What can be cached, when it becomes invalid |

### 11.4 Outputs

* Lifecycle definition
* Execution order description
* State read/write rules
* Dependency resolution rules
* Conflict handling rules
* Concurrency and reentrancy rules
* Rollback and recovery strategy

---

## 12. Layer 8: Failure Model

### 12.1 Goal

Design both success paths and failure paths simultaneously. Failure paths often determine system quality more than normal paths.

### 12.2 Core Questions

```text
How are missing input, invalid input, configuration errors, missing dependencies, circular dependencies, conflicts from multiple sources, version incompatibility, external system failures, and partial success handled respectively?
Should the system roll back after failure?
Is degradation allowed?
How are errors located and exposed to users?
```

### 12.3 Failure Model Table

| Failure Type | Detection Timing | System Behavior | Interrupts Execution | Recoverable | External Error |
| --- | --- | --- | --- | --- | --- |
| Missing input | Edit-time / Load-time / Runtime | Default / Skip / Error | Yes / No | Yes / No | Clear error |
| Invalid input | Load-time / Runtime | Reject / Degrade | Yes / No | Depends | Input location |
| Conflicting input | Load-time / Runtime | Priority / Merge / Reject | Yes / No | Depends | Conflict source |
| Invalid configuration | Load-time | Reject loading | Yes | Yes | Configuration location |
| Circular dependency | Load-time / Runtime | Reject / Abort | Yes | Yes | Dependency chain |
| Version incompatibility | Load-time | Migrate / Reject | Depends | Depends | Version description |

### 12.4 Outputs

* Failure classification
* Error codes or error objects
* Degradation strategy
* Rollback strategy
* Error location information
* Failure tracing mechanism

---

## 13. Layer 9: Engineering Constraint Validation

### 13.1 Goal

Ensure the system is not only conceptually sound, but also implementable, testable, maintainable, and optimizable.

### 13.2 Core Questions

```text
Which paths are high-frequency paths?
Which processing must be pre-computed?
Which results can be cached, and when does the cache expire?
Does debugging capability affect performance?
What is the maximum scale?
What are the platform limitations?
What are the memory and performance budgets?
How is the system tested and regression-verified?
```

### 13.3 Validation Content

* Performance budget
* Memory budget
* Platform limitations
* Thread model
* Hot path cost
* Caching strategy
* Precompilation strategy
* Debugging overhead
* Testing approach
* Deployment approach
* Version upgrade
* Compatibility strategy

### 13.4 Outputs

* Performance targets
* Resource budgets
* Hot path analysis
* Caching and precompilation strategy
* Testing strategy
* Platform adaptation description
* Engineering risk inventory

---

## 14. Layer 10: Role Workflow and Responsibility Attribution

### 14.1 Goal

Verify that the key subjects of responsibility in the system lifecycle are clear, and that the system supports different responsibility subjects in completing their respective work closed-loop.

### 14.2 Primary Roles

| Primary Role | Core Perspective | Core Question |
| --- | --- | --- |
| System Designer | Defines the system | What the system should be, what it should not be, and how it should evolve |
| Core Implementer | Implements the system | How to implement the system correctly, stably, performantly, and maintainably |
| System User | Uses the system | How externals use the system to achieve their own goals |
| Product End User | Perceives the result | Whether the final product truly solves the end user's problem |

### 14.3 Responsibility Domains by Role

| Primary Role | Responsibility Domain | Deliverables |
| --- | --- | --- |
| System Designer | System positioning, boundary governance, core abstraction, runtime semantics principles, interface principles, failure model principles, extension governance principles, evolution governance | System positioning, goals/non-goals, boundary definition, core concept model, principles-based design, version strategy |
| Core Implementer | Core mechanism implementation, interface implementation, runtime implementation, configuration and data loading, failure handling, observability and debugging, testing and validation, performance stability, version compatibility, engineering tools | Core modules, API/SDK, runtime, loader, error objects, trace/log/replay, testing tools, migration tools, editor/validator/previewer |
| System User | Integration and onboarding, configuration/content production, business consumption, extension development, user-side validation, user-side maintenance | Adapter layer, configuration, rules, content packages, consumption logic, plugins, integration tests, business acceptance, migration records |
| Product End User | Goal achievement, interaction experience, result trustworthiness, exception awareness, long-term feedback | User task completion, feedback paths, explainability feedback, exception feedback, usage data and frequent issues |

### 14.4 Cross-Role Horizontal Responsibility Domains

Horizontal responsibility domains are not independent roles, but responsibilities that span multiple roles. Primary responsibility and collaboration relationships must be clarified.

| Horizontal Responsibility Domain | Primary Responsibility | Collaboration |
| --- | --- | --- |
| Testing and validation | Core Implementer / System User | System Designer defines standards; Product End User provides feedback |
| Debugging and troubleshooting | Core Implementer provides capabilities; System User locates user-side issues | System Designer defines attribution principles |
| Performance stability | System Designer defines budgets; Core Implementer implements budgets | System User provides scale scenarios |
| Version governance | System Designer defines principles; Core Implementer implements mechanisms | System User performs adaptation |
| Documentation synchronization | System Designer maintains design baseline; Core Implementer maintains engineering documentation | System User maintains user-side documentation |
| Tooling support | Core Implementer | System User provides feedback on requirements |
| Experience validation | Product End User provides feedback | System User and System Designer digest feedback |

### 14.5 Simplest Judgment

```text
The System Designer is responsible for whether the definition is correct.
The Core Implementer is responsible for whether the implementation is reliable.
The System User is responsible for whether the usage is valid.
The Product End User is responsible for whether the final value is realized.
```

---

## 15. Layer 11: Extension and Governance

### 15.1 Goal

Support extension while governing it. Extensions without governance can inversely undermine core stability.

### 15.2 Core Questions

```text
How is the system extensible?
How are extensions registered, loaded, isolated, disabled, and rolled back?
Do extensions have namespace, permission boundaries, dependency declarations, and version constraints?
How are conflicts between extensions handled?
What can extensions override, and what can they not override?
Is the source of extensions traceable?
```

### 15.3 Key Principles

```text
The extension mechanism belongs to the core.
Extension content does not belong to the core.
Extension governance must belong to the core.
```

### 15.4 Outputs

* Extension mechanism description
* Extension boundary
* Namespace rules
* Dependency declaration rules
* Override and priority rules
* Permission and isolation rules
* Extension version compatibility rules
* Extension disable and rollback mechanism

---

## 16. Layer 12: Versioning Solidification

### 16.1 Goal

Solidify the results of each round of discussion into maintainable, reviewable, and traceable design assets. Documentation is not merely a record of results; it is a tool for governing system evolution.

### 16.2 Core Questions

```text
What was revised in this round, and why?
Which use cases are affected?
Does it change system positioning, boundaries, core concepts, interface contracts, or runtime semantics?
Does the old design need to be migrated?
Are deprecation notices retained?
```

### 16.3 Recommended Documentation to Solidify

* System design baseline
* Use case analysis document
* System boundary document
* Core concept document
* Interface contract document
* Runtime semantics document
* Failure model document
* Engineering constraint document
* Role workflow document
* Extension specification document
* Version migration guide
* Change log

### 16.4 Outputs

* Versioned design baseline
* Change log
* Impact scope description
* Deprecation notice
* Migration guide
* Open issues list

---

## 17. General Design Checklist

### 17.1 Scenarios and Abstraction

```text
Have sufficiently realistic scenarios been collected?
Do they cover normal, boundary, and exceptional paths?
Have high-frequency scenarios, low-frequency critical scenarios, and future expansion scenarios been identified?
Has a common structure been extracted from the scenarios?
Has business vocabulary been stripped away and stable concepts identified?
Have scenario-specific special cases been avoided?
```

### 17.2 Aesthetics and Boundary

```text
Is the system simple, clear, self-consistent, and self-explanatory?
Are concepts orthogonal and mechanisms composable?
Are layers well-defined and dependency directions single?
Are core semantics closed and expressions stable?
Is behavior predictable, are results traceable, and are failures explicit?
Do default behaviors follow least surprise and safe by default?
Is extension open but controlled, and is complexity gradually unfolded?
Are core mechanisms unified and external expressions flexible?
Is system positioning clear?
Are core responsibilities minimal and stable?
Are external responsibilities clear?
Is there responsibility bloat or contamination of the core by external domain semantics?
```

### 17.3 Semantic Attribution

```text
Does this semantics define the core system itself, or does it define the external use of core capabilities?
Does it belong to core ontology, runtime, interface, tool, or governance semantics?
Is it merely an interpretation of core results by external business, process, presentation, context, or product experience?
Is there a problem of judging semantic attribution only by literal word?
```

### 17.4 Interface, Runtime, and Failure

```text
Are inputs, outputs, invocation timing, error behavior, and dependable behaviors clear?
Are interfaces testable and version-compatible?
Are lifecycle, execution order, state changes, dependencies, and conflicts clear?
Can the system recover or degrade after failure?
Are errors locatable, traceable, and explainable?
```

### 17.5 Engineering, Roles, and Governance

```text
Are performance budgets, hot paths, caching, precompilation, and debugging overhead clear?
Are testing and regression strategies clear?
Are the responsibilities of the four primary roles clear?
Do horizontal responsibility domains have primary and collaborating parties?
Are extension mechanisms, namespaces, permissions, overrides, conflicts, version compatibility, and migration defined?
Are documents versioned, and is the impact of changes traceable?
```

---

## 18. Final Methodology Summary

This methodology can be compressed into five loops:

```text
From scenarios to abstraction: real scenarios → commonality extraction → stable abstraction.
From abstraction to aesthetics: simple, orthogonal, clear, self-consistent, predictable, traceable.
From aesthetics to boundary: clear positioning → clear semantic attribution → minimal and stable core responsibilities.
From boundary to runtime: clear interfaces → clear timing → clear state → clear failures.
From runtime to governance: controllable performance → role closed-loop → controlled extension → evolvable versions → traceable documentation.
```

One-sentence version:

> Use real-world scenarios to discover problems, use commonality extraction to derive abstractions, use aesthetic preferences to constrain structural quality, use semantic attribution to clarify interpretive authority, use boundary governance to control complexity, use runtime semantics to ensure correctness, use engineering constraints to ensure implementability, use role workflows to ensure responsibility closed-loop, use extension governance to ensure long-term evolution, and use versioned documentation to solidify consensus.

Shortest version:

> Scenario-driven, abstraction convergence, aesthetic calibration, semantic attribution, boundary governance, runtime validation, engineering implementation, role closed-loop, long-term evolution.
