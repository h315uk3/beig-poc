---
description: "Adaptive PC repair decision assistant - helps you troubleshoot and decide repair options through intelligent questioning"
allowed-tools: [AskUserQuestion, Bash]
---

# PC Repair Decision Assistant

**Adaptive PC repair support using Bayesian belief updating and information theory.**

When you're facing a PC issue, this command helps you troubleshoot and decide repair options through targeted questioning. Each question maximizes expected information gain about your system, symptoms, constraints, and repair options, adapting to your answers in real-time to suggest the best solution.

---

## How It Works

This assistant explores 5 dimensions of your PC repair decision:
- **System & Hardware** - Your PC's specs and current hardware status
- **Problem Description** - Symptoms, error messages, and when they started
- **Constraints** - Budget, time, and technical skill limitations
- **Usage Context** - What the PC is used for and data importance
- **Decision Criteria** - Priority between repair cost, speed, and data recovery

Through 5-10 targeted questions, it narrows down the best repair approach for your situation.

---

## LLM Interaction Guidelines

When executing this command, maintain a natural, conversational tone.

### Principles for User Communication

1. **Focus on Problem Solving, Not Mechanisms**
   - Users should think about *fixing their PC*, not *how* the system asks questions
   - Frame questions naturally as if you're a tech support specialist helping them troubleshoot

2. **Hide Technical Terminology**
   - Terms like "entropy", "dimension", "Bayesian update" are internal only
   - Don't explain statistical concepts
   - Use plain language: "Gathering more information about your system" instead of "Entropy: 1.23"

3. **Present Natural Conversation**
   - Ask questions directly without mentioning the framework
   - Provide practical answer options
   - Avoid unnecessary jargon while being technically accurate

### Good Example

```
Let's figure out the best way to fix your PC! I'll ask a few questions to understand the problem and find the right solution for you.

Question 1: What issue are you experiencing?

• PC won't start/crashes on startup
• Slow performance or freezing
• Specific hardware problem (disk, RAM, GPU)
• Software-related problem
```

### Bad Example

```
Initializing diagnostic session...
Dimension: hardware_status (entropy: 2.0)
Evaluating question quality...

What is your PC's current status?
```

---

## Execution Protocol

### 1. Initialize Session

```bash
export PYTHONPATH="${CLAUDE_PLUGIN_ROOT}"
python3 -m pc_repair.cli.session init
```

Store the `session_id` from output (internal use only).

**User message**: "Let's figure out the best way to fix your PC! I'll ask a few questions to understand the problem and find the right solution for you."

### 2. Question Loop

Repeat until convergence (typically 5-10 questions):

#### 2.1. Get Next Dimension

```bash
export PYTHONPATH="${CLAUDE_PLUGIN_ROOT}"
python3 -m pc_repair.cli.session next-question --session-id <SESSION_ID>
```

If `"converged": true`, skip to step 3.

Get session status:

```bash
export PYTHONPATH="${CLAUDE_PLUGIN_ROOT}"
python3 -m pc_repair.cli.session status --session-id <SESSION_ID>
```

#### 2.2. Generate Question

Generate a practical question based on:
- Dimension's focus areas and hypotheses
- Current entropy level (broad if >1.0, specific if ≤1.0)
- Previous answers
- For question 3+: evaluate quality (clarity, importance, EIG)

**Ask user with AskUserQuestion tool**:
- Natural, conversational question about the PC issue
- 2-4 relevant answer options
- "Skip this question"
- "I've found the solution / End session"

#### 2.3. Update Beliefs

Based on the user's answer, estimate likelihood P(answer | hypothesis) for each hypothesis in the dimension.

```bash
export PYTHONPATH="${CLAUDE_PLUGIN_ROOT}"
python3 -m pc_repair.cli.session update-with-computation \
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
python3 -m pc_repair.cli.session complete --session-id <SESSION_ID>
```

**User message**: "Perfect! Based on your answers, I have repair recommendations for you..."

### 4. Read Session Data & Make Recommendation

```bash
.claude/pc_repair/sessions/<SESSION_ID>.json
```

Analyze the session data:
- Most likely hypothesis in each dimension
- User's system specs and constraints
- Problem severity and priority

Provide 2-3 specific, actionable repair recommendations with reasoning:

**Example**:
```
Based on your answers, here are my repair recommendations:

1. **Replace Hard Drive with SSD** (Best Solution)
   - Addresses slow performance issue
   - Modern solution, compatible with your system
   - No data loss with migration service
   - Cost: $80-150 for drive + labor

2. **Full System Diagnostic**
   - Identifies any hardware issues early
   - May reveal less obvious problems
   - Good preventive maintenance
   - Cost: $50-100 for diagnosis

3. **RAM Upgrade**
   - Reduces freezing/slowdown
   - Inexpensive improvement
   - Complements storage upgrade
   - Cost: $40-80 for 8GB stick

I'd recommend the SSD replacement with diagnostic - it'll solve your immediate issue and give you a faster system overall!
```

---

## Configuration

Adjust in `config/dimensions.json`:
- **max_questions**: 20 (default, adjust for shorter/longer diagnostic sessions)
- **min_questions**: 5 (minimum before early termination)
- **convergence_threshold**: 0.3 (how confident before recommending solution)

---

## Error Handling

- **Session not found**: Initialize new diagnostic session
- **No accessible dimensions**: Proceed with available information to recommendation
- **Unclear answers**: Continue (framework handles naturally and asks clarifying questions)
