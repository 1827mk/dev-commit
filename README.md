# dev-commit

Claude Code plugin for generating conventional commit messages from staged changes.

## Installation

```bash
claude --plugin-dir /path/to/dev-commit
```

## Usage

1. Stage your changes: `git add <files>`
2. Say `dev-commit` or `commit` in Claude Code
3. Done! The commit is created automatically

## Commit Types

| Type | Description |
|------|-------------|
| `feat` | New feature |
| `fix` | Bug fix |
| `docs` | Documentation |
| `refactor` | Code refactoring |
| `test` | Adding tests |
| `chore` | Maintenance |
| `style` | Formatting |
| `perf` | Performance |

Append `!` for breaking changes (e.g., `feat!`, `fix!`)

## Message Format

```
[<type>]: <description>
```

- Lowercase, imperative mood
- No trailing period
- Max 72 characters

## License

MIT
