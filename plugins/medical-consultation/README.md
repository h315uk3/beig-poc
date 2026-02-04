# Medical Consultation Assistant

**Claude Provides Intelligent Medical Symptom Analysis**

> Experiencing health concerns? Claude helps you understand your symptoms and provides appropriate guidance.
> No setup. No dependencies. (Just Claude Code itself.)

## Example

```
You: /medical-consultation:good-question
Claude: Let's understand your health concerns. I'll ask a series of questions.

Question 1: What brings you here today?

• Experiencing specific symptoms or discomfort
• Monitoring a known health condition
• Concerned about potential health risks
• Seeking preventive care guidance

You: Experiencing specific symptoms or discomfort

Claude: Question 2: When did these symptoms start?

• Within the last few hours
• 1-3 days ago
• Over a week ago
• Recurring over time

You: 1-3 days ago

Claude: Question 3: How would you describe the severity?

You: Moderate discomfort, manageable but concerning

Claude: Based on your responses, I recommend scheduling a medical consultation within 24-48 hours. These symptoms warrant professional evaluation but are not an emergency...

[Claude then provides detailed guidance and recommendations]
```

> **After convergence**: Claude automatically generates a health assessment including severity analysis, recommended actions, and warning signs.

---

## Demo

![Adaptive Medical Consultation Demo](https://h315uk3.github.io/symbiosis/assets/video/demo-medical-consultation-questions.gif)

---

## Key Features

- **Adaptive Questioning** - Each question builds on previous answers
- **5 Dimensions** - Systematically covers symptoms, severity, history, context, care goals
- **Information Theory** - Shannon Entropy measures uncertainty, EIG selects optimal questions
- **Bayesian Convergence** - Beliefs update with each answer until clarity is achieved
- **Local-First** - All data stays on your machine, no external services
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
