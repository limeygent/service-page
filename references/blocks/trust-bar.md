### TRUST_BAR
**When**: Always recommended for high-stakes niches (`stakes == 'high'` OR `niche in ['dental', 'medical', 'pediatric_medical', 'personal_injury']`)
**Where**: Immediately after HERO (row 2)
**Purpose**: Quick-scan trust signals in a slim horizontal bar

**Content Model**:
```yaml
TRUST_BAR:
  stats:
    min_count: 3
    max_count: 5
    structure:
      - number: "5.0"
        label: "Google Reviews"
        icon: "star-fill"
    examples:
      - {number: "4.9", label: "Google Rating", icon: "star-fill"}
      - {number: "15+", label: "Years Experience", icon: "calendar-check"}
      - {number: "Same Day", label: "Appointments", icon: "clock"}

  layout: "Full-width slim bar (py-2 or py-3)"

meclabs_contribution:
  increases: [value_prop_3x (instant credibility)]
  reduces: [anxiety_2x (quick proof)]
```
