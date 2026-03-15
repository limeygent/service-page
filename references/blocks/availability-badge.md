### AVAILABILITY_BADGE
**When**: `urgency in ['emergency','soon']` OR `'speed' in top_objections`
**Where**: Inside HERO or row directly below

**Content Model**:
```yaml
AVAILABILITY_BADGE:
  text: "🚐 {tech_count} technicians available today in {city}"
  subtext: "Average arrival: {response_time_hours} hours"
  dynamic: true (if live data available)

meclabs_contribution:
  increases: [incentive_2x (act now)]
  reduces: [friction_2x (availability confirmed)]
```
