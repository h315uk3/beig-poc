# Python Project - GitHub Copilot Instructions

**For GitHub Copilot**: Project-specific development principles.

**For Claude Code**: See `CLAUDE.md` and `.claude/rules/` for detailed constraints.

---

## Philosophy

- **Type Safety**: Type hints required for all functions
- **Testability**: Write testable, modular code
- **Standard Library First**: Minimize external dependencies
- **Simplicity**: Clear code over clever code

## Development Standards

**Python**: 3.11+, type hints, `ruff` compliance (CI enforced)

**Documentation Responsibilities**:
- **README.md**: User-facing (simple, example-driven, < 100 lines)
- **CONTRIBUTING.md**: Development setup, testing, PR process (for contributors)
- **Code docstrings**: Implementation details, API documentation

**Documentation Rules**:
- ❌ Never mix marketing and technical content in README
- ❌ No development setup/testing in user docs (belongs in CONTRIBUTING.md)
- ❌ Forbidden: Directory structures, file paths, version numbers in docs
- ✅ README links to CONTRIBUTING.md for development details
- ✅ Document "why" not "what"

**Anti-Patterns**:
- ❌ External dependencies without justification
- ❌ Volatile information in docs
- ❌ Over-engineering, premature optimization
- ❌ Warning suppression (noqa, type: ignore)

## Workflow

```bash
mise install        # Setup
mise run lint       # Lint (ruff check)
mise run typecheck  # Type check (pyright)
mise run format:check  # Format check
```

**Before committing**: Run `mise run lint && mise run typecheck && mise run format:check`

**Git**: `feature/`, `fix/`, `docs/` branches. Descriptive commits, reference issues.

## Reference

- `CLAUDE.md` - Philosophy
- `CONTRIBUTING.md` - Process
- `.claude/rules/` - Constraints
- `gh issue list` - Current issues
- `gh pr list` - Current PRs

---

For current implementation details, examine the codebase directly.
