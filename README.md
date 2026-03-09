# dev-commit

Generate conventional commit messages from staged changes.

**Silent mode** - outputs only the commit hash.

## Installation

```bash
/plugin marketplace add 1827mk/dev-commit
/plugin install dev-commit
```

## Usage

1. Stage your changes: `git add <files>`
2. Type: `commit`
3. Output: `commit a1b2c3d`

That's it.

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

## License

MIT
