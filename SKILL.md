---
name: de-slopify
description: Simplify existing code or recent changes by removing unnecessary complexity, redundant abstractions, and misleading noise while preserving behavior. Use for de-slopifying, removing AI code slop, or a deliberate code simplification pass. Supports uncommitted changes, branch diffs, and file or codebase snapshots; respects review-only requests. Not a substitute for feature development or a general bug/security audit.
---

# De-slopify Code

Make the selected code easier to understand and change. Judge the code's actual maintenance cost, not whether it looks AI-generated. A successful pass can make no edits.

Use the spirit of The Pragmatic Programmer, Clean Code, and the Zen of Python as decision aids. Prefer repository and language conventions over mechanical application of book advice. For source provenance, consult [references/principles.md](references/principles.md); routine use does not require browsing or rereading the sources. When a candidate touches dependencies, contracts, resource ownership, configuration, concurrency, or algorithms, read the relevant section of [references/structural-refactoring.md](references/structural-refactoring.md).

## Establish the target

Follow the user's requested mode. Simplification requests authorize implementing local improvements; review, audit, or plan-only requests produce recommendations without editing. Preserve any already-authorized broader work.

Use the explicit paths or comparison when provided. Otherwise infer the target from the active task: recent work means the relevant diff; a named module or whole codebase means its snapshot. If materially different targets remain plausible, inspect enough to identify them, then clarify before editing.

| Target | Scope and evidence |
| --- | --- |
| Uncommitted changes | Inspect staged and unstaged diffs separately and inventory relevant untracked files. Simplify the selected changes plus the minimum adjacent code needed for coherence. Preserve unrelated edits and staging decisions. |
| Branch diff | Resolve the exact requested base ref, compute its merge base with HEAD, and inspect the committed diff from that merge base to HEAD. Do not silently substitute the base's upstream or include local edits. Read current files for context; if local edits overlap a proposed patch, preserve them and verify the combined result. If the ref or merge base cannot resolve, report that rather than inventing a comparison. |
| Snapshot | Inspect current code in the selected files, folders, or repository. History is context, not an eligibility filter. Exclude generated, vendored, and build output unless specifically targeted; change their source or generator when appropriate. |

Read applicable AGENTS.md, build/test configuration, and existing conventions. Look for relevant SIMPLIFY_GUIDELINES.md without requiring a .pi directory. If only REVIEW_GUIDELINES.md is present, use applicable engineering constraints; do not let review-only output instructions change an implementation request. Resolve conflicts using the user's current scope and applicable instruction hierarchy.

Record the initial working-tree state and available checks. Trace affected callers, data flow, and contracts before deciding a structure is redundant. In a large scope, work through coherent areas and state any coverage limits.

## Choose changes that earn their cost

For each candidate, identify the concrete burden, the simpler replacement, and the behavior at risk. Test the benefit against a realistic change suggested by current requirements or callers: what would a maintainer need to understand, edit, and verify before versus after? Favor localized changes and replaceable components. Discard edits justified only by taste, a slogan, a metric, or an imagined future architecture.

| Candidate | Decision rule |
| --- | --- |
| Forwarding layers, factories, interfaces, or generic helpers | Reuse or inline when a layer adds no useful domain meaning or boundary. Retain adapters, compatibility surfaces, framework hooks, and test seams that serve a real purpose. One implementation alone does not prove an interface is useless. |
| Repeated logic | Consolidate when sites express the same rule and should change together. Similar syntax for independently evolving concepts can remain separate. Avoid creating a parameter-heavy universal helper. |
| Long or deeply nested logic | Use clear conditions, guard clauses, and named concepts when they reduce the reader's mental work. Keep cohesive code together; do not scatter a readable sequence into tiny functions merely to shorten it. Preserve evaluation order and cleanup. |
| Misleading names or comments | Check names at their call sites against domain vocabulary; make units, state, and effects clear. Preserve externally bound names. Remove obsolete narration and commented-out code after checking relevance. Retain rationale, contracts, constraints, and explanations of surprising behavior. |
| Apparently dead code or dependencies | Check callers, exports, configuration, dynamic registration, reflection, templates, and supported compatibility paths as relevant. Absence from text search alone is not proof of non-use. |
| Repeated state or derived values | Prefer one owner of a fact. Keep deliberate caches or denormalization when justified, with their consistency rules intact. Preserve measured optimizations. |
| Defensive checks, catches, defaults, and fallbacks | Verify the input and error contracts before removing anything. Preserve boundary validation and intentional recovery. A swallowed failure or misleading success value may be a bug; do not change that behavior under a cleanup-only request. |
| Excess machinery in tests | Retain tests of observable contracts and independent expected results. Difficult setup can reveal hidden dependencies; investigate those without automatically adding test-only abstractions. Simplify redundant setup or mocks without losing meaningful cases. |

Prefer an existing idiom or direct implementation before adding a dependency, abstraction, or configuration option. Count the total understanding cost across callers and helpers, not just lines removed from one function.

For structural edits, locate invariant enforcement, state ownership, and required ordering. A thin layer may isolate vendor knowledge, protect an atomic operation, or balance resource lifetimes. Prefer explicit local data flow when it removes hidden coordination without moving those guarantees. Trace an odd workaround to its rationale or runtime contract before deleting it; passing examples alone do not prove the underlying assumption.

## Apply and verify

Implement useful changes in coherent, reviewable batches. Preserve outputs, API shapes, persisted data, ordering, side effects, error behavior, resource lifetimes, and relevant performance or concurrency guarantees. An apparently tiny bug fix is still a behavior change: include it only if the user's scope already authorizes it, identify it separately, and verify it as a fix. Otherwise report the concrete issue as deferred and continue safe cleanup.

Run the repository's required checks and relevant existing tests for the affected paths. Where behavior is poorly captured and the refactor has real uncertainty, add a focused characterization or contract test before changing it. Use relevant invariants or state combinations when examples alone leave a material gap, and retain discovered counterexamples as reproducible cases. Do not add tests that merely mirror trivial implementation details. Check applicable boundary and failure cases; record baseline failures so pre-existing problems are not attributed to the cleanup.

When a candidate changes loops, queries, caching, or materialization, compare runtime and memory growth at expected input sizes. Measure representative cases when the tradeoff matters; a shorter expression is not evidence of acceptable cost.

If execution is unavailable, inspect the diff and contracts, state the validation gap, and limit changes to what that evidence supports. Defer an uncertain transformation rather than weakening checks or claiming equivalence without evidence.

Inspect the final diff against the starting state and selected scope. Remove churn, speculative helpers, unrelated formatting, and accidental behavior changes introduced by the pass. Do not treat reduced line count, more functions, fewer comments, or a clean linter as proof of improvement. Stop when further changes would be cosmetic, speculative, or harder to verify than their benefit warrants.

## Report the result

Keep the report proportional to the work:

- State the scope and the important completed changes, with concrete reasons they simplify maintenance.
- Report checks actually run, their results, and material validation or coverage limits.
- Mention only worthwhile deferred issues; distinguish behavior changes from refactors.
- If no edit is justified, say so and identify what was inspected.

For review-only work, give actionable locations, the maintenance burden, and a proposed simplification; do not imply changes were applied. Describe completed work in the past tense so a later agent does not repeat it.
