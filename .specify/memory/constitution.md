<!--
Sync Impact Report
Version change: unratified template -> 1.0.0 (initial adoption)
Modified principles: all five unnamed template principles replaced with:
- I. UX First
- II. Input Validation and Actionable Feedback
- III. Consistent Coding Conventions
- IV. Clear Architecture
- V. Complete and Current Documentation
Added sections: Quality Standards; Development Workflow and Review
Removed sections: none; generic template slots populated.
Deferred TODOs: none.
Dependent templates and commands: unchanged; read this constitution at runtime.
Review note: remove this temporary report before committing the constitution.
-->
# PythonProject Constitution

## Core Principles

### I. UX First

Every feature MUST define the user's goal and acceptance scenarios before implementation.
User flows MUST use consistent terminology, make available actions understandable, and provide
observable outcomes for success, failure, and any waiting state. Reviews MUST verify that the
primary flow and recovery from expected errors can be completed without reading source code.
Design decisions MUST prioritize user task completion and understandable interactions.

### II. Input Validation and Actionable Feedback

All user inputs MUST be validated before they are used to change application state or trigger
an operation. Validation MUST cover required values, types, formats, permitted ranges, and
applicable business rules. Each input MUST have explicit rules, including whether empty values
are allowed. Invalid input MUST prevent the affected operation and produce feedback identifying
the problem and how to correct it. Recoverable errors MUST preserve valid input where applicable.
Successful operations MUST provide clear confirmation; technical tracebacks MUST NOT serve as
user-facing error messages. Validation at the trusted application boundary MUST remain effective
regardless of any earlier interface checks.

### III. Consistent Coding Conventions

Python code MUST follow PEP 8 naming and formatting conventions and use descriptive names.
Changes MUST follow established project conventions; when none exist, the first implementation
MUST document the selected conventions. Functions and classes MUST have a clear responsibility.
Duplicate business rules MUST be consolidated, and expected failures MUST be handled explicitly
rather than silently ignored. Reviews MUST check readability, consistency, and error handling.

### IV. Clear Architecture

User interaction, business rules, and external data access MUST have distinct responsibilities.
Business rules MUST be verifiable independently of the user interface and external services.
Module dependencies MUST have an explicit direction and MUST NOT introduce circular dependencies.
New abstractions and dependencies MUST address a documented current requirement. Architecture
changes MUST document responsibilities, dependency direction, and significant tradeoffs so that
maintainers can evaluate the design without reconstructing it from implementation details.

### V. Complete and Current Documentation

Every module, class, function, and method MUST have documentation describing its purpose.
Callable documentation MUST state parameters, return values, expected errors, and side effects
where applicable. Non-obvious logic MUST explain its rationale in comments. Project documentation
MUST explain setup, execution, verification, architecture, and user-facing workflows, including
input constraints and recovery behavior. Code and behavior changes MUST update affected
documentation in the same change. Documentation MUST match actual behavior; redundant comments
that merely restate individual statements do not satisfy this principle.

## Quality Standards

A feature's acceptance criteria MUST cover its primary user journey, successful completion,
invalid input, boundary values, and expected failure recovery. Every user input MUST be mapped
to its validation rules and feedback expectations. Verification MUST demonstrate that rejected
input does not trigger the affected operation or corrupt existing state.

Automated checks MUST cover business rules, input validation, and error behavior introduced or
changed by the feature. User-facing flows MUST also be reviewed for clarity and consistency.
Documentation completeness and architectural boundaries MUST be checked during review.

## Development Workflow and Review

Before implementation, specifications MUST describe user outcomes and acceptance scenarios,
and plans MUST explain architectural boundaries and relevant conventions. Tasks MUST include
validation, feedback, documentation, and verification work required by the feature.

Before a change is accepted, the author MUST record the checks performed and their results.
Review MUST assess all five principles, confirm documentation matches behavior, and identify
any unresolved defects. An unresolved violation MUST be corrected before acceptance unless a
specific exception has been approved and recorded under Governance.

## Governance

This constitution is the authoritative project governance document. Specifications, plans,
tasks, code reviews, and implementation decisions MUST be assessed against it. Existing code
MUST be brought into compliance when changed; unrelated existing gaps MUST be recorded for
follow-up rather than silently treated as compliant.

Amendments MUST record the proposed wording, rationale, impact on existing work, and any
migration required. A project maintainer MUST approve an amendment before it becomes governing
policy. Amendments MUST update the version and last-amended date while preserving the original
ratification date.

Versions MUST follow semantic versioning: MAJOR for incompatible principle removals or
redefinitions, MINOR for new principles or materially expanded guidance, and PATCH for wording
or clarification changes that do not alter obligations.

Exceptions MUST identify the affected rule, rationale, scope, approving maintainer, and an
expiry or follow-up condition. Reviewers MUST verify that an exception remains applicable
before relying on it. Templates and commands read this constitution at runtime and MUST NOT be
edited solely to duplicate its contents.

**Version**: 1.0.0 | **Ratified**: 2026-11-12 | **Last Amended**: 2026-11-12
