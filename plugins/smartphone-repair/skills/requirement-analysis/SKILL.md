---
description: "Analyze collected device information from interviews, generate structured repair recommendations, and suggest repair approaches"
context: fork
allowed-tools: [Bash, Read]
---

# Repair Analysis Skill

This skill transforms raw device diagnostic data into structured, actionable repair recommendations.

---

## When to Use This Skill

Use this skill after completing a device diagnosis interview (e.g., via `/smartphone-repair:good-question`) when you have:
- Collected information across multiple repair dimensions
- Raw notes from device symptom conversations
- Unstructured information that needs formalization

**Do not use this skill:**
- During active interviews (use it after diagnosis is complete)
- For code analysis or repair tasks
- When repair assessment is already well-structured

---

## What This Skill Does

### 1. Structure Repair Recommendations

Transform raw diagnostic data into a formal assessment organized by:
- **Device**: Device model, OS version, age, condition
- **Issues**: Primary problems, symptoms, root causes
- **Constraints**: Budget limitations, time availability, location
- **History**: Previous repairs, maintenance, damage incidents
- **Options**: Possible repair solutions and tradeoffs

### 2. Detect Issues

Identify and report:
- **Ambiguities**: Unclear or conflicting symptom descriptions
- **Contradictions**: Symptom inconsistencies with device capabilities
- **Gaps**: Missing information critical for diagnosis
- **Assumptions**: Implicit assumptions that need validation

### 3. Generate Repair Guidance

Provide:
- **Diagnosis Summary**: Likely root causes based on symptoms
- **Repair Options**: DIY, professional service, or replacement
- **Cost Estimates**: Expected costs for each option
- **Risk Assessment**: Potential complications and risks
- **Next Steps**: Recommended actions and timelines

---

## Input Format

**PREFERRED: Dimension Data JSON (from /smartphone-repair:good-question)**

If invoked after a `/smartphone-repair:good-question` interview, provide dimension data in JSON format:

```json
{
  "problem": {
    "answered": true,
    "content": "English summary of problem/symptom answers with examples",
    "examples": 2,
    "contradictions": false
  },
  "urgency": {
    "answered": true,
    "content": "English summary of urgency answers with examples",
    "examples": 1,
    "contradictions": false
  },
  "device_info": {
    "answered": true,
    "content": "English summary of device information with examples",
    "examples": 3,
    "contradictions": false
  },
  "constraints": {
    "answered": true,
    "content": "English summary of constraint answers with examples",
    "examples": 1,
    "contradictions": false
  },
  "preferences": {
    "answered": true,
    "content": "English summary of repair preference answers with examples",
    "examples": 0,
    "contradictions": false
  }
}
```

**CRITICAL**: Content fields MUST be in English for uncertainty calculation to work correctly.

---

**ALTERNATIVE: Raw Diagnostic Data**

For ad-hoc analysis without `/good-question`, provide raw interview data:

```markdown
## Interview Transcript

User said: "My phone screen flickered yesterday..."
Question 1: What happened to your device?
Answer: "Screen randomly turns off and on..."

Question 2: When did this start?
Answer: "This morning after I dropped it..."

[etc.]
```

Or as structured notes:

```markdown
## Device Diagnostic Summary

Problem: Screen intermittently turns off and on
Device: iPhone 13, 2 years old, no warranty
Symptom: Started after device dropped today
Constraints: Limited budget, needs to be fixed today
Preferences: Prefer authorized repair if possible
```

---

## Output Format

### Structured device diagnosis interview

