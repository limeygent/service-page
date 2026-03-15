### PROCESS_TIMELINE
**Purpose**: Set expectations, reduce uncertainty
**When**: Always
**Placement**: Mid-page, before FAQ

**Content Model**:
```yaml
PROCESS_TIMELINE:
  intro_text:
    required: true
    example: "From your first call to fixed and tested, here's exactly what to expect. No surprises, no pressure."
    intent_mapping:
      emotional_driver: "Uncertainty about process, loss of control"
      functional_driver: "Know what to prepare, timeline expectations"

  steps:
    min_count: 4
    max_count: 7
    structure:
      - step_number: 1
        title: "Call or Book Online"
        description: "We'll ask about your issue and schedule a visit, often same-day"
        icon: "telephone"
        duration: optional
    examples:
      step_1: "Call/Book" → "Schedule within your availability"
      step_2: "Diagnostic" → "Licensed tech inspects and explains ($89, waived with repair)"
      step_3: "Pricing" → "Exact costs before work begins"
      step_4: "Approval" → "You decide, no obligation"
      step_5: "Repair" → "Fixed right the first time"
      step_6: "Verify" → "Test, clean, confirm working"

meclabs_contribution:
  increases: [value_prop_3x]
  reduces: [friction_2x, anxiety_2x]
```
