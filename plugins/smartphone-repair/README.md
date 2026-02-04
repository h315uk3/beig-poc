# smartphone-repair

**Claude's Smartphone Repair Advisor**

> Need to fix your phone? Claude helps you diagnose the issue and find the best repair solution.
> No setup. No dependencies. (Just Claude Code itself.)

## Example

```
You: /smartphone-repair:good-question
Claude: Let's diagnose your smartphone issue. I'll ask a series of questions.

Question 1: What type of smartphone do you have?

• iPhone
• Samsung
• Google Pixel
• Other Android

You: iPhone

Claude: Question 2: What problem are you experiencing?

• Cracked or damaged screen
• Battery issues
• Not charging
• Water damage
• Other issues

You: Battery not lasting all day

Claude: Question 3: How old is your iPhone?

• Less than 1 year
• 1-2 years
• 2-3 years
• More than 3 years

You: About 2 years old

Claude: Got it. Battery degradation is common on iPhones after 2 years. Let me ask a few more questions...

[Claude then generates detailed repair recommendations with costs and options]
```

> **After convergence**: Claude automatically generates a detailed repair recommendation including cost estimates, DIY vs professional options, and potential complications.

---

## Demo

![Smartphone Repair Diagnosis Demo](https://h315uk3.github.io/symbiosis/assets/video/demo-smartphone-repair.gif)

---

## Key Features

- **Adaptive Diagnosis** - Each question builds on previous answers about your device
- **5 Dimensions** - Systematically covers device info, symptoms, constraints, history, and options
- **Information Theory** - Shannon Entropy measures diagnostic uncertainty, EIG selects optimal questions
- **Bayesian Convergence** - Beliefs update with each answer until diagnosis is clear
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