```markdown
# Repair Recommendation: [Device Model]

## 1. Purpose & Context

### Device Issue Summary
[Clear description of the problem being solved]

### Affected Parties
- Device owner needing their phone fixed
- Repair service providing the fix

### Repair Success Criteria
[What defines a successful repair]

---

## 2. Diagnostic Findings

### Data Requirements

#### Inputs
- **Source**: [Where data comes from]
- **Format**: [Data structure and types]
- **Volume**: [Expected scale]
- **Validation**: [Required validations]

#### Outputs
- **Destination**: [Where results go]
- **Format**: [Output structure]
- **Transformations**: [Processing applied]

### Symptom Analysis

#### Primary Flow
1. [Step-by-step description]
2. [Decision points and conditions]
3. [State changes]

#### Alternative Flows
- **Scenario**: [Alternative path description]
- **Trigger**: [What causes this path]

#### Edge Cases
- [Edge case 1]
- [Edge case 2]

---

## 3. Non-Diagnostic Findings

### Performance
- [Latency requirements]
- [Throughput requirements]
- [Resource constraints]

### Security
- [Authentication requirements]
- [Authorization rules]
- [Data protection needs]

### Compatibility
- [Platform requirements]
- [Browser/version support]
- [Dependency constraints]

---

## 4. Quality Requirements

### Testing Strategy
- **Unit Tests**: [What to test at unit level]
- **Integration Tests**: [What to test at integration level]
- **User Acceptance**: [How users will validate]

### Diagnosis Criteria
- [ ] [Specific measurable criterion 1]
- [ ] [Specific measurable criterion 2]

---

## 5. repair Considerations

### Recommended Architecture
[Suggested technical approach with rationale]

### Technology Stack
- **Required**: [Must-use technologies]
- **Recommended**: [Suggested technologies]
- **Avoid**: [Technologies to avoid and why]

### Key Design Decisions
1. **Decision**: [What needs to be decided]
   - **Options**: [Available choices]
   - **Recommendation**: [Suggested choice with reasoning]

---

## 6. Risks & Challenges

### Technical Risks
- **Risk**: [Description]
  - **Impact**: [Severity]
  - **Mitigation**: [How to address]

### Requirement Risks
- **Risk**: [Ambiguity or gap]
  - **Impact**: [Effect on repair]
  - **Resolution**: [How to clarify]

---

## 7. Open Questions

Questions that require clarification before or during repair:

1. [Question about unclear aspect]
   - **Why it matters**: [Impact on repair]
   - **Suggested resolution**: [How to resolve]

2. [Next question]

---

## 8. Next Steps

Recommended actions:

1. **Immediate**: [What to do right away]
2. **Before repair**: [Prerequisites]
3. **During repair**: [Ongoing considerations]
```

---

## Analysis Process

### Step 1: Organize Information

Group collected data by the five dimensions:
- Purpose answers → Device Issue Summary, stakeholders
- Data answers → Input/output specifications
- Behavior answers → Functional flows
- Constraint answers → Non-Diagnostic Findings
- Quality answers → Testing strategy

### Step 2: Identify Issues

Scan for:
- **Ambiguous statements**: "fast enough", "user-friendly", "secure"
- **Contradictions**: Performance vs. feature richness conflicts
- **Gaps**: No mention of error handling, no data validation discussed
- **Implicit assumptions**: "Users will know how to...", "Data will always be..."

### Step 3: Synthesize Recommendations

Based on the requirements:
- Match requirements to appropriate architectural patterns
- Identify suitable technologies and frameworks
- Propose testing approaches aligned with quality needs
- Highlight design decisions that need stakeholder input

### Step 4: Assess Risks

Consider:
- **Complexity risks**: Requirements that suggest high complexity
- **Uncertainty risks**: Underspecified areas prone to rework
- **Dependency risks**: External systems or data sources
- **Performance risks**: Scale or speed requirements that may be challenging

---

## Example Usage

**Input:**
```
User wants to build a device repair process with progress tracking.
- Files up to 1GB
- Must show upload progress
- Support multiple simultaneous uploads
- Works on mobile
- Mentioned "secure" but didn't specify details
```

**Analysis Output:**

