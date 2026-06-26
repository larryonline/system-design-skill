# General Design Checklist

## Scenario & Abstraction

- Have enough realistic scenarios been collected?
- Are normal, boundary, and error paths covered?
- Are high-frequency scenarios, low-frequency critical scenarios, and future extension scenarios identified?
- Has common structure been extracted from the scenarios?
- Has business jargon been stripped away and stable concepts identified?
- Have special-case designs for individual scenarios been avoided?

## Aesthetics & Boundaries

- Is the system simple, clear, self-consistent, and self-explanatory?
- Are concepts orthogonal and mechanisms composable?
- Is layering clear and dependency unidirectional?
- Is core semantics closed and expression stable?
- Is behavior predictable, are results traceable, and is failure explicit?
- Do defaults conform to the principle of least surprise and secure by default?
- Is extension open but controlled, and is complexity progressively revealed?
- Are core mechanisms unified and external representations flexible?
- Is the system's positioning clear?
- Is the core responsibility minimal and stable?
- Are external responsibilities clear?
- Is there responsibility bloat or contamination of the core by external domain semantics?

## Semantic Attribution

- Does this semantics define the core system itself, or an external use of a core capability?
- Does it belong to core ontology, runtime, interface, tool, or governance semantics?
- Is it merely an interpretation of core results by external business, process, presentation, context, or product experience?
- Is there a problem of judging semantic attribution solely by surface-level wording?

## Interface, Runtime & Failure

- Are inputs, outputs, invocation timing, error behavior, and dependable behavior clearly specified?
- Is the interface testable and version-compatible?
- Are lifecycle, execution order, state transitions, dependencies, and conflicts clearly specified?
- Is recovery or graceful degradation possible after failure?
- Are errors localizable, traceable, and explainable?

## Engineering, Roles & Governance

- Are performance budgets, hot paths, caching, precompilation, and debugging overhead clearly specified?
- Are testing and regression strategies clearly specified?
- Are the responsibilities of the four main role types clear?
- Does each cross-cutting responsibility domain have a clear owner and collaborators?
- Are extension mechanisms, namespaces, permissions, overrides, conflicts, version compatibility, and migration defined?
- Is documentation versioned, and is the impact of changes traceable?
