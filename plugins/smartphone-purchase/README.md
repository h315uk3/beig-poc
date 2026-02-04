# Smartphone Purchase Assistant

**Claude Helps You Choose the Right Phone**

> Looking for the perfect smartphone? Claude helps you decide through intelligent questioning.
> No setup. No dependencies. (Just Claude Code itself.)

## Example

```
You: /smartphone-purchase:good-question
Claude: Let's find the perfect smartphone for you. I'll ask some questions to understand your needs.

Question 1: How do you plan to use your phone?

• Productivity and work
• Gaming and entertainment
• Photography and content creation
• Everyday casual use

You: Photography and content creation

Claude: Question 2: What's your budget range?

• Under $500
• $500-800
• $800-1200
• Over $1200

You: $800-1200

Claude: Question 3: Which ecosystem do you prefer?

• iOS (Apple)
• Android (Google, Samsung, etc.)
• No strong preference

You: iOS

Claude: Got it. You're looking for a powerful iOS phone great for photography with a budget of $800-1200. Let me ask a couple more questions about specific features...

[Claude continues with targeted questions]
```

> **After convergence**: Claude automatically generates specific smartphone recommendations tailored to your needs, including pros/cons and price points.

---

## Demo

![Adaptive Questioning Demo](https://h315uk3.github.io/symbiosis/assets/video/demo-smartphone-purchase-questions.gif)

---

## Key Features

- **Adaptive Questioning** - Each question builds on previous answers
- **5 Dimensions** - Systematically covers use case, performance, specifications, budget, ecosystem
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