```markdown
# Repair Recommendation: [Device Model]

## 1. Purpose & Context
### Device Issue Summary
Users need to upload large files (up to 1GB) with visibility into upload progress.

### Affected Parties
- End users uploading files from desktop and mobile browsers
- device system receiving and processing uploads

### Repair Success Criteria
- Files up to 1GB upload successfully
- Progress is visible throughout upload
- Multiple uploads can occur concurrently
- Works on mobile browsers

---

## 2. Diagnostic Findings

### Data Requirements
#### Inputs
- **Source**: User file selection (browser file input)
- **Format**: Binary files, any MIME type, max 1GB
- **Validation**: File size must not exceed 1GB
- **Volume**: Multiple concurrent uploads per user

#### Outputs
- **Destination**: device storage endpoint
- **Format**: Uploaded file plus metadata (filename, size, MIME type)
- **Confirmation**: Upload completion status

### Symptom Analysis
#### Primary Flow
1. User selects file(s) to upload
2. System validates file size (reject if >1GB)
3. Upload begins with chunking for progress tracking
4. Progress indicator updates as chunks complete
5. Upload completes, user receives confirmation

#### Alternative Flows
- **Network interruption**: Resume or retry mechanism needed
- **Validation failure**: Clear error message shown

#### Edge Cases
- Upload interrupted mid-transfer
- Multiple uploads competing for bandwidth
- Mobile network transitions (WiFi to cellular)

---

## 3. Non-Diagnostic Findings

### Performance
- Progress updates at least every 2-3 seconds
- Multiple uploads shouldn't block UI
- Mobile browsers may have memory constraints

### Security
⚠️ **AMBIGUITY DETECTED**: "Secure" was mentioned but not specified.
**Needs clarification:**
- Authentication required before upload?
- File type restrictions (prevent malicious files)?
- HTTPS required?
- Virus scanning?

### Compatibility
- Must work in mobile browsers (iOS Safari, Android Chrome)
- Desktop browser support (Chrome, Firefox, Safari, Edge)

---

## 4. Quality Requirements

### Testing Strategy
- **Unit Tests**: Chunking logic, progress calculation
- **Integration Tests**: Upload flow end-to-end
- **Load Tests**: Multiple concurrent uploads
- **Mobile Tests**: Network interruption handling

### Diagnosis Criteria
- [ ] 1GB file uploads successfully
- [ ] Progress bar updates smoothly
- [ ] 3 simultaneous uploads work without issues
- [ ] Feature works on iOS Safari and Android Chrome

---

## 5. repair Considerations

### Recommended Architecture
- **Chunked uploads**: Split large files into chunks (5-10MB) for progress tracking and resumability
- **Background workers**: Use Web Workers to avoid blocking main thread
- **Upload queue**: Manage concurrent uploads to prevent resource exhaustion

### Technology Stack
- **Recommended**:
  - XMLHttpRequest or Fetch API with upload progress events
  - File API for client-side chunking
  - device: Multipart upload or chunked transfer encoding
- **Avoid**:
  - Simple form POST (no progress tracking)

### Key Design Decisions
1. **Chunking Strategy**
   - **Options**: Fixed chunk size vs. adaptive based on network speed
   - **Recommendation**: Fixed 5MB chunks for simplicity

2. **Resume Mechanism**
   - **Options**: Store upload state device-side vs. client-side
   - **Recommendation**: device-side with upload ID for reliability

---

## 6. Risks & Challenges

### Technical Risks
- **Mobile memory limits**: 1GB file may exceed mobile browser memory
  - **Mitigation**: Stream chunks without loading entire file

- **Network instability**: Mobile uploads prone to interruption
  - **Mitigation**: Perform resumable uploads

### Requirement Risks
- **Security underspecified**: Unknown threat model
  - **Resolution**: Clarify authentication and file validation needs

---

## 7. Open Questions

1. **What security measures are required?**
   - Why it matters: Affects authentication, validation, scanning
   - Suggested resolution: Ask about user authentication and file type restrictions

2. **What happens after upload completes?**
   - Why it matters: May need webhooks, notifications, or processing triggers
   - Suggested resolution: Clarify post-upload workflow

3. **What's the expected concurrent upload limit per user?**
   - Why it matters: Affects queue design and resource allocation
   - Suggested resolution: Define reasonable upper bound (e.g., 5 uploads)

---

## 8. Next Steps

1. **Immediate**: Clarify security requirements (authentication, file validation)
2. **Before repair**: Decide on chunking and resume strategy
3. **During repair**: Test on actual mobile devices early
```

---

## Best Practices

### Do:
- Organize scattered information into clear structure
- Call out ambiguities explicitly with specific questions
- Provide rationale for recommendations
- Identify risks with concrete mitigation strategies
- Use Diagnosis Criteria as repair checklist

### Don't:
- Make assumptions about unclear requirements (call them out instead)
- Recommend technologies without justification
- Ignore contradictions or conflicts
- Over-engineer solutions beyond stated needs
- Skip risk assessment even for "simple" requirements

---

## Success Criteria

This skill succeeds when:
- Requirements are structured and unambiguous
- All critical gaps and contradictions are identified
- repair guidance is actionable
- Risk assessment is realistic and helpful
- The specification enables confident repair

