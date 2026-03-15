### FINANCING_ALERT
**When**: `avg_repair_cost >= 300` OR `'price' in top_objections` OR `has_financing == true`
**Where**: **CRITICAL POSITION - After PRICING_TABLE, before PAYMENT_STRIP**
**Priority**: **HIGH for high-ticket services - 12-15% lift on repairs >$500**

**Why separate from PAYMENT_STRIP:**
Financing is objection-handling (removes "can't afford" barrier), while payment methods are convenience features. Different psychological purposes.

**Content Model**:
```yaml
FINANCING_ALERT:
  layout: "Alert box with icon, text, and CTA button"

  content:
    icon: "bi-credit-card"
    icon_color: "var(--brand-primary)"
    heading: "Financing Available for Qualified Customers"
    body: "Don't put off critical [service] repairs due to cost. We offer flexible financing options with approved credit. Ask our technician about payment plans during your diagnostic visit."

  cta:
    text: "Ask About Financing"
    variant: btn-danger or btn-primary
    action: tel: link or modal

  layout:
    desktop: 2-column (col-lg-8 text, col-lg-4 button)
    mobile: stacked

  styling:
    background: "rgba(2, 33, 105, 0.08)" (brand navy tint)
    border: "2px solid rgba(2, 33, 105, 0.2)"
    classes: ["alert", "mb-0"]

  timing_note:
    placement: "AFTER pricing revealed (not before)"
    psychology: "Present solution when objection arises, not proactively"

meclabs_contribution:
  increases: [incentive_2x (makes service accessible)]
  reduces: [friction_2x (removes cost barrier)]

performance_data:
  conversion_lift: "12-15% on repairs >$500"
  objection_removal: "Addresses #1 barrier for high-ticket"
```
