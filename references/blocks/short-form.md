### SHORT_FORM
**When**: `intent_primary != 'research'`
**Where**: HERO right column OR row after HERO

**Content Model**:
```yaml
SHORT_FORM:
  heading: "Get a Free Diagnosis Today"
  subheading: "We'll call you within 15 minutes"

  fields:
    minimal:
      - name: text, required
      - phone: tel, required, pattern

    standard:
      - name, phone (required)
      - issue: select dropdown
      - preferred_time: select

  submit:
    text: "Get Help Now"
    classes: ["btn-danger" if emergency else "btn-primary", "btn-lg", "w-100"]

  privacy: adjacent PRIVACY_TCPA

meclabs_contribution:
  reduces: [friction_2x (minimal fields)]
```
