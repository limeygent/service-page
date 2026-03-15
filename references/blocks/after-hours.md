### AFTER_HOURS
**When**: `has_after_hours == true` OR `urgency == 'emergency'`
**Where**: ops_row OR near HERO, before FAQ

**Content Model**:
```yaml
AFTER_HOURS:
  text: "No heat emergency? We're on-call 24/7 with no extra charge for evening service until 8pm"
  premium_hours: "After 8pm: +$50"
```
