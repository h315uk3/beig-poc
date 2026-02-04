# Python Project Template

[![Python 3.11+](https://img.shields.io/badge/Python-3.11%2B-blue)](https://www.python.org/downloads/)
[![Tests](https://github.com/USERNAME/REPO/actions/workflows/test.yml/badge.svg)](https://github.com/USERNAME/REPO/actions/workflows/test.yml)
[![CodeQL](https://github.com/USERNAME/REPO/actions/workflows/codeql.yml/badge.svg)](https://github.com/USERNAME/REPO/actions/workflows/codeql.yml)

A clean Python project template with modern development tools and best practices.

## Features

- **Python 3.11+** - Modern Python with type hints
- **Ruff** - Fast linter and formatter
- **Pyright** - Static type checking
- **mise** - Tool version management and task runner
- **GitHub Actions** - Automated testing and security scanning

## Quick Start

```bash
# Clone the repository
git clone https://github.com/USERNAME/REPO.git
cd REPO

# Install mise (if not already installed)
curl https://mise.run | sh

# Install dependencies
mise install
```

## Development

### Available Tasks

```bash
mise run lint           # Lint code
mise run format         # Format code
mise run typecheck      # Type check
mise run format:check   # Check formatting
```

### Project Structure

```
.
├── src/              # Source code
├── tests/            # Test files
├── .github/          # GitHub workflows
├── .claude/          # Claude Code settings
├── ruff.toml         # Ruff configuration
├── pyrightconfig.json # Pyright configuration
└── mise.toml         # Tool and task definitions
```

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md) for development guidelines.

## License

[Specify your license here]
