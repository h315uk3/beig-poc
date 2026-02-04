---
description: "Analyze collected crop planning information from interviews, detect ambiguities, generate structured specifications, and suggest implementation approaches"
context: fork
allowed-tools: [Bash, Read]
---

# Crop Planning Analysis Skill

This skill transforms raw crop planning interview data into structured, actionable crop planning specifications.

---

## When to Use This Skill

Use this skill after completing a crop planning interview (e.g., via `/crop-planning:good-question`) when you have:
- Collected answers across multiple crop planning dimensions
- Raw notes from farmer conversations
- Unstructured information that needs formalization

**Do not use this skill:**
- During active interviews (use it after information gathering is complete)
- For code analysis or implementation tasks
- When crop plans are already well-structured

---

## What This Skill Does

### 1. Structure Crop Plans

Transform raw interview data into a formal specification organized by:
- **Location**: Climate zone, location details, growing conditions
- **Soil**: Soil type, pH, nutrients, soil composition
- **Market**: Demand, pricing, sales channels, market analysis
- **Constraints**: Budget, land size, labor availability, regulations
- **Sustainability**: Environmental goals, organic practices, water usage

### 2. Detect Issues

Identify and report:
- **Ambiguities**: Vague climate descriptions, unclear market demands
- **Contradictions**: Climate unsuitable for requested crops, resource conflicts
- **Gaps**: Missing soil data, no market research done
- **Assumptions**: Implicit assumptions about water availability, local climate patterns

### 3. Generate Crop Recommendations

Provide:
- **Crop Selection**: Recommended crops for the farmer's situation
- **Risk Assessment**: Potential challenges (weather, pests, market conditions)
- **Cultivation Strategy**: Planting schedule, care requirements
- **Open Questions**: Information gaps that need clarification

---

## Input Format

**PREFERRED: Dimension Data JSON (from /crop-planning:good-question)**

If invoked after a `/crop-planning:good-question` interview, provide dimension data in JSON format:

```json
{
  "location": {
    "answered": true,
    "content": "English summary of location answers with examples",
    "examples": 2,
    "contradictions": false
  },
  "soil": {
    "answered": true,
    "content": "English summary of soil answers with examples",
    "examples": 1,
    "contradictions": false
  },
  "market": {
    "answered": true,
    "content": "English summary of market answers with examples",
    "examples": 3,
    "contradictions": false
  },
  "constraints": {
    "answered": true,
    "content": "English summary of constraints answers with examples",
    "examples": 1,
    "contradictions": false
  },
  "sustainability": {
    "answered": true,
    "content": "English summary of sustainability answers with examples",
    "examples": 0,
    "contradictions": false
  }
}
```

**CRITICAL**: Content fields MUST be in English for uncertainty calculation to work correctly.

---

**ALTERNATIVE: Raw Interview Data**

For ad-hoc analysis without `/crop-planning:good-question`, provide raw interview data:

```markdown
## Interview Transcript

Farmer said: "I want to grow vegetables for local markets..."
Question 1: What's your climate zone?
Answer: "Temperate, cold winters..."

Question 2: How much land do you have?
Answer: "About 2 acres..."

[etc.]
```

Or as structured notes:

```markdown
## Collected Information

Location: Temperate climate, zone 6, cold winters
Soil: Well-drained, slightly acidic (pH 6.5)
Market: Local farmer's market, looking for good income
Constraints: 2 acres of land, limited labor
Sustainability: Interested in organic certification
```

---

## Output Format

### Structured Crop Planning Specification

