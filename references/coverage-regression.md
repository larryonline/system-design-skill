# Use Case Coverage and Regression Mechanism

> In interactive design mode, load this document on demand when a use case table file exists.

## Logic Block Coverage Check

After completing each logic block, following the design baseline write:

1. Read the use case table file to obtain the full list of use cases
2. Check each use case against the current logic block's design decisions to verify whether it is supported
3. Output the coverage conclusion:
   - Full coverage: brief confirmation
   - Gaps exist: list the uncovered use case IDs, mark them in the "Pending Issues" section of the design baseline, and provide remediation directions

## Automatic Regression After Use Case Changes

When the skill assists the user in making changes to the use case table (adding, modifying, or deleting use cases) during the interaction, automatically perform regression:

1. Read all sections of the design baseline file
2. Traverse all use cases and check coverage against each design dimension:
   - System Positioning and Boundaries: Do new use cases fall within existing boundaries? Are there out-of-bounds use cases?
   - Core Abstraction: Can the existing abstractions express the new use cases?
   - Interface Contract: Can the existing interfaces support the inputs and outputs of the new use cases?
   - Runtime Semantics and Failure Model: Does runtime behavior still cover the normal and exception paths of the new use cases?
   - Engineering Constraints: Do the new use cases introduce new performance, resource, or platform constraints?
3. Output a regression report: list the affected use case IDs and gap descriptions for each design dimension
4. Automatically write gaps into the "Pending Issues" section of the design baseline
5. For gaps that can be auto-repaired (such as merely supplementing UC-ID references), directly update the corresponding section
