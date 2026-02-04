# Contributing to pc-repair

This guide covers pc-repair plugin specific development. For general contribution guidelines, see the [root CONTRIBUTING.md](../../CONTRIBUTING.md).

## Plugin Overview

pc-repair is a diagnostic assistant plugin that:
- Guides users through adaptive troubleshooting questions
- Explores problem dimensions systematically
- Tracks question effectiveness with reward scoring
- Converges when sufficient diagnostic information is gathered

## Architecture

**Key Components:**
- **Commands**: User-facing slash commands (`/pc-repair:good-question`)
- **Skills**: Computational algorithms (`/pc-repair:repair-analysis`)
- **Library**: Shared Python modules for feedback tracking and statistics

**Question Dimensions:**
- System hardware and specifications
- Problem description and symptoms
- Time and budget constraints
- System usage and data importance
- Decision priority (cost vs speed vs data recovery)

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

**`/pc-repair:good-question` - Requirement Elicitation**
- Test: Start a new elicitation session
- Verify:
  1. Session starts (question_feedback.json created/updated)
  2. Adaptive questions are asked based on uncertainty dimensions
  3. Each question-answer pair is recorded with reward scores
  4. Session completes with summary displayed
  5. Check `<workspace>/.claude/pc_repair/question_feedback.json` contains session data

### Skill Test Procedures

**`/pc-repair:repair-analysis` - Analyze Repair Options**
- Test: Run after collecting repair information via good-question
- Verify: Structured repair analysis output with options and suggestions

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

1. Follow existing module patterns in `pc_repair/lib/` for structure and doctest format
2. Use isolated paths in doctests (temporary directories, never actual `.claude/` directory)
3. Run `mise run test` to verify doctests pass without contaminating workspace
4. Run `mise run lint` to ensure code style compliance

**Doctest Isolation**: Use `tempfile.mkdtemp()` or explicit test paths in examples. Never assume `.claude/pc_repair/` directory structure exists during tests.

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
