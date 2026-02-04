# Testing

## Philosophy

Every function must be testable:
- Clear input/output contracts
- Reproducible with mock data
- No external dependencies

## Test Coverage Requirements

**Coverage Requirements**:
- Normal operation (happy path)
- Edge cases (empty input, max values)
- Boundary conditions (0, 1, n-1, n)
- Error conditions (invalid input, missing files)

**Use realistic data**, not trivial tests like `1 + 1 == 2`.

## Type Checking

**Tool**: Pyright (Pylance CLI)

**Why**: Catch type errors before runtime, improve code quality, enable better IDE support.

**Requirements**:
- All public functions must have type hints
- Use Python 3.11+ syntax: `list[str]`, `dict[str, Any]`
- Avoid `Any` unless truly necessary

**Running**:
```bash
mise run typecheck      # Type check all code
```

**Common Issues**:
- Missing return type annotations
- Incorrect parameter types
- Untyped dictionary access
- Missing None checks for optional values

## Interactive Testing

**Manual testing required for**:
- CLI interactions
- User input flows
- Complex integration scenarios

**Procedure**:
1. Test with various inputs
2. Verify output and file changes
3. Test edge cases (invalid input, cancellation)

## CI/CD

All checks must pass before merging:
1. `mise run format:check`
2. `mise run lint`
3. `mise run typecheck`
