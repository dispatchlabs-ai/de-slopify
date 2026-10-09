# De-slopify Code

A Codex skill for simplifying existing code while preserving behavior. It targets unnecessary abstractions, duplicated rules, misleading names, noisy comments, and incidental complexity. A successful pass can make no edits.

## Install

Ask Codex:

```text
Use $skill-installer to install the skill at the root of
https://github.com/dispatchlabs-ai/de-slopify as de-slopify.
```

For manual installation, clone this repository into `$CODEX_HOME/skills/de-slopify`, or `~/.codex/skills/de-slopify` when `CODEX_HOME` is unset. The installed folder should contain `SKILL.md` directly.

## Use

```text
$de-slopify simplify my uncommitted changes.

$de-slopify simplify this branch against local main, committed changes only.

$de-slopify simplify the current code in src/billing while preserving behavior.

$de-slopify review src/billing for simplification opportunities without editing.
```

The skill follows repository guidance, preserves unrelated local work, and runs relevant checks. It checks whether repeated code expresses the same rule before consolidating it, preserves useful boundaries and comments, and keeps bug fixes separate unless they are already authorized. For structural changes, it examines contracts, resource ownership, configuration semantics, ordering, and performance tradeoffs. It does not impose function-length quotas or require an architectural rewrite.

## Contents

- [SKILL.md](SKILL.md): scope selection, cleanup decisions, verification, and reporting.
- [agents/openai.yaml](agents/openai.yaml): Codex display metadata and suggested prompt.
- [references/principles.md](references/principles.md): source material and interpretation.
- [references/structural-refactoring.md](references/structural-refactoring.md): conditional checks for dependencies, state, resource lifetimes, concurrency, algorithms, and tests.

The skill draws on a full-text review of *The Pragmatic Programmer*, 20th Anniversary Edition, public excerpts and author material for *Clean Code*, and [PEP 20](https://peps.python.org/pep-0020/), together with an existing PI simplification workflow. Source notes record coverage and limitations. The guidance is an original synthesis; no book files, PI extension, or external service are required.
