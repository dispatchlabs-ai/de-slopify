# Sources and interpretation

Consult this reference when explaining the skill's foundations or resolving a disputed cleanup choice. The full texts of both **The Pragmatic Programmer** and **Clean Code** were available and referenced in developing this skill. The full text of **The Clean Coder**, included in the supplied Clean Code Collection, was also reviewed. The source review was completed on 2026-10-09. The operational workflow is an original synthesis, not a claim that any one book prescribes it.

## The Pragmatic Programmer

Material consulted: Dave Thomas and Andy Hunt, *The Pragmatic Programmer: Your Journey to Mastery*, 20th Anniversary Edition, supplied EPUB version P3.0 (January 22, 2020). The full-text review covered all 53 numbered topics, introductions, postface, and appendices.

Application: judge design by how easily a real change can be made. Limit coupling, keep domain knowledge with a clear owner, preserve useful feedback, and work incrementally. Ask whether two sites should evolve together before merging them: similar syntax need not mean duplicated knowledge. Deliberate caching can be appropriate when consistency remains controlled.

The review informs the dependency, configuration, contract, ownership, temporal, scaling, and evidence checks in [structural-refactoring.md](structural-refactoring.md). Topic identifiers there locate the source discussions.

## Clean Code

Material consulted: Robert C. Martin and contributors, *Clean Code: A Handbook of Agile Software Craftsmanship*, first edition, ISBN 9780132350884, in *The Robert C. Martin Clean Code Collection*. The full-text review covered all 17 chapters, the successive-refinement, JUnit, and SerialDate case studies, the concurrency appendix, and textual front and back matter.

Application: make names, calls, responsibilities, and tests communicate their purpose. Inspect hidden effects, mode flags, output mutation, and implicit semantic dependencies. Choose data-oriented or object-oriented structure according to actual change needs. Preserve useful boundary adapters, absence and error distinctions, and clear test scenarios.

The case studies support small, verified iterations and reconsidering an extraction that makes the whole harder to understand. They also mix refactoring with behavior changes; parsing, error, API, and serialization changes still need authorization from the user's task. Function length, argument count, switch statements, comments, and assertion counts are signals to inspect, not automatic violations. Historical Java tooling and architectural examples are not requirements for other languages or current projects.

## The Clean Coder

Material consulted: Robert C. Martin, *The Clean Coder: A Code of Conduct for Professional Programmers*, ISBN 9780137081073, in the same collection. The full-text review covered all 14 chapters, the tooling appendix, and textual front and back matter.

Application: define what completion means for the requested work, retain proportionate verification under pressure, and report uncertainty honestly. Preserve test independence and distinguish unit, component, integration, and acceptance evidence when simplifying tests. The skill does not adopt the book's career expectations, scheduling practices, universal TDD prescriptions, or coverage targets as cleanup requirements.

## The Zen of Python

Material consulted: [PEP 20 in full](https://peps.python.org/pep-0020/#the-zen-of-python). It values explicitness, readability, understandable structure, deliberate error handling, and practical judgment. Its simplicity principles do not eliminate necessary domain complexity.

Application: favor direct control flow and clear contracts, resist dense tricks and hidden effects, and investigate uncertain semantics. These ideas transfer across languages; Python syntax and conventions do not automatically transfer with them. Making an error visible can alter behavior, so diagnose hidden failures separately when only refactoring is authorized.

## Coverage and source handling

The book reviews used complete supplied EPUBs. Embedded image-only listings, illustrations, and equations were not systematically inspected; this guidance relies on the full prose and text-rendered examples. The EPUBs, extracted text, and copied book listings are not part of this skill or its public repository. Routine use requires neither the books nor an external service.

## Workflow provenance

An existing PI simplification workflow informed the three target scopes, minimal adjacent edits for diffs, preference for reuse and deletion, acceptance of no-op results, and factual summaries of completed work. The original extension is not required to use this skill.

The Codex adaptation separates review from implementation, uses the exact requested Git base, distinguishes committed changes from local work, and preserves behavior without an incidental-bug-fix exception. Repository guidance does not require a .pi directory. Conversation navigation is omitted because a conversation branch does not isolate or revert filesystem changes.
