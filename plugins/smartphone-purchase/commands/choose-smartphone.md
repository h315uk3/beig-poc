---
description: "Adaptive smartphone purchase assistant - helps you choose the right phone through intelligent questioning"
allowed-tools: [AskUserQuestion, Bash]
---

# Which Smartphone Should I Buy?

**Adaptive smartphone purchase support using Bayesian belief updating and information theory.**

When you're unsure which smartphone to buy, this command helps you decide through targeted questioning. Each question maximizes expected information gain about your needs, preferences, and constraints, adapting to your answers in real-time to suggest the perfect smartphone option.

---

## How It Works

This assistant explores 5 dimensions of your smartphone purchase decision:
- **Use Case** - How you plan to use the phone and primary purposes
- **Performance** - Processing power, speed, and performance requirements
- **Specifications** - Camera, display, battery, and hardware features
- **Budget** - Price range and budget constraints
- **Brand/Ecosystem** - Preference for iOS, Android, brand ecosystem

Through 5-10 targeted questions, it narrows down which smartphone truly matches your needs.

---

## LLM Interaction Guidelines

When executing this command, maintain a natural, conversational tone.

### Principles for User Communication

1. **Focus on Phone Preferences, Not Mechanisms**
   - Users should think about *what* phone they want, not *how* the system asks questions
   - Frame questions naturally as if you're a friend helping them decide

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
Let's find the perfect smartphone for you! I'll ask a few questions to understand what you're looking for.

Question 1: How do you plan to use your phone?

• Productivity and work
• Gaming and entertainment
• Photography and content creation
• Everyday casual use
```

### Bad Example

```
Initializing session...
Dimension: mood (entropy: 2.0)
Evaluating question quality...

How are you feeling about lunch today?
```

---

## Execution Protocol

### 1. Initialize Session

```bash
export PYTHONPATH="${CLAUDE_PLUGIN_ROOT}"
python3 -m smartphone_purchase.cli.session init
```

Store the `session_id` from output (internal use only).

**User message**: "Let's find the perfect smartphone for you! I'll ask a few questions to understand what you're looking for."

### 2. Question Loop

Repeat until convergence (typically 5-10 questions):

#### 2.1. Get Next Dimension

```bash
export PYTHONPATH="${CLAUDE_PLUGIN_ROOT}"
python3 -m smartphone_purchase.cli.session next-question --session-id <SESSION_ID>
```

If `"converged": true`, skip to step 3.

Get session status:

```bash
export PYTHONPATH="${CLAUDE_PLUGIN_ROOT}"
python3 -m smartphone_purchase.cli.session status --session-id <SESSION_ID>
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
python3 -m smartphone_purchase.cli.session update-with-computation \
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
python3 -m smartphone_purchase.cli.session complete --session-id <SESSION_ID>
```

**User message**: "Great! Based on your answers, let me suggest some smartphone options..."

### 4. Read Session Data & Make Recommendation

```bash
.claude/smartphone_purchase/sessions/<SESSION_ID>.json
```

Analyze the session data:
- Most likely hypothesis in each dimension
- User's explicit preferences from answers
- Key constraints mentioned

Provide 2-3 specific, actionable smartphone recommendations with reasoning:

**Example**:
```
Based on your answers, here are my top suggestions:

1. **iPhone 15 Pro** (Best Match)
   - Matches your need for professional-grade camera
   - Excellent performance for productivity
   - Strong ecosystem integration
   - Price: $999

2. **Google Pixel 8 Pro**
   - Outstanding computational photography
   - Pure Android experience
   - Excellent AI features
   - Price: $899

3. **Samsung Galaxy S24 Ultra**
   - Best-in-class display and performance
   - Versatile camera system
   - Excellent battery life
   - Price: $1,199

I'd go with the iPhone 15 Pro - it hits all your key criteria and excels in both photography and productivity!
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
