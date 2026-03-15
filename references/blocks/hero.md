### HERO
**Purpose**: Declare service/location + surface primary CTAs
**When**: Always
**Layout**: 2-column asymmetric (text 60-70%, form/image 30-40%)

**Content Model**:
```yaml
HERO:
  heading:
    type: string
    max_length: 60
    formula: "[Service] in [Location]" or "[Pain Point Solved] in [Location]"
    examples:
      emergency: "Emergency Heater Repair in McKinney, TX"
      cost_focused: "Honest HVAC Repair in McKinney - No Hidden Fees"
      trust_focused: "Licensed Heater Repair in McKinney Since 1987"

  subhead:
    type: string
    max_length: 120
    purpose: "Value prop + differentiator + trust signal"
    examples:
      - "Certified HVAC technicians serving DFW since 1987"
      - "Same-day emergency response with upfront pricing"

  explanation_text:
    required: true
    length: "120-180 characters"
    formula: "[Acknowledge pain] + [Your solution] + [Why it matters]"
    example: "When your heater fails during a North Texas winter, every minute matters. Our licensed technicians carry common parts and can diagnose most issues within the first visit, meaning you're back to warmth faster."
    intent_mapping:
      emotional_driver: "Fear of prolonged discomfort, family safety anxiety"
      functional_driver: "Fast resolution, minimize downtime"
      trust_signal: "Licensed, prepared, experienced"

  badges:
    max_count: 3
    examples:
      - text: "Licensed & Insured"
        icon: "shield-check"
        tooltip: "TACLB00024715E"
      - text: "Same-Day Service"
        icon: "clock-fast"
      - text: "4.8★ Rating"
        icon: "star-fill"

  ctas:
    - text: "Call [phone]"
      variant: "primary"
      size: "lg"
      icon: "telephone-fill"
      meclabs_role: "friction_reducer"
    - text: "Schedule Online"
      variant: "outline-primary"
      size: "lg"
      icon: "calendar-check"
      meclabs_role: "convenience_option"

  image:
    display: optional (desktop only if text-heavy)
    type: "Technician at work or equipment close-up"
    lazy: false

meclabs_contribution:
  increases: [motivation_4x, value_prop_3x]
  reduces: [friction_2x (direct action)]
```
