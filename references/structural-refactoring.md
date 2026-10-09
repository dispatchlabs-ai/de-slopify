# Structural refactoring decisions

Read only the sections relevant to a proposed simplification. These are original applications of The Pragmatic Programmer, 20th Anniversary Edition, to the skill's behavior-preserving scope. Topic numbers identify the source discussion; they are not extra tasks or authority to redesign the project.

## Dependencies and change boundaries

Use when removing a layer, changing inheritance, or untangling hidden state. Source topics: 8, The Essence of Good Design; 10, Orthogonality; 11, Reversibility; 28, Decoupling; 31, Inheritance Tax.

- Follow the knowledge a caller needs. An adapter that contains vendor semantics or a domain invariant can reduce coupling even if its implementation is short. Inlining it may scatter assumptions. Conversely, a forwarding layer that contains no meaningful knowledge may be removable.
- Prefer explicit, narrowly scoped inputs to hidden mutable context when that actually simplifies existing dependencies. Avoid replacing one global with a large context object passed everywhere.
- Distinguish inheritance for a supported polymorphic contract from inheritance used only to borrow implementation. Local composition may help the latter, but preserve dispatch, initialization, visibility, and framework contracts. Do not mandate an inheritance migration.
- A fluent transformation chain is not equivalent to navigating another component's private structure. Judge what must be known, not the number of dots or methods. Do not add forwarding methods just to satisfy a chain-length rule.

## Duplicated knowledge and configurable policy

Use when consolidating rules across code, schemas, generated artifacts, documentation, or configuration. Source topics: 9, DRY; 14, Domain Languages; 32, Configuration; 45, The Requirements Pit.

- Find the authoritative owner of the rule and all relevant in-scope representations. Reuse an existing schema or generation path where it prevents drift. Do not patch generated output or build a new generator merely to avoid a small amount of text.
- Keep independent checks independent: tests should not calculate expected results by calling the implementation under test. Similar client and server validation may protect different trust boundaries; matching text alone does not justify deleting either.
- Distinguish a domain invariant from an actual deployment or customer setting. Consolidate repeated interpretation of existing settings, preserving defaults, precedence, validation, read timing, and reload behavior. A module-level cached read can change a per-request policy.
- Use ordinary domain functions or existing data formats before introducing a DSL, parser, configuration service, or new setting. More configurable behavior is not automatically simpler.

## Contracts, errors, and resource ownership

Use when removing checks or catches, flattening control flow, or replacing lifecycle wrappers. Source topics: 23, Design by Contract; 24, Dead Programs Tell No Lies; 25, Assertive Programming; 26, How to Balance Resources.

- Identify caller obligations, return guarantees, and state invariants separately. Establish which code enforces each one. An expected calling convention does not prove a boundary check redundant; do not narrow accepted inputs or replace production validation with an assertion that may be disabled.
- Examine assertions for effects before moving or removing them. Work required for correctness cannot silently become conditional on assertion settings. Treat an existing assertion-dependent defect as a bug under the main skill's scope rule.
- Classify each catch by recovery, translation, cleanup, or diagnostics. A log-and-rethrow path may provide correlation or operational evidence; it is not automatically noise. Advice to fail early does not authorize replacing established fallbacks with new failures.
- Trace acquisition, partial failure, ownership transfer, early returns, exceptions, and cancellation. Retain borrowed-versus-owned distinctions, release order, and cleanup timing. Prefer an existing scope-bound idiom only when it preserves those guarantees, including for locks, transactions, timers, and subscriptions.

## Data flow and time

Use when replacing temporary fields, merging stages, simplifying asynchronous code, or changing synchronization. Source topics: 29, Juggling the Real World; 30, Transforming Programming; 33, Breaking Temporal Coupling; 34, Shared State Is Incorrect State; 35, Actors and Processes; 36, Blackboards.

- If temporary object fields merely pass results between steps, explicit local inputs and outputs may remove hidden coordination. Preserve aliasing and externally observed mutation. A loop can be clearer than a pipeline; no functional or reactive framework is required.
- If flags encode a lifecycle, establish existing states and transitions before considering a clearer representation. Preserve invalid-state handling, event delivery, and callback timing. Do not invent a state-machine framework for a straightforward branch.
- Preserve short-circuiting, evaluation counts, lazy versus eager work, and error propagation when rearranging transformations. Reading a property or enumerating a stream can have effects.
- Identify the complete protected operation. A check followed by an update must not become two separately locked actions; extracting or caching a read outside the critical section can change correctness. Shared state can live in files, services, or process configuration, not just object fields.
- Do not parallelize, remove awaits, or collapse message boundaries merely to reduce code. Account for ordering, cancellation, retries, partial completion, and rollback. Preserve schemas, ownership, and useful tracing at asynchronous boundaries.

## Evidence and computational cost

Use when a change relies on undocumented behavior or changes an algorithm's work. Source topics: 19, Version Control; 20, Debugging; 27, Don't Outrun Your Headlights; 38, Programming by Coincidence; 39, Algorithm Speed; 40, Refactoring.

- Name the assumption that makes the proposed change safe. Check it against actual callers, dependencies, supported environments, and focused history when a workaround's purpose is unclear. Successful observations do not establish a general guarantee. Do not turn this into routine repository archaeology or dependency upgrades.
- Size a batch so available feedback can establish its result before the next structural edit. For an uncertain integration boundary, exercise a representative path through it; isolated unit tests may miss the changed interaction.
- Compare work and storage at relevant input bounds: repeated scans, extra allocations, materialized streams, round trips, and cache invalidation can dominate shorter code. Benchmark when the decision depends on cost. A straightforward algorithm can be appropriate for bounded inputs; theoretical optimality is not the goal.

## Tests and useful feedback

Use when choosing evidence for an uncertain refactor or interpreting difficult test setup. Source topics: 41, Test to Code; 42, Property-Based Testing; 44, Naming Things; 48, The Essence of Agility; 50, Coconuts Don't Cut It; 51, Pragmatic Starter Kit.

- Test from the caller's view. Large fixtures or extensive mocking can indicate incidental dependencies; investigate the cause before adding interfaces or flags only to make tests possible.
- Choose properties that follow from the real contract, such as preservation of record order or round-trip behavior for supported inputs. Generated cases can supplement examples when the input space warrants them, preferably using existing tools. Keep a discovered failing input as a deterministic regression case.
- Check that a newly relied-on regression test can detect the failure it targets. Coverage percentages and counts of passing tests alone do not establish that meaningful states were exercised.
- Reconsider a change if its result is harder to explain, test, or modify than the starting point. Do not import the book's broader team practices, release processes, security projects, or product advice into a cleanup request.
