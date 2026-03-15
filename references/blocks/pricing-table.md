### PRICING_TABLE
**When**: `'price' in top_objections` OR `niche in ['hvac','plumbing','roofing','dental','financial']`
**Where**: After PATH_CHOICE, before PAYMENT_STRIP

**Content Model**:
```yaml
PRICING_TABLE:
  intro_text:
    required: true
    example: "No surprises. Every repair starts with a $89 diagnostic (waived if we do the work). We show you the problem, explain your options, and only proceed with your approval. If we can't fix it, you pay nothing."
    intent_mapping:
      emotional_driver: "Fear of price gouging, hidden fees"
      functional_driver: "Budget planning, informed decisions"

  diagnostic_fee:
    amount: "$89"
    waiver: "waived with repair"
    explanation: "Covers inspection, diagnosis, written estimate"

  common_repairs:
    max_count: 6
    structure:
      - service: "Filter & tune-up"
        price_range: "$95-150"
        includes: optional
        typical_time: optional
    prioritization: "Most common first, then by price"

  footer_note:
    required: true
    example: "Final pricing determined after diagnostic. Prices shown are typical for {area} and include parts & labor. We'll always get your approval before starting work."

meclabs_contribution:
  increases: [value_prop_3x]
  reduces: [friction_2x, anxiety_2x]
```
