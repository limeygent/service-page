### SYMPTOM_MATRIX
**When**: `niche in ['hvac','plumbing','dental']`
**Where**: Mid, before PATH_CHOICE and PRICING_TABLE

**Content Model**:
```yaml
SYMPTOM_MATRIX:
  intro_text:
    example: "Is your heater acting up? Here's what those strange noises, weak airflow, or cycling issues usually mean, and what it typically costs to fix. Use this to decide if you need emergency service or can wait until morning."
    intent_mapping:
      emotional_driver: "Uncertainty about severity, DIY capability"
      functional_driver: "Self-diagnosis, urgency assessment, cost estimation"

  symptoms:
    type: map
    max_count: 6
    structure:
      symptom_description:
        likely_causes: [cause1, cause2]
        price_range: "$95-350"
        urgency: [wait, schedule_today, emergency]
        explanation: "What this means for you"

    examples:
      "Not blowing hot air":
        causes: ["Pilot light out", "Thermostat issue"]
        price: "$95-350"
        urgency: schedule_today
        note: "Usually fixable within an hour. Not dangerous, but home won't warm up."

  responsive:
    mobile: accordion
    tablet: card_grid
    desktop: table

meclabs_contribution:
  increases: [value_prop_3x]
  reduces: [friction_2x, anxiety_2x]
```
