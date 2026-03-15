### MID_CTA
**When**: `urgency in ['emergency', 'soon']` OR `stakes == 'high'`
**Where**: Around block 6-7, between content sections
**Purpose**: Slim inline CTA nudge without disrupting reading flow

**Content Model**:
```yaml
MID_CTA:
  layout: "Full-width slim bar (py-3, not py-5)"
  trust_point: "One social proof data point"
  cta: "Single low-friction action"

  examples:
    - trust: "Trusted by 500+ Frisco families"
      cta: "Call (469) 555-1234"
    - trust: "4.9 stars from 200+ Google reviews"
      cta: "Schedule Your Visit"
    - trust: "Serving North Texas since 1987"
      cta: "Get Help Today"

  cta_stage: "3 - Social Proof (see Progressive CTA System)"

  note: |
    This is NOT a full PRIMARY_CTAS section. It is a slim bar similar
    to AVAILABILITY_BADGE in visual weight. One trust point + one CTA.

meclabs_contribution:
  increases: [incentive_2x (act now with social proof)]
  reduces: [friction_2x (always-visible action)]
```
