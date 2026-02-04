# Code Style

## Python Standards

**Version**: Python 3.11+ required

**Type Hints**: Required for all functions
- Annotate parameters and return types
- Use modern syntax: `list[str]`, `dict[str, Any]`

**Formatting**: Enforced by ruff
- Line length: 88 characters
- Double quotes for strings
- Run `mise run lint` and `mise run format`

## File Organization

**Python modules**: `src/`
- One module per logical component
- 644 permissions (rw-r--r--)

**Tests**: `tests/`
- Test files and test utilities

## Documentation

**Inline comments**: Only for complex algorithms or non-obvious behavior

**Docstrings**: One-line summary + detailed description
- Explain "why" not "what"
- Document parameters and return values
- Include usage examples when helpful
