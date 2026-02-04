# Contributing

Thank you for your interest in contributing!

## Philosophy

### Core Values

- **Type Safety**: Type hints required for all functions
- **Testability**: Write testable, modular code
- **Standard Library First**: Minimize external dependencies
- **Local-First**: No unnecessary network calls

### Roles and Responsibilities

**Contributors:**
- Write type-annotated, well-tested code
- Ensure all checks pass locally before pushing
- Update relevant documentation
- Respond to review feedback constructively

**Reviewers:**
- Verify tests are comprehensive and meaningful
- Check type hints are present and correct
- Ensure code meets project standards
- Provide constructive feedback

## Development Environment Setup

### Prerequisites

- Git
- [mise](https://mise.jdx.dev/) - Tool version management and task runner

### Setup

```bash
# Clone and setup
git clone https://github.com/USERNAME/REPO.git
cd REPO

# Install mise (if not already installed)
curl https://mise.run | sh

# Install dependencies
mise install
```

## Development Workflow

### Code Quality

```bash
mise run lint           # Lint Python code (ruff)
mise run format         # Format Python code (ruff)
mise run typecheck      # Type check (pyright)
```

### Available Tasks

See all available tasks:
```bash
mise tasks
```

## Code Standards

**Python**:
- Python 3.11+ with type hints
- Must pass `ruff check` and `ruff format`
- Include comprehensive tests for all functions
- Prefer standard library over external dependencies

**Documentation**:
- Keep focused on principles, not implementation details
- Update docstrings for code changes
- Document "why" not "what"

## Pull Request Process

1. **Fork and Branch**
   ```bash
   git checkout -b feature/descriptive-name
   ```

2. **Develop with Quality Checks**
   ```bash
   mise run lint           # Fix style issues
   mise run typecheck      # Check types
   mise run format:check   # Verify formatting
   ```

3. **Commit Thoughtfully**
   - Write descriptive commits
   - Reference issues when relevant
   - Keep commits atomic

4. **Push and Create PR**
   - Fill out PR template
   - Explain what/why/how
   - Link related issues

5. **Respond to Reviews**
   - Address feedback promptly
   - Ask questions if unclear
   - Update PR based on comments

## CI/CD

GitHub Actions automatically runs on:
- Push to `main` or `develop` branches
- Pull requests to `main` or `develop`

Checks performed:
1. Install dependencies with mise
2. Run formatter check (`mise run format:check`)
3. Run linter (`mise run lint`)
4. Run type checker (`mise run typecheck`)

All checks must pass before merging.

## Questions?

- Open an issue for bugs or feature requests
- Check existing issues before creating new ones
- Be respectful and constructive in all interactions
