# pc-repair

**Claude Helps You Fix Your PC**

> Your PC acting up? Claude helps you diagnose the problem and find the best repair solution.
> No setup. No dependencies. (Just Claude Code itself.)

## Example

```
You: /pc-repair:good-question
Claude: Let's diagnose your PC issue. I'll ask a series of questions to understand the problem.

Question 1: What problem are you experiencing?

• PC won't start or crashes on boot
• Slow performance or freezing
• Specific hardware failure (hard drive, RAM, etc.)
• Software or driver issues

You: Slow performance or freezing

Claude: Question 2: How long has this been happening?

• Just started today
• Past few days
• A week or more
• It's been getting worse gradually

You: Past few days

Claude: Question 3: Are you seeing any error messages?

You: No specific errors, just freezing

Claude: Got it. You're experiencing recent performance degradation with freezing but no error messages. Let me gather a bit more information...

[Claude asks more diagnostic questions about your system specs, usage patterns, and constraints]

[Claude then generates targeted repair recommendations with cost estimates and implementation guidance]
```

> **After convergence**: Claude automatically generates actionable repair recommendations including cost analysis, time estimates, and data recovery options.

---

## Demo

![Adaptive Questioning Demo](https://h315uk3.github.io/symbiosis/assets/video/demo-pc-repair-questions.gif)

---

## Key Features

- **Adaptive Questioning** - Each diagnostic question builds on previous answers
- **5 Problem Dimensions** - Systematically covers hardware, symptoms, constraints, usage, and priorities
- **Information Theory** - Shannon Entropy measures diagnostic uncertainty, EIG selects optimal questions
- **Bayesian Convergence** - Beliefs update with each answer until confident diagnosis is achieved
- **Local-First** - All diagnostic data stays on your machine, no external services
- **Zero Dependencies** - Pure Python standard library only

---

## Documentation

- **[Technical Overview](./docs/technical-overview.md)** - Architecture, information theory, configuration, and design principles

---

## Installation

See [main README](../../README.md#installation) for installation instructions.

**Requirements:**
- Python 3.11+
- Claude Code CLI

---

## License

GNU AGPL v3 - [LICENSE](../../LICENSE)