```markdown
# Crop Planning Specification: [Farm Name/Location]

## 1. Farm Overview & Context

### Location & Climate
[Description of location, climate zone, weather patterns]

### Available Resources
[Land size, soil type, water availability, labor]

### Primary Goals
[What farmer wants to achieve - income, food, sustainability, etc.]

---

## 2. Recommended Crops

### Primary Crop Selections

1. **[Crop Name]** (Best Match)
   - **Why this crop**: [Climate suitability, market demand, profitability]
   - **Growing season**: [Planting to harvest timeline]
   - **Land required**: [Acres or area]
   - **Expected yield**: [Production estimates]
   - **Market value**: [Pricing and sales potential]

2. **[Secondary Crop]**
   - [Same details]

3. **[Tertiary Crop]**
   - [Same details]

---

## 3. Growing Requirements

### Soil Requirements
- **pH**: [Optimal range]
- **Nutrients**: [Required levels]
- **Amendments needed**: [What to add to current soil]

### Water & Climate Needs
- **Water requirements**: [Gallons/inches per season]
- **Temperature ranges**: [Min/max optimal]
- **Frost dates**: [Last spring / first fall frost]

### Labor & Care
- **Planting labor**: [Person-hours needed]
- **Maintenance**: [Weekly/monthly requirements]
- **Harvesting**: [Timeline and labor needed]

---

## 4. Market & Economics

### Revenue Projections
- **Expected yield**: [Units per acre]
- **Market price**: [Per unit price]
- **Expected revenue**: [Annual income estimate]

### Cost Structure
- **Seed/starts**: [Cost]
- **Soil amendments**: [Cost]
- **Labor**: [Cost]
- **Equipment**: [Cost]
- **Total estimated cost**: [Bottom line]

### Profitability Analysis
- **Gross profit**: [Revenue - Cost]
- **Break-even timeline**: [When profitable]
- **Payback period**: [Time to recoup investment]

---

## 5. Risk Assessment

### Climate Risks
- **Risk**: [Description]
  - **Impact**: [Severity]
  - **Mitigation**: [How to address]

### Market Risks
- **Risk**: [Market saturation, price volatility, etc.]
  - **Impact**: [Effect on profitability]
  - **Mitigation**: [Diversification strategy, contracts, etc.]

### Operational Risks
- **Risk**: [Pest pressures, disease, labor shortage, etc.]
  - **Impact**: [Crop failure probability]
  - **Mitigation**: [Prevention and management strategies]

---

## 6. Planting Schedule

### Recommended Timeline

**Spring**
- [Month]: [Crop 1 planting]
- [Month]: [Crop 2 planting]

**Summer**
- [Month]: [Harvesting/maintenance]

**Fall**
- [Month]: [Crop 3 planting / Crop 1 harvesting]

**Winter**
- [Month]: [Planning / soil preparation for spring]

---

## 7. Implementation Roadmap

### Phase 1: Preparation (Before Planting)
1. [Soil testing and amendment]
2. [Seed/start procurement]
3. [Equipment acquisition]

### Phase 2: Planting (Spring)
1. [Soil preparation]
2. [Planting timeline]
3. [Initial care]

### Phase 3: Growing Season (Summer)
1. [Maintenance schedule]
2. [Pest/disease monitoring]
3. [Watering strategy]

### Phase 4: Harvest & Sell
1. [Harvest timing and method]
2. [Market logistics]
3. [Sales process]

---

## 8. Open Questions

Questions that need clarification before final commitment:

1. **[Question about market demand]**
   - Why it matters: [Impact on profitability]
   - Suggested resolution: [How to research/validate]

2. **[Question about resources]**
   - Why it matters: [Impact on feasibility]
   - Suggested resolution: [How to determine availability]

---

## 9. Sustainability Considerations

- **Water usage**: [Conservation strategies]
- **Organic certification**: [Path to certification if desired]
- **Soil health**: [Long-term sustainability practices]
- **Environmental impact**: [Positive/negative externalities]

---

## 10. Next Steps

1. **Immediate**: [Validate crop choices with local agricultural extension]
2. **Before Planting**: [Prepare soil, procure seeds]
3. **First Season**: [Document yields, learn from experience]
4. **Ongoing**: [Refine strategy based on results]
```

---


## Example Usage

**Input:**
```
Farmer wants to grow crops for local farmer's market in zone 6.
- Has 2 acres of land
- Slightly acidic, well-drained soil
- Good rainfall, some irrigation available
- Can do most labor themselves, limited hired help
- Interested in certified organic
- Wants to maximize income
```

**Analysis Output Summary:**

# Crop Planning Specification: Johnson Family Farm

## Recommended Crops
1. **Tomatoes** (0.75 acres) - Zone 6 varieties thrive, strong farmer's market demand
2. **Lettuce & Mixed Greens** (0.5 acres) - High-demand, 4-6 week cycles, year-round potential
3. **Squash & Zucchini** (0.75 acres) - Prolific, long season, manageable water needs

## Financial Projections
- **Total Revenue**: $133,750 (all crops combined)
- **Total Costs**: $15,300 (seeds, amendments, labor, irrigation)
- **Gross Profit**: $118,450
- **Break-even**: Year 1 if market channels established

## Key Recommendations
- Install drip irrigation (reduces water use 30-50%, critical for summer crops)
- Pursue organic certification ($800-1,000/year investment, 20-40% price premium)
- Develop direct relationships with local restaurants (better margins than farmers market)
- Use crop rotation to manage pests and soil health

## Open Questions to Resolve
1. What farmer's markets are available? (Affects volume/pricing)
2. Restaurant sales opportunity? (Better margins)
3. Organic certification timeline needed?
4. Irrigation infrastructure current status?

---

## Best Practices

### Do:
- Organize scattered information into clear structure
- Call out ambiguities explicitly with specific questions
- Provide rationale for crop recommendations
- Identify risks with concrete mitigation strategies
- Use financial projections and market research to validate recommendations

### Don't:
- Make assumptions about unclear farm conditions (call them out instead)
- Recommend crops without climate/soil validation
- Ignore contradictions or conflicts (e.g., water-intensive crops in dry climate)
- Over-engineer solutions beyond farmer's realistic capacity
- Skip risk assessment even for "simple" growing situations

---

## Success Criteria

This skill succeeds when:
- Crop selections are well-suited to climate, soil, and goals
- All critical gaps and risks are identified
- Market and financial guidance is realistic
- Risk assessment includes both mitigation strategies
- The specification enables confident planting decisions
