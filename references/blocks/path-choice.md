### PATH_CHOICE
**When**: `niche in ['hvac','roofing','dental','financial']` OR `'price' in top_objections`
**Where**: After SYMPTOM_MATRIX, before PRICING_TABLE

**Content Model**:
```yaml
PATH_CHOICE:
  title: "Repair vs Replace?"

  repair:
    when: ["Under 10 years old", "First major issue", "Single component failure"]
    cost: "$200-1,200 typical"
    pros: ["Lower upfront cost", "Quick fix", "Extends life 2-5 years"]

  replace:
    when: ["15+ years old", "Frequent repairs", "Efficiency loss"]
    cost: "$3,500-7,000 typical"
    pros: ["10-15 year warranty", "Lower energy bills", "Modern features"]

  decision_support:
    text: "We'll walk you through the math with no pressure either way"

meclabs_contribution:
  increases: [value_prop_3x]
  reduces: [anxiety_2x (education, no pressure)]
```
