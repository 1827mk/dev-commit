---
name: dev-commit
description: >
  This skill should be used when the user says "commit". Generate conventional
  commit message from staged changes, show preview, commit after confirmation.
  Never run git add automatically.
---

## Commit Types

`feat` `fix` `docs` `refactor` `test` `chore` `style` `perf`

Append `!` for breaking changes: `feat!` `fix!`

## Message Format

```
[<type>]: <description>
```

- Lowercase, imperative mood
- No trailing period
- Max 72 characters
- Breaking: add `-m "BREAKING CHANGE: <detail>"` to commit

## Pre-flight Checks

Run in order, stop on first failure:

| Check | Command | Error |
|-------|---------|-------|
| Git installed | `git --version` | "Git is not installed." |
| In git repo | `git rev-parse --is-inside-work-tree` | "Not inside a git repository." |
| No merge/rebase | Check `MERGE_HEAD`, `CHERRY_PICK_HEAD`, `REBASE_HEAD` | "A merge/cherry-pick/rebase is in progress." |
| No conflicts | `git diff --name-only --diff-filter=U` | "Unresolved conflicts in: [files]." |
| Has staged | `git diff --cached --quiet` (exit 1 = has staged) | "Nothing staged. Run git add first." |
| Git config | `git config user.name && git config user.email` | "Git user not configured." |

> **Never run `git add` under any circumstance.**

## Workflow

1. **Inspect staged changes**
   ```bash
   git diff --cached --stat
   git diff --cached
   ```

2. **Detect breaking changes**
   - Removed/renamed exports
   - Changed function signatures
   - Deleted endpoints
   - Renamed env vars
   - If found → use `[type!]` + BREAKING CHANGE footer

3. **Determine commit type**
   - Single type → proceed
   - Multiple unrelated types → ask to split

4. **Generate message**
   - Trim to ≤72 chars if needed
   - Warn if truncated

5. **Get branch**
   ```bash
   git branch --show-current
   ```

6. **Show preview**
   ```
   Branch : <branch>
   Message: [<type>]: <description>
   Files  : <stat>

   Note: Unstaged changes will NOT be included.
   Commit? [y/n/e]
   ```

7. **On `y` — commit**
   ```bash
   git commit -m "[<type>]: <description>"
   # If breaking:
   git commit -m "[<type>!]: <description>" -m "BREAKING CHANGE: <detail>"
   ```

8. **Show result**
   ```bash
   git log -1 --oneline
   ```

## Split Commits

When multiple unrelated types detected:

1. Ask: "Split into separate commits? [y/n]"
2. **y** → Explain manual steps, abort:
   ```
   git restore --staged <files-for-second-commit>
   commit  # for first group
   git add <files-for-second-commit>
   commit  # for second group
   ```
3. **n** → Generate combined message, continue

## Rules

- **NEVER** run `git add`
- **NEVER** commit without showing preview
- **NEVER** commit during merge/rebase/cherry-pick
- On commit failure → show git error, do not retry
- On user cancel → abort silently
