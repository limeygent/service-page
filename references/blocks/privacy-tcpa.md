### PRIVACY_TCPA
**Purpose**: Legal consent for forms/SMS
**When**: Any form or click-to-text present
**Placement**: Adjacent to each data collection point

**Content Model**:
```yaml
PRIVACY_TCPA:
  instances: multiple (one per form)
  text: "By submitting, you agree to receive calls/texts about your service request. Reply STOP to opt out. Standard rates apply."
  links: ["Privacy Policy", "Terms"]
  classes: ["small", "text-muted"]
```
