### TESTIMONIAL
**When**: `review_count >= 1`
**Where**: After decision aids, before FAQ

**Content Model**:
```yaml
TESTIMONIAL:
  quote:
    max_length: 180
    must_include: [specific situation, outcome, timeframe]
    example: "Furnace died during the February freeze. They came within 2 hours and had us warm again by dinner. The tech explained everything and didn't upsell us."

  attribution:
    author: "First Name L." (privacy)
    location: "McKinney"
    date: "February 2024"
    image: optional (headshot or initials badge)

  compliance:
    disclosure_required: true (if regulatory_disclosures_required)
    text: "Individual results may vary."

meclabs_contribution:
  increases: [motivation_4x]
  reduces: [anxiety_2x]
```
