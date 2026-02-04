# Python Project - Development Philosophy

Core principles for development with Claude Code.

## Core Values

- **Type Safety**: Prevent runtime errors through static analysis
- **Testability**: Every function must be independently testable
- **Simplicity**: Clear code over clever code
- **Documentation**: Clear documentation for maintainability

## Architectural Philosophy

### Simplicity First

Maintain simplicity through deliberate constraints:
- Clear input/output contracts
- Explicit data flow
- Minimal abstractions

### Testability as Foundation

Every component must be independently testable:
- Type hints for all functions
- Tests for all public functions
- Reproducible behavior

## Anti-Patterns

### Over-Engineering
- Don't add features "for the future"
- Don't create abstractions for single-use code
- Don't optimize prematurely

### Breaking Simplicity
- Don't introduce external dependencies casually
- Don't replace clear code with "clever" code
- Don't skip type hints or tests

## Documentation Responsibilities

Clear separation of documentation purposes:

### README.md (User-Facing)
- **Purpose**: First impression, quick start, concrete examples
- **Length**: < 100 lines
- **Content**: Problem → Solution → Example → Key Features
- **Style**: Simple, concise, example-driven

### CONTRIBUTING.md (Contributor Guide)
- **Purpose**: How to develop, test, and contribute
- **Audience**: Contributors and maintainers
- **Content**: Setup, testing, code style, PR process

### Code Docstrings
- **Purpose**: Implementation details, API contracts
- **Audience**: Developers reading the code
- **Content**: Function behavior, parameters, return values, usage examples

## Documentation Rules

**Never Do:**
- ❌ Mix marketing and technical content in README
- ❌ Put development setup/testing in user docs
- ❌ Document directory structures, file paths, version numbers
- ❌ Create CHANGELOG files (git log is source of truth)

**Always Do:**
- ✅ Keep README simple and example-driven
- ✅ Separate process (CONTRIBUTING.md) from principles (CLAUDE.md)
- ✅ Use docstrings for implementation details
- ✅ Document "why" not "what"

---

**Note**: For development constraints, code style, testing, and contribution process, see `.claude/rules/` and `CONTRIBUTING.md`.
