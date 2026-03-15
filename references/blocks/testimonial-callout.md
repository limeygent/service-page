### TESTIMONIAL_CALLOUT
**When**: `review_count >= 3` AND `has_pricing_transparency == true`
**Where**: **STRATEGIC POSITION - After PATH_CHOICE, before PRICING_TABLE**
**Priority**: **MEDIUM - 5-7% conversion lift through strategic placement**

**Why separate from REVIEWS_CAROUSEL:**
Carousel provides volume for trust-building. Callout provides STRATEGIC single quote to pre-empt specific objection at critical moment.

**Content Model**:
```yaml
TESTIMONIAL_CALLOUT:
  purpose: "Reinforce honesty/transparency immediately before pricing"

  selection_criteria:
    themes: ["honest advice", "didn't upsell", "saved me money", "transparent pricing"]
    length: 120-180 characters
    must_include: [decision_point, honest_recommendation, outcome]
    example: "We were ready to replace our 13-year-old furnace after it quit. The tech was totally honest. Showed us it was just a $280 part and said we'd get another 5 years easy. Saved us thousands. That kind of honesty earns a customer for life."

  layout:
    width: "Centered, max-width col-lg-8"
    card: "border-0 shadow-sm"
    accent: "border-left: 4px solid var(--brand-primary)"

  elements:
    quote_icon:
      icon: "bi-chat-quote-fill fs-2"
      color: "var(--brand-primary)"
      position: "Left of content"

    rating:
      display: 5 stars
      position: "Above quote"

    attribution:
      name: "First Name L."
      location: "City, State"
      source: "Google Review"
      date: "Month Year"

  placement_psychology:
    position: "After repair vs replace discussion, before pricing"
    timing: "User is thinking: 'Will they upsell me?'"
    message: "We recommend what's best for YOU, not our bottom line"

meclabs_contribution:
  increases: [value_prop_3x (trust in transparency)]
  reduces: [anxiety_2x (fear of upselling), friction_2x (confidence in pricing)]

performance_data:
  conversion_lift: "5-7%"
  objection_pre_emption: "Highly effective"
```
