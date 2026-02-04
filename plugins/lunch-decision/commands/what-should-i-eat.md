---
description: "Adaptive lunch decision assistant - helps you decide what to eat through intelligent questioning"
allowed-tools: [AskUserQuestion, Bash]
---

# What Should I Eat?

**Adaptive lunch decision support using Bayesian belief updating and information theory.**

When you're unsure what to eat for lunch, this command helps you decide through targeted questioning. Each question maximizes expected information gain about your mood, preferences, and constraints, adapting to your answers in real-time to suggest the perfect lunch option.

---

## How It Works

This assistant explores 5 dimensions of your lunch decision:
- **Mood & Context** - How you're feeling and your current situation
- **Taste Preferences** - What flavors and cuisines appeal to you today
- **Constraints** - Budget, time, and location limitations
- **Health** - Dietary restrictions and nutritional goals
- **Decision Criteria** - What matters most in your choice

Through 5-10 targeted questions, it narrows down what you truly want to eat right now.

---

## LLM Interaction Guidelines

When executing this command, maintain a natural, conversational tone.

### Principles for User Communication

1. **Focus on Food Preferences, Not Mechanisms**
   - Users should think about *what* they want to eat, not *how* the system asks questions
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
Let's figure out what you should eat for lunch! I'll ask a few questions to understand what you're in the mood for today.

Question 1: How are you feeling about lunch today?

• Want something comforting and familiar
• Feeling adventurous, want to try something new
• Need something quick and practical
• Looking for a nice social experience
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
python3 -m lunch_decision.cli.session init
```

Store the `session_id` from output (internal use only).

**User message**: "Let's figure out what you should eat for lunch! I'll ask a few questions to understand what you're in the mood for today."

### 2. Question Loop

Repeat until convergence (typically 5-10 questions):

#### 2.1. Get Next Dimension

```bash
export PYTHONPATH="${CLAUDE_PLUGIN_ROOT}"
python3 -m lunch_decision.cli.session next-question --session-id <SESSION_ID>
```

If `"converged": true`, skip to step 3.

Get session status:

```bash
export PYTHONPATH="${CLAUDE_PLUGIN_ROOT}"
python3 -m lunch_decision.cli.session status --session-id <SESSION_ID>
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
python3 -m lunch_decision.cli.session update-with-computation \
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
python3 -m lunch_decision.cli.session complete --session-id <SESSION_ID>
```

**User message**: "Great! Based on your answers, let me suggest some lunch options..."

### 4. Read Session Data & Make Recommendation

```bash
.claude/lunch_decision/sessions/<SESSION_ID>.json
```

Analyze the session data:
- Most likely hypothesis in each dimension
- User's explicit preferences from answers
- Key constraints mentioned

Provide 2-3 specific, actionable lunch recommendations with reasoning:

**Example**:
```
Based on your answers, here are my top suggestions:

1. **Ramen at [Local Shop]** (Best Match)
   - Matches your craving for Asian food
   - Warm and comforting on a cold day
   - Quick service, fits your time constraint
   - Budget-friendly at ~$12

2. **Poke Bowl at [Nearby Café]**
   - Fresh and healthy option
   - Asian flavors you wanted
   - Customizable to preferences
   - About $15

3. **Thai Curry Takeout**
   - Rich, satisfying flavors
   - Can order ahead for speed
   - Vegetarian options available
   - $12-15 range

I'd go with the ramen - it hits all your key criteria and the cozy atmosphere matches your mood today!
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
