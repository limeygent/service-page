### AWARD_BADGES
**When**: `review_count >= 50` OR `years_in_business >= 10` OR `has_bbb_rating == true`
**Where**: Top of TRUST section (row with CREDENTIALS_LICENSES)
**Priority**: **MEDIUM-HIGH - 8-10% credibility boost**

**Content Model**:
```yaml
AWARD_BADGES:
  layout: "Full-width centered row above credentials"
  heading: "Trusted by [Region] Homeowners"

  badges:
    types:
      logo_badges:
        - type: "BBB Rating"
          image: "bbb-a-plus.png"
          text: "A+ Rated"
          subtext: "Better Business Bureau"

        - type: "Industry Certification"
          image: "nate-certified.png"
          text: "NATE Certified"
          subtext: "Technicians"

      stat_badges:
        - type: "Years in Business"
          number: "38"
          display: "display-4 fw-bold"
          color: "var(--brand-primary)"
          text: "Years in Business"
          subtext: "Since 1987"

        - type: "Customer Count"
          number: "2K+"
          display: "display-4 fw-bold"
          color: "var(--brand-primary)"
          text: "Satisfied Customers"
          subtext: "[Region] Area"

  responsive:
    desktop: 4 columns (col-md-3)
    tablet: 2 columns (col-6)
    mobile: 2 columns (col-6)

  styling:
    logos: .brand-logo class (grayscale with hover)
    numbers: Large display font in brand color
    spacing: mb-5 (separates from credentials below)

meclabs_contribution:
  increases: [value_prop_3x (authority signals)]
  reduces: [anxiety_2x (legitimacy, longevity)]

performance_data:
  conversion_lift: "8-10%"
  trust_score_increase: "significant"
```
