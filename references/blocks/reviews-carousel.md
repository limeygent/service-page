### REVIEWS_CAROUSEL
**When**: `review_count >= 20` AND `avg_rating >= 4.5` AND `urgency in ['emergency', 'soon']`
**Where**: After BRANDS_SYSTEMS, before SYMPTOM_MATRIX
**Priority**: **HIGH for emergency pages - social proof drives 20-25% conversion lift**

**Why separate from TESTIMONIAL:**
Carousel provides quantity (4-6 reviews) for trust-building, while single testimonial provides strategic placement. Emergency buyers need VOLUME of social proof early.

**Content Model**:
```yaml
REVIEWS_CAROUSEL:
  intro:
    heading: "What [City] Families Are Saying"
    aggregate_display: "⭐ 4.9 stars from 200+ Google reviews"

  reviews:
    min_count: 4
    max_count: 6
    optimal: 4 (fits desktop row)

    structure:
      - quote:
          max_length: 180
          must_include: [specific_situation, outcome, price_mention_optional]
          example: "Furnace died during the February freeze. They came within 2 hours and had us warm again by dinner. Price was exactly what they quoted: $320."

      - attribution:
          name: "First Name L."
          location: "City, State"
          source: "Google Review"
          date: "Month Year"

      - rating:
          display: 5 star icons (Bootstrap Icons bi-star-fill)
          color: text-warning (yellow stars)

  layout:
    desktop: 4 columns (col-lg-3)
    tablet: 2 columns (col-md-6)
    mobile: 1 column (col-12)
    card_height: h-100 (equal height)

  cta:
    text: "View All [count]+ Reviews"
    variant: btn-outline-danger or btn-outline-primary
    placement: centered below cards

  content_strategy:
    focus: Emergency experiences ("came within 2 hours", "fixed same day")
    include_prices: Yes (builds trust: "$400 for ignitor, exactly what they quoted")
    emotional_journey: Show stress → relief ("was so stressed, they calmed me down")
    avoid: Generic praise, lengthy stories, complaints

meclabs_contribution:
  increases: [motivation_4x (social proof), value_prop_3x (proof of claims)]
  reduces: [anxiety_2x (others succeeded), friction_2x (validation)]

performance_data:
  conversion_lift: "20-25% for emergency pages"
  bounce_reduction: "15%"
  time_on_page: "+45 seconds average"
```
