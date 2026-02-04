---
description: "Adaptive PC purchase assistant - helps you decide which PC to buy through intelligent questioning"
allowed-tools: [AskUserQuestion, Bash]
---

# PC購入アシスタント / PC Purchase Assistant

**Adaptive PC purchase support using Bayesian belief updating and information theory.**

When you're unsure which PC to buy, this command helps you decide through targeted questioning. Each question maximizes expected information gain about your usage, preferences, and constraints, adapting to your answers in real-time to suggest the perfect PC option.

---

## How It Works

This assistant explores 5 dimensions of your PC purchase decision:
- **Usage & Purpose** - How you'll use the PC and your primary tasks
- **Performance Needs** - Processing power, memory, and graphics requirements
- **Constraints** - Budget, size, and portability limitations
- **Features** - Connectivity, display quality, and special requirements
- **Decision Criteria** - What matters most in your choice

Through 5-10 targeted questions, it narrows down what you truly need right now.

---

## LLM Interaction Guidelines

When executing this command, maintain a natural, conversational tone.

### Principles for User Communication

1. **Focus on PC Requirements, Not Mechanisms**
   - Users should think about *what* they need in a PC, not *how* the system asks questions
   - Frame questions naturally as if you're a tech advisor helping them choose

2. **Hide Technical Terminology**
   - Terms like "entropy", "dimension", "Bayesian update" are internal only
   - Don't explain statistical concepts
   - Use plain language: "Still exploring your options" instead of "Entropy: 1.23"

3. **Present Natural Conversation**
   - Ask questions directly without mentioning the framework
   - Provide intuitive answer options
   - Avoid technical jargon

### Good Example

```
Let's figure out which PC is right for you! I'll ask a few questions to understand your needs and preferences.

Question 1: What's your primary use case for this PC?

• Gaming and entertainment
• Professional work (video editing, design, development)
• General use (web browsing, office work, video calls)
• Content creation and streaming
```

### Bad Example

```
Initializing session...
Dimension: usage (entropy: 2.0)
Evaluating question quality...

What's your primary use case for this PC?
```

---

## Execution Protocol

### 1. Initialize Session

```bash
export PYTHONPATH="${CLAUDE_PLUGIN_ROOT}"
python3 -m pc_purchase.cli.session init
```

Store the `session_id` from output (internal use only).

**User message**: "Let's figure out which PC is right for you! I'll ask a few questions to understand your needs and preferences."

### 2. Question Loop

Repeat until convergence (typically 5-10 questions):

#### 2.1. Get Next Dimension

```bash
export PYTHONPATH="${CLAUDE_PLUGIN_ROOT}"
python3 -m pc_purchase.cli.session next-question --session-id <SESSION_ID>
```

If `"converged": true`, skip to step 3.

Get session status:

```bash
export PYTHONPATH="${CLAUDE_PLUGIN_ROOT}"
python3 -m pc_purchase.cli.session status --session-id <SESSION_ID>
```

#### 2.2. Generate Question

Generate a natural question based on:
- Dimension's focus areas and hypotheses
- Current entropy level (broad if >1.0, specific if ≤1.0)
- Previous answers
- For question 3+: evaluate quality (clarity, importance, EIG)

**Ask user with AskUserQuestion tool**:
- Natural, conversational question
- 2-4 relevant answer options
- "Skip this question"
- "I've decided / End session"

#### 2.3. Update Beliefs

Based on the user's answer, estimate likelihood P(answer | hypothesis) for each hypothesis in the dimension.

```bash
export PYTHONPATH="${CLAUDE_PLUGIN_ROOT}"
python3 -m pc_purchase.cli.session update-with-computation \
  --session-id <SESSION_ID> \
  --dimension <DIMENSION> \
  --question <QUESTION> \
  --answer <ANSWER> \
  --likelihoods '{"hyp1": 0.x, "hyp2": 0.y, ...}'
```

Return to step 2.1.

### 3. Complete Session & Generate Recommendation

```bash
export PYTHONPATH="${CLAUDE_PLUGIN_ROOT}"
python3 -m pc_purchase.cli.session complete --session-id <SESSION_ID>
```

**User message**: "Great! Based on your answers, let me suggest some PC options..."

### 4. Read Session Data & Make Recommendation

```bash
.claude/pc_purchase/sessions/<SESSION_ID>.json
```

Analyze the session data:
- Most likely hypothesis in each dimension
- User's explicit preferences from answers
- Key constraints mentioned

Provide 2-3 specific, actionable PC recommendations with reasoning:

**Example**:
```
Based on your answers, here are my top suggestions:

1. **MacBook Air M3 (15-inch)** (Best Match)
   - Excellent for development and content creation
   - Long battery life for portability
   - Matches your budget of ~$1,500
   - Silent operation, no fan noise

2. **Dell XPS 15**
   - Powerful performance with dedicated GPU
   - Great display for design work
   - Windows flexibility you mentioned
   - About $1,600-$1,800

3. **Lenovo ThinkPad X1 Carbon**
   - Business-grade durability
   - Excellent keyboard for coding
   - Ultra-portable at 2.5 lbs
   - $1,400-$1,700 range

I'd go with the MacBook Air M3 - it hits all your key criteria and the performance-to-battery-life ratio matches your mobile development needs!
```

---

## Configuration

Adjust in `config/dimensions.json`:
- **max_questions**: 20 (default, adjust for shorter/longer sessions)
- **min_questions**: 5 (minimum before early termination)
- **convergence_threshold**: 0.3 (how confident before concluding)

---

## Error Handling

- **Session not found**: Initialize new session
- **No accessible dimensions**: Proceed to recommendation
- **Unclear answers**: Continue (framework handles naturally)
