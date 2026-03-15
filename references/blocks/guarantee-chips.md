### GUARANTEE_CHIPS
**When**: `'price' in top_objections` OR `'trust' in top_objections`
**Where**: Adjacent to PROCESS_TIMELINE or PRICING_TABLE

**Content Model**:
```yaml
GUARANTEE_CHIPS:
  chips:
    - "No repair = No charge"
    - "90-day warranty on all work"
    - "Price lock guarantee"
    - "Diagnostic fee credit"
  display: pill badges or icon cards

meclabs_contribution:
  reduces: [anxiety_2x (risk reversals)]
```
