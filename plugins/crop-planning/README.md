# crop-planning

**Claude Helps You Plan Your Crops**

> Planning what to grow? Claude helps you choose the right crops for your situation.
> No setup. No dependencies. (Just Claude Code itself.)

## Example

```
You: /crop-planning:good-question
Claude: Let's figure out what crops you should plant! I'll ask a few questions about your growing conditions.

Question 1: What's your climate zone?

• Cool climate (short growing season)
• Temperate climate (moderate seasons)
• Warm/tropical climate (long growing season)
• Multiple zones / variable climate

You: Temperate climate

Claude: Question 2: How much land do you have available?

• Less than 1 acre
• 1-5 acres
• 5-20 acres
• 20+ acres

You: 2 acres

Claude: Question 3: What's your primary goal?

• Maximize profit
• Sustainability and organic farming
• Personal consumption
• Local market sales

You: Local market sales

Claude: Got it. You're looking to grow crops in a temperate climate on about 2 acres for local market sales. Let me suggest some perfect options...

[Claude then generates crop recommendations with reasoning]
```

> **After convergence**: Claude automatically generates specific, actionable crop recommendations tailored to your climate, land, and goals.

---

## Demo

![Adaptive Crop Planning Demo](https://h315uk3.github.io/symbiosis/assets/video/demo-crop-planning-questions.gif)

---

## Key Features

- **Adaptive Questioning** - Each question builds on previous answers
- **5 Dimensions** - Systematically covers climate, soil, market, constraints, sustainability
- **Information Theory** - Shannon Entropy measures uncertainty, EIG selects optimal questions
- **Bayesian Convergence** - Beliefs update with each answer until crop recommendations are clear
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
