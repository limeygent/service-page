### PAYMENT_STRIP
**When**: `has_financing == true` OR `'price' in top_objections`
**Where**: After PRICING_TABLE, before SCHEDULER

**Content Model**:
```yaml
PAYMENT_STRIP:
  accepted: [Visa, MC, Amex, Discover, Check, Cash]
  financing:
    available: true
    terms: "0% for 12 months (OAC)"
    link: "See terms"
  display: logo strip + text

meclabs_contribution:
  increases: [incentive_2x]
  reduces: [friction_2x (payment options)]
```
