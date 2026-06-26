# Logic Block 2: Abstraction → Failure

> Corresponds to Methodology Sections 9-12

## Section 9: Core Abstraction Design

### Objective
Cover as many scenarios as possible with as few, stable, and clear core concepts as possible. Core abstraction is not about splitting modules; it is about defining the system's own language.

### Core Questions

- What are the minimum core concepts the system needs?
- What is the responsibility of each concept?
- What are the relationships between concepts?
- Which concepts belong to definition-time, runtime, input, output, process, or tracing information?
- Which concepts are merely external interpretations?

### Abstraction Principles

| Principle | Meaning |
| --- | --- |
| Determine abstraction attribution by system positioning | Judge attribution not by "who could do it" but by "who should be responsible" |
| Determine right of interpretation by semantic attribution | Core explains core system semantics; external explains external domain semantics |
| Prefer structural concepts over business concepts | Prioritize cross-scenario concepts such as input, state, rule, condition, computation, result, event, dependency, conflict, priority, lifecycle, tracing |
| Prefer unified mechanism expression over scenario-specific expression | Commonalities enter the mechanism; differences enter configuration, rules, extensions, or external interpretation |
| Core does not understand external business meaning, but understands its own operational rules | Lifecycle, execution order, dependencies, conflicts, state consistency, errors, versioning, tracing belong to core runtime semantics |
| External is responsible for using results; core is responsible for ensuring result semantic stability | External determines the purpose of results; core guarantees what the result is, how it is produced, whether it is valid, and whether it can be traced |
| Combine, do not bloat | New requirements should first be expressed through combination of existing concepts and mechanisms; only add a new concept when genuinely new stable core semantics emerge |
| Abstraction serves long-term stability | Abstraction must balance stability, comprehensibility, implementability, extensibility, debuggability, maintainability, and cost of use |

### Judgment Sequence for Adding New Core Concepts

```
Can existing concepts express it?
Can existing mechanisms combine to express it?
Is it merely a configuration difference?
Is it merely an external interpretation difference?
Has genuinely new stable core semantics truly emerged?
```

### Deliverables
- Core concept model
- Concept relationship description
- Concept naming conventions
- Abstraction attribution judgment rules
- Classification of definition-time, runtime, input, output, and tracing

---

## Section 10: Interface Contract

### Objective
Transform system boundaries into executable, testable, and dependable interface contracts.

> Boundaries answer: who is responsible for what. Interfaces answer: how they interact.

### Core Questions

- What capabilities does the system expose externally?
- What are the inputs, outputs, callers, and invocation timing?
- Synchronous or asynchronous?
- Is it idempotent?
- How are failures expressed?
- How are versions compatible?
- Which behaviors can external systems depend on?
- Which are merely internal implementation details?

### Interface Contract Table

| Interface | Caller | Callee | Input | Output | Timing | Error Behavior | Stability |
| --- | --- | --- | --- | --- | --- | --- | --- |

### Deliverables
- External interface inventory
- Input/output models
- Invocation timing description
- Error contracts
- Idempotency description
- Stability commitments
- Version compatibility rules

---

## Section 11: Runtime Semantics Design

### Objective
Move from static architecture to dynamic execution, clarifying how the system works along the time dimension. Many systems fail not because the architecture diagram is wrong, but because runtime semantics are not clearly defined.

### Core Questions

- When does the system initialize, load configuration, receive input, execute processing, update state, output results, and clean up resources?
- Does it support pause, resume, rollback?
- What happens when multiple inputs arrive simultaneously?
- What happens when multiple rules match simultaneously?
- What happens when multiple states update simultaneously?

### Common Runtime Semantics

| Semantic | Questions to Clarify |
| --- | --- |
| Lifecycle | Create, initialize, run, destroy |
| Execution Order | Sequential relationship among multiple processing steps |
| State Consistency | When to read, when to write, whether transactional |
| Dependency Relationships | How dependencies are declared, resolved, and validated |
| Conflict Handling | How to decide when multiple results conflict |
| Concurrency / Reentrancy | Whether the same object can be processed simultaneously |
| Rollback / Recovery | How state is handled after failure |
| Cache / Invalidation | What can be cached, when it becomes invalid |

### Deliverables
- Lifecycle definition
- Execution order description
- State read/write rules
- Dependency resolution rules
- Conflict handling rules
- Concurrency and reentrancy rules
- Rollback and recovery strategy

---

## Section 12: Failure Model

### Objective
Design both success paths and failure paths simultaneously. Failure paths often determine system quality more than normal paths.

### Core Questions

- How are missing input, invalid input, configuration errors, missing dependencies, circular dependencies, conflicts from multiple sources, version incompatibility, external system failures, and partial success handled respectively?
- Should rollback occur after failure?
- Is degradation allowed?
- How are errors located and exposed to users?

### Failure Model Table

| Failure Type | Detection Timing | System Behavior | Interrupts? | Recoverable? | External Error |
| --- | --- | --- | --- | --- | --- |
| Missing Input | Edit-time / Load-time / Runtime | Default / Skip / Error | Yes / No | Yes / No | Clear error |
| Invalid Input | Load-time / Runtime | Reject / Degrade | Yes / No | Depends | Input location |
| Conflicting Input | Load-time / Runtime | Priority / Merge / Reject | Yes / No | Depends | Conflict source |
| Invalid Configuration | Load-time | Reject loading | Yes | Yes | Configuration location |
| Circular Dependency | Load-time / Runtime | Reject / Abort | Yes | Yes | Dependency chain |
| Version Incompatibility | Load-time | Migrate / Reject | Depends | Depends | Version description |

### Deliverables
- Failure classification
- Error codes or error objects
- Degradation strategy
- Rollback strategy
- Error location information
- Failure tracing mechanism
