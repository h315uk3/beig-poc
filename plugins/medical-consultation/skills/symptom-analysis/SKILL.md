---
description: "Analyze collected medical symptoms from consultations, assess severity, generate structured health assessments, and suggest appropriate care recommendations"
context: fork
allowed-tools: [Bash, Read]
---

# Symptom Analysis Skill

This skill transforms raw medical consultation data into structured, actionable health assessments.

---

## When to Use This Skill

Use this skill after completing a symptom analysis consultation (e.g., via `/good-question`) when you have:
- Collected answers across multiple symptom dimensions
- Raw notes from patient conversations
- Unstructured health information that needs formalization

**Do not use this skill:**
- During active consultations (use it after information gathering is complete)
- For diagnosis or treatment decisions (defer to healthcare professionals)
- When symptoms are already well-documented

---

## What This Skill Does

### 1. Structure Health Assessment

Transform raw consultation data into a formal assessment organized by:
- **Symptoms**: Reported symptoms, onset, duration, severity
- **Medical History**: Relevant past conditions, medications, allergies
- **Lifestyle Context**: Environmental factors, recent activities, stress levels
- **Severity Assessment**: Urgency level, risk factors, complications
- **Care Recommendations**: Suggested actions, monitoring needs, warning signs

### 2. Detect Issues

Identify and report:
- **Ambiguities**: Vague or underspecified symptom descriptions
- **Contradictions**: Conflicting statements about symptoms or timeline
- **Gaps**: Missing information critical for proper assessment
- **Red Flags**: Symptoms requiring immediate medical attention

### 3. Generate Care Guidance

Provide:
- **Urgency Assessment**: How soon medical attention is needed
- **Recommended Actions**: Immediate steps, self-care, when to seek help
- **Monitoring Strategy**: What symptoms to track and report
- **Warning Signs**: When to escalate to emergency care

---

## Input Format

**PREFERRED: Dimension Data JSON (from /good-question)**

If invoked after a `/good-question` consultation, provide dimension data in JSON format:

```json
{
  "symptoms": {
    "answered": true,
    "content": "English summary of reported symptoms with details",
    "examples": 2,
    "contradictions": false
  },
  "severity": {
    "answered": true,
    "content": "English summary of severity and urgency indicators",
    "examples": 1,
    "contradictions": false
  },
  "history": {
    "answered": true,
    "content": "English summary of medical history and medications",
    "examples": 3,
    "contradictions": false
  },
  "context": {
    "answered": true,
    "content": "English summary of lifestyle and environmental factors",
    "examples": 1,
    "contradictions": false
  },
  "care_goals": {
    "answered": true,
    "content": "English summary of what type of care or guidance is needed",
    "examples": 0,
    "contradictions": false
  }
}
```

**CRITICAL**: Content fields MUST be in English for uncertainty calculation to work correctly.

---

**ALTERNATIVE: Raw Consultation Data**

For ad-hoc analysis without `/good-question`, provide raw consultation data:

```markdown
## Consultation Transcript

Patient said: "I've been experiencing headaches..."
Question 1: When did the headaches start?
Answer: "About 3 days ago..."

Question 2: How severe are they?
Answer: "Moderate, manageable with over-the-counter pain relief..."

[etc.]
```

Or as structured notes:

```markdown
## Collected Information

Symptoms: Persistent headaches with visual disturbances for 3 days
Severity: Moderate discomfort, impacting daily activities
Medical History: No relevant past conditions, no current medications
Context: High stress at work, reduced sleep
Care Goals: Determine if medical consultation is needed
```

---

## Output Format

### Structured Health Assessment

```markdown
# Health Assessment: [Patient Concern]

## 1. Symptom Summary

### Primary Symptoms
[Clear description of main symptoms reported]

### Timeline
[When symptoms started, progression, changes over time]

### Severity Indicators
[Assessment of symptom severity and impact on daily life]

---

## 2. Medical Context

### Relevant Medical History
- **Past Conditions**: [Relevant conditions]
- **Current Medications**: [List of medications]
- **Allergies**: [Known allergies]
- **Family History**: [Relevant family medical history]

### Lifestyle Factors
- **Recent Activities**: [Changes or events that may be relevant]
- **Environmental Factors**: [Exposure or environmental concerns]
- **Stress Levels**: [Work, life stressors]

---

## 3. Severity Assessment

### Urgency Level
[Immediate/Urgent/Routine/Non-urgent]

### Risk Factors
- [Risk factor 1]
- [Risk factor 2]

### Red Flags Detected
⚠️ [Any concerning symptoms requiring immediate attention]

---

## 4. Recommended Actions

### Primary Recommendation
[Main course of action - seek medical care, self-care, monitoring]

**Timeframe**: [How soon to act]
**Provider**: [Type of healthcare provider to see]

### Self-Care Measures
1. [Immediate self-care step 1]
2. [Self-care step 2]
3. [What to avoid]

### Monitoring Plan
Track and document:
- [Symptom 1 to monitor]
- [Symptom 2 to monitor]
- [Changes to report]

---

## 5. Warning Signs

### Seek Emergency Care Immediately If:
- [Emergency symptom 1]
- [Emergency symptom 2]
- [Emergency symptom 3]

### Escalate to Medical Care If:
- [Worsening symptom pattern]
- [New symptoms develop]
- [No improvement timeframe]

---

## 6. Information Gaps

### Missing Information
[What information would help refine this assessment]

### Questions for Healthcare Provider
1. [Question 1]
   - **Why it matters**: [Relevance]
2. [Question 2]

---

## 7. Important Disclaimers

⚠️ **This is guidance based on reported symptoms. A healthcare professional should evaluate your condition for proper diagnosis and treatment.**

**Not for Emergency Use**: If experiencing severe symptoms, call emergency services immediately.
```

---

## Analysis Process

### Step 1: Organize Information

Group collected data by the five dimensions:
- Symptoms answers → Primary symptoms, timeline, severity
- Severity answers → Urgency assessment, risk factors
- History answers → Medical background, medications
- Context answers → Lifestyle and environmental factors
- Care goals → Type of guidance needed

### Step 2: Identify Issues

Scan for:
- **Vague symptoms**: "not feeling well", "uncomfortable", "unusual"
- **Contradictions**: Severity vs. symptom description conflicts
- **Gaps**: No mention of timeline, no severity indicators discussed
- **Red flags**: Symptoms suggesting serious conditions

### Step 3: Assess Urgency

Based on the symptoms:
- Match symptoms to urgency categories (emergency, urgent, routine, preventive)
- Identify warning signs requiring immediate attention
- Consider risk factors and patient context
- Determine appropriate care provider and timeframe

### Step 4: Assess Risks

Consider:
- **Severity risks**: Symptoms that could indicate serious conditions
- **Progression risks**: Symptoms likely to worsen without intervention
- **Complication risks**: Potential for complications if untreated
- **Psychological risks**: Impact on mental health and wellbeing

---

## Best Practices

### Do:
- Organize scattered symptom information into clear structure
- Call out ambiguities explicitly with specific questions
- Provide rationale for urgency assessment
- Identify warning signs with clear escalation criteria
- Use disclaimers appropriately

### Don't:
- Make medical diagnoses (assess and guide only)
- Recommend specific treatments or medications
- Ignore red flags or downplay serious symptoms
- Over-reassure when medical evaluation is needed
- Skip risk assessment even for "minor" symptoms

---

## Success Criteria

This skill succeeds when:
- Symptoms are structured and clearly described
- All critical gaps and red flags are identified
- Urgency assessment is appropriate and justified
- Care recommendations are actionable
- The assessment enables informed healthcare decisions
