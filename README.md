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

The skill follows repository guidance, preserves unrelated local work, and runs relevant checks. It checks whether repeated code expresses the same rule before consolidating it, preserves useful boundaries and comments, and keeps bug fixes separate unless they are already authorized. It examines hidden effects at call sites, missing versus empty results, error contracts, resource ownership, configuration, ordering, and performance tradeoffs. Test cleanup preserves independent cases and meaningful evidence across boundaries. It does not impose function-length quotas or require an architectural rewrite.

## Contents

- [SKILL.md](SKILL.md): scope selection, cleanup decisions, verification, and reporting.
- [agents/openai.yaml](agents/openai.yaml): Codex display metadata and suggested prompt.
- [references/principles.md](references/principles.md): source material and interpretation.
- [references/structural-refactoring.md](references/structural-refactoring.md): conditional checks for call sites, dependencies, contracts, state, resource lifetimes, concurrency, algorithms, and tests.

The full texts of both *The Pragmatic Programmer*, 20th Anniversary Edition, and *Clean Code*, first edition, were available and referenced for this skill. The review also covered the full text of *The Clean Coder* from the supplied collection and [PEP 20](https://peps.python.org/pep-0020/), together with an existing PI simplification workflow. [Source notes](references/principles.md) record editions and coverage. The guidance is an original synthesis; no book files, PI extension, or external service are required.
