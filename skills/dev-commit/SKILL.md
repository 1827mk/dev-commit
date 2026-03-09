---
name: dev-commit
description: >
  This skill should be used when the user says "commit". Generate conventional
  commit message from staged changes and commit immediately. Silent mode - only
  output commit hash.
---

## Commit Types
`feat` `fix` `docs` `refactor` `test` `chore` `style` `perf`

Append `!` for breaking changes → `feat!` `fix!`

## Message Format
```
[<type>]: <description>
```
- Lowercase, imperative mood, no trailing period
- Max 72 characters

## Workflow

1. Run `git diff --cached` silently
2. Generate commit message
3. Run `git commit -m "[<type>]: <description>"`
4. Output only: `commit <hash>`

## Output Format

Only output the commit hash, nothing else:
```
commit a1b2c3d
```
