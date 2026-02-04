# Contributing to pc-purchase

This guide covers pc-purchase plugin specific development. For general contribution guidelines, see the [root CONTRIBUTING.md](../../CONTRIBUTING.md).

## Plugin Overview

pc-purchase is a PC purchase decision assistant that:
- Guides users through adaptive questioning
- Explores uncertainty dimensions systematically
- Tracks question effectiveness with reward scoring
- Converges when sufficient information is gathered

## Architecture

**Key Components:**
- **Commands**: User-facing slash commands (`/pc-purchase:good-question`)
- **Skills**: Computational algorithms (`/pc-purchase:requirement-analysis`)
- **Library**: Shared Python modules for feedback tracking and statistics

**Question Dimensions:**
- Usage and purpose
- Performance needs
- Constraints (budget, size, portability)
- Features and connectivity
- Decision criteria

## Testing Commands

### Test Setup

1. **Start Fresh Session**
   ```bash
   /exit
   claude
   ```

2. **Verify Plugin Loaded**
   - Check for plugin loaded message

### Command Test Procedures

**`/pc-purchase:good-question` - PC Purchase Decision Support**
- Test: Start a new decision session
- Verify:
  1. Session starts (question_feedback.json created/updated)
  2. Adaptive questions are asked based on uncertainty dimensions
  3. Each question-answer pair is recorded with reward scores
  4. Session completes with summary displayed
  5. Check `<workspace>/.claude/pc_purchase/question_feedback.json` contains session data

### Skill Test Procedures

**`/pc-purchase:requirement-analysis` - Analyze PC Requirements**
- Test: Run after collecting requirements via good-question
- Verify: Structured analysis output with recommendations and comparisons

### When to Test

**Must test before commit:**
- New command creation
- Question logic changes
- Feedback tracking modifications
- Frontmatter modifications

**Optional:**
- Minor wording improvements
- Comment/documentation changes

## Adding New Python Modules

1. Follow existing module patterns in `pc_purchase/lib/` for structure and doctest format
2. Use isolated paths in doctests (temporary directories, never actual `.claude/` directory)
3. Run `mise run test` to verify doctests pass without contaminating workspace
4. Run `mise run lint` to ensure code style compliance

**Doctest Isolation**: Use `tempfile.mkdtemp()` or explicit test paths in examples. Never assume `.claude/pc_purchase/` directory structure exists during tests.

## Common Issues

**Frontmatter Errors:**
- Missing `allowed-tools`: Add required tools to frontmatter
- Invalid YAML: Check indentation and quotes

**AskUserQuestion Errors:**
- Maximum 4 options (excluding auto-added "Other")
- Ensure options are distinct and meaningful

## Resources

- [Technical Overview](./docs/technical-overview.md) - Architecture and information theory
- [Root CONTRIBUTING](../../CONTRIBUTING.md) - General guidelines
