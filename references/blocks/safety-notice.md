### SAFETY_NOTICE
**When**: `safety_hazard_possible == true` OR `(niche == 'hvac' AND outage_severity == 'no_heat')`
**Where**: **CRITICAL - Row 2 or 3 MAXIMUM. MUST appear before ANY diagnostic/educational content**
**Priority**: **LIFE SAFETY - Overrides all other positioning preferences**

**CRITICAL POSITIONING RULE:**
```
SAFETY_NOTICE must appear BEFORE:
- SYMPTOM_MATRIX
- PATH_CHOICE
- Any "Common Causes" or educational content
- BRANDS_SYSTEMS (if educational)

Violation creates life-threatening risk - user may read educational
content while experiencing gas leak or CO exposure.
```

**Content Model**:
```yaml
SAFETY_NOTICE:
  alert_text:
    max_length: 80
    example: "⚠️ Smell gas or see soot? Turn off system and call immediately"

  explanation_text:
    example: "Carbon monoxide is colorless and odorless. If you notice soot buildup or burning smells, your system may have incomplete combustion: a safety hazard requiring immediate attention."
    intent_mapping:
      emotional_driver: "Fear of invisible danger, family safety"
      functional_driver: "Know when to evacuate vs troubleshoot"

  action_steps:
    max_count: 4
    examples:
      - "Turn off heating system at thermostat"
      - "Open windows if you smell gas"
      - "Check CO detectors are working"
      - "Call us or 911 if you feel lightheaded"

  styling:
    background: "rgba(220, 53, 69, 0.1)" (danger red, not brand red)
    border: "border-start border-5 border-danger"
    note: "Use Bootstrap danger color to distinguish from brand colors - this is life-critical"

meclabs_contribution:
  increases: [motivation_4x]
  reduces: [anxiety_2x (gives control)]
```
