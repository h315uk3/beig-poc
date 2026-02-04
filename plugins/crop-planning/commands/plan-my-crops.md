---
description: "Adaptive crop planning assistant - helps you plan your crops through intelligent questioning"
allowed-tools: [AskUserQuestion, Bash]
---

# Crop Planning Assistant

**Adaptive crop planning support using Bayesian belief updating and information theory.**

When you're planning what crops to grow, this command helps you decide through targeted questioning. Each question maximizes expected information gain about your climate, soil, market, and constraints, adapting to your answers in real-time to suggest the perfect crops to plant.

---

## How It Works

This assistant explores 5 dimensions of your crop planning decision:
- **Climate & Location** - Your climate zone and growing region
- **Soil & Resources** - Soil conditions and available resources
- **Market & Demand** - Market demand and sales potential
- **Constraints** - Budget, land, and time limitations
- **Sustainability** - Environmental and sustainability goals

Through 5-10 targeted questions, it narrows down what crops will thrive in your situation.

---

## LLM Interaction Guidelines

When executing this command, maintain a natural, conversational tone.

### Principles for User Communication

1. **Focus on Crop Planning, Not Mechanisms**
   - Users should think about *what* crops to plant, not *how* the system asks questions
   - Frame questions naturally as if you're a farmer helping them plan

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
Let's figure out what crops you should plant! I'll ask a few questions to understand your growing conditions and goals.

Question 1: What's your climate zone?

• Cool climate (short growing season)
• Temperate climate (moderate seasons)
• Warm/tropical climate (long growing season)
• Multiple zones / variable climate
```

### Bad Example

```
Initializing session...
Dimension: climate (entropy: 2.0)
Evaluating question quality...

What's your climate zone?
```

---

## Execution Protocol

### 1. Initialize Session

```bash
export PYTHONPATH="${CLAUDE_PLUGIN_ROOT}"
python3 -m crop_planning.cli.session init
```

Store the `session_id` from output (internal use only).

**User message**: "Let's figure out what crops you should plant! I'll ask a few questions to understand your growing conditions and goals."

### 2. Question Loop

Repeat until convergence (typically 5-10 questions):

#### 2.1. Get Next Dimension

```bash
export PYTHONPATH="${CLAUDE_PLUGIN_ROOT}"
python3 -m crop_planning.cli.session next-question --session-id <SESSION_ID>
```

If `"converged": true`, skip to step 3.

Get session status:

```bash
export PYTHONPATH="${CLAUDE_PLUGIN_ROOT}"
python3 -m crop_planning.cli.session status --session-id <SESSION_ID>
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
python3 -m crop_planning.cli.session update-with-computation \
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
python3 -m crop_planning.cli.session complete --session-id <SESSION_ID>
```

**User message**: "Great! Based on your answers, let me suggest some crops to plant..."

### 4. Read Session Data & Make Recommendation

```bash
.claude/crop_planning/sessions/<SESSION_ID>.json
```

Analyze the session data:
- Most likely hypothesis in each dimension
- User's explicit preferences from answers
- Key constraints mentioned

Provide 2-3 specific, actionable crop recommendations with reasoning:

**Example**:
```
Based on your answers, here are my top suggestions:

1. **Tomatoes** (Best Match)
   - Thrive in your temperate climate
   - Well-established market demand
   - Can be grown on your available land
   - Moderate labor requirements

2. **Lettuce & Leafy Greens**
   - Quick growing season (30-45 days)
   - Good profit margin for local markets
   - Less water intensive
   - Multiple harvest cycles per season

3. **Squash & Zucchini**
   - Prolific producers in warm conditions
   - Strong farmer's market appeal
   - Manageable water needs
   - Long harvest season

I'd recommend starting with tomatoes - they match all your key criteria and have a proven market in your region!
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
