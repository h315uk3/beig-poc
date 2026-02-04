# pc-purchase

**Claude Helps You Choose the Right PC**

> Unsure which PC to buy? Claude helps you decide through intelligent questioning.
> No setup. No dependencies. (Just Claude Code itself.)

## Example

```
You: /pc-purchase:good-question
Claude: Let's figure out which PC is right for you! I'll ask a few questions.

Question 1: What's your primary use case for this PC?

• Gaming and entertainment
• Professional work (video editing, design, development)
• General use (web browsing, office work)
• Content creation and streaming

You: Professional work (video editing, design, development)

Claude: Question 2: What's your budget range?

• Under $1,000
• $1,000 - $1,500
• $1,500 - $2,500
• Over $2,500

You: $1,500 - $2,500

Claude: Question 3: How important is portability?

You: Very important - I travel frequently

Claude: Got it. Let me suggest some options for a portable professional workstation
in the $1,500-$2,500 range...

[Claude then generates specific PC recommendations with detailed reasoning]
```

> **After convergence**: Claude automatically generates PC recommendations including specifications, price comparisons, and purchase advice.

---

## Demo

![Adaptive Questioning Demo](https://h315uk3.github.io/symbiosis/assets/video/demo-pc-purchase-questions.gif)

---

## Key Features

- **Adaptive Questioning** - Each question builds on previous answers
- **5 Dimensions** - Systematically covers usage, performance, constraints, features, criteria
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
