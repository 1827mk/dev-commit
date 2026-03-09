---
name: dev-commit
description: >
  This skill should be used when the user says "dev-commit", "/dev-commit",
  "commit", or "git commit". Generate conventional commit message from staged
  changes and commit immediately. No push. No confirmation.
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

1. Run `git diff --cached` to inspect staged changes
2. Generate appropriate commit message
3. Run `git commit -m "[<type>]: <description>"`
4. Done - no push, no confirmation
