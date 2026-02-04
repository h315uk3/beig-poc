# Contributing to Medical Consultation Assistant

This guide covers medical-consultation plugin specific development. For general contribution guidelines, see the [root CONTRIBUTING.md](../../CONTRIBUTING.md).

## Plugin Overview

medical-consultation is a symptom analysis plugin that:
- Guides users through adaptive medical questioning
- Explores symptom dimensions systematically
- Tracks question effectiveness with reward scoring
- Converges when sufficient information is gathered

## Architecture

**Key Components:**
- **Commands**: User-facing slash commands (`/medical-consultation:good-question`)
- **Skills**: Computational algorithms (`/medical-consultation:symptom-analysis`)
- **Library**: Shared Python modules for feedback tracking and statistics

**Question Dimensions:**
- Symptoms and health concerns
- Severity and urgency
- Medical history
- Lifestyle context
- Care goals

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

**`/medical-consultation:good-question` - Medical Symptom Analysis**
- Test: Start a new analysis session
- Verify:
  1. Session starts (question_feedback.json created/updated)
  2. Adaptive questions are asked based on symptom dimensions
  3. Each question-answer pair is recorded with reward scores
  4. Session completes with assessment displayed
  5. Check `<workspace>/.claude/medical_consultation/question_feedback.json` contains session data

### Skill Test Procedures

**`/medical-consultation:symptom-analysis` - Analyze Symptoms**
- Test: Run after collecting symptoms via good-question
- Verify: Structured analysis output with recommendations and guidance

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

1. Follow existing module patterns in `medical_consultation/lib/` for structure and doctest format
2. Use isolated paths in doctests (temporary directories, never actual `.claude/` directory)
3. Run `mise run test` to verify doctests pass without contaminating workspace
4. Run `mise run lint` to ensure code style compliance

**Doctest Isolation**: Use `tempfile.mkdtemp()` or explicit test paths in examples. Never assume `.claude/medical_consultation/` directory structure exists during tests.

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
