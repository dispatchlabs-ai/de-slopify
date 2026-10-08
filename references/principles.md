# Sources and interpretation

Consult this reference when explaining the skill's foundations or resolving a disputed cleanup choice. The operational workflow in SKILL.md is a synthesis, not a claim that any one source prescribes it. Research was performed on 2026-10-08 using public primary material; neither complete commercial book was read.

## The Pragmatic Programmer

Material consulted: the publisher's [100 tips from the 20th Anniversary Edition](https://store.pragprog.com/tips/) and its complete [public DRY chapter extract](https://media.pragprog.com/titles/tpp20/dry.pdf).

The tips connect maintainability with ease of change, limited coupling, accurate domain language, feedback, and incremental work. The DRY extract distinguishes repeated knowledge from code that happens to look alike: independent concepts need not share a function. It also allows deliberate cached representations when their consistency is encapsulated.

Application: ask whether two sites should evolve together before merging them. Prefer a simpler change path over an impressive abstraction. Do not erase useful caching or force unrelated responsibilities into a common helper.

## Clean Code

Material consulted: the contents and relevant chapter-one passages in the [first-edition publisher sample](https://www.informit.com/content/images/9780132350884/samplepages/9780132350884.pdf), plus public passages from the second edition's [First Principles excerpt](https://www.informit.com/articles/article.aspx?p=3222335). The first edition acknowledges other valid design approaches; the later excerpt explicitly treats its principles as contextual guidance.

Application: improve names, cohesion, and readability incrementally. Extract a meaningful concept when it helps the reader; impose neither a function-length quota nor a Java-style architecture on every language.

Additional author material supplies important counterweights:

- [Avoid Redundant Comments](https://www.informit.com/articles/article.aspx?p=1327761): comments that repeat visible code create noise. Remove repetition while keeping useful behavioral explanation.
- [Necessary Comments](https://blog.cleancoder.com/uncle-bob/2017/02/23/NecessaryComments.html): rationale and a timing diagram can carry information names cannot express. Preserve explanations of subtle ordering or concurrency.
- [Pattern Pushers](https://blog.cleancoder.com/uncle-bob/2015/07/05/PatternPushers.html): familiarity with patterns is not a reason to impose them. Require an actual problem before adding structural machinery.

## The Zen of Python

Material consulted: [PEP 20 in full](https://peps.python.org/pep-0020/#the-zen-of-python). It values explicitness, readability, understandable structure, deliberate error handling, and practical judgment. Its advice about ambiguity discourages guessing; its simplicity principles do not eliminate necessary domain complexity.

Application: favor direct control flow and clear contracts, resist dense tricks and hidden effects, and investigate uncertain semantics. These ideas transfer across languages; Python syntax and conventions do not automatically transfer with them. Making an error visible can alter behavior, so diagnose hidden failures separately when only refactoring is authorized.

## Workflow provenance

An existing PI simplification workflow informed the three target scopes, minimal adjacent edits for diffs, preference for reuse and deletion, acceptance of no-op results, and factual summaries of completed work. The original extension is not required to use this skill.

The Codex adaptation separates review from implementation, uses the exact requested Git base, distinguishes committed changes from local work, and preserves behavior without an incidental-bug-fix exception. Repository guidance does not require a .pi directory. Conversation navigation is omitted because a conversation branch does not isolate or revert filesystem changes.
