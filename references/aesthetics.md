# System Design Aesthetic Preferences

## Definition

System design aesthetic preferences are quality orientations that permeate scenario analysis, abstraction design, boundary governance, interface design, runtime semantics, engineering implementation, extension governance, and version evolution. They are not local style choices but fundamental criteria for design trade-offs.

## Core Preferences

| Preference | Meaning | Evaluation Focus |
| --- | --- | --- |
| Simple | Keep only necessary concepts and mechanisms | Can it be expressed with existing concepts; is an overly heavy structure introduced for a few special cases |
| Clear | Layers, responsibilities, boundaries, dependencies, and interfaces are well-defined | Is responsibility attribution clear; what can externally be depended on; what is hidden internally |
| Self-consistent | Concepts, boundaries, runtime semantics, and failure models are not contradictory | Are definitions, behavior, interfaces, failure, and governance consistent |
| Self-explanatory | Concepts, outputs, errors, and trace information can explain themselves | Are result sources, error causes, configuration effects, and interface promises understandable |
| Concept Orthogonality | Core concepts have minimal overlap | Is there overlapping responsibility; can it be expressed through composition |
| Composable | Combine existing mechanisms to create new capabilities | Does a new requirement call for new core semantics or can it be composed from existing mechanisms |
| Clear Layering | Each layer only handles its own concerns | Does the lower layer understand higher-layer business; does the higher layer bypass lower-layer mechanisms |
| Unidirectional Dependency | Dependency direction is stable and predictable | Are there reverse dependencies, circular dependencies, or dependency bypassing |
| Semantic Closure | The semantics of core promises can be explained, executed, traced, verified, and governed | Do all core definitions have runtime semantics and governance rules |
| Stable Expression | Core language and mechanisms are stable over the long term | Is it merely a transient business term; is it suitable as core language |
| Predictable | Output is reproducible when inputs, state, and rules are clear | Are execution order, conflict handling, and failure behavior clearly specified |
| Traceable | Key results have sources, processes, and attribution | What was read, what was matched, and why that result was produced |
| Explicit Failure | Failures are classified, exposed, and handled | How are absence, illegality, conflicts, and version incompatibilities handled |
| Least Surprise | Behavior matches user intuition | Is the default behavior natural; is exceptional behavior clearly communicated |
| Open but Controlled | Extensible, but constrained by boundaries, permissions, version, and conflict rules | What extensions can and cannot do, and how to roll back |
| Progressive Complexity | Simple scenarios are expressed simply; complex capabilities are revealed on demand | Are the entry path and advanced path clear |
| Local Understandability | Modifying a local part does not require understanding the whole | Can configurations, components, and extensions be validated locally |
| Secure by Default | Default paths are safe, stable, and controllable | Are high-risk capabilities explicitly opt-in |
| Unified Mechanism, Diverse Expression | Core mechanisms are uniform; peripheral expression is flexible | Does the core bloat due to differences in expression |

## Summary

> A good system should use a small set of stable, orthogonal, and composable core concepts to form a simple, clear, self-consistent, predictable, traceable, and evolvable structure; keeping simple scenarios simple, enabling controlled extension of complex capabilities, unifying core mechanisms, and allowing flexible external expression.

A shorter expression:

> Core is simple and self-consistent, boundaries are clear and stable, behavior is predictable and traceable, and extension is open but controlled.
