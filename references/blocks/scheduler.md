### SCHEDULER
**When**: `has_scheduler == true` AND `intent_primary != 'research'`
**Where**: After PRICING/PAYMENT, before FAQ

**Content Model**:
```yaml
SCHEDULER:
  embed_type: [calendly, acuity, custom]
  heading: "Choose Your Time Slot"
  options:
    - "Today (Emergency)"
    - "Tomorrow AM/PM"
    - "Schedule Later"
  adjacent: PRIVACY_TCPA (if collects data)

meclabs_contribution:
  reduces: [friction_2x (eliminates phone tag)]
```
