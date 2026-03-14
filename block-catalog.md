# Block Catalog

Complete catalog of page blocks with conditional logic, content models, and MECLABS contributions.

## Progressive CTA System

CTAs must evolve as the reader scrolls and accumulates trust. Never use the same CTA text twice on a page.

| Stage | Position | Reader State | CTA Strategy | Example |
|-------|----------|-------------|--------------|---------|
| 1. Intent-Matching | HERO | Just arrived, zero trust | Match dominant intent | Emergency: "Call Now". Planning: "Schedule Free Consultation" |
| 2. Service-Specific | After SYMPTOM_MATRIX or condition content | Knows your scope | Narrow to their likely need | "Schedule Your [Specific Service] Visit" |
| 3. Social Proof | MID_CTA bar (block 6-7) | Has differentiation + some trust | Trust-leveraging nudge | "Join 500+ [City] families who trust us" |
| 4. Objection-Handling | After REVIEWS | Seen peer validation | Address remaining barrier | "No obligation, no pressure" |
| 5. Closing Argument | FINAL_CTA | Consumed everything | Reference specific value prop from page | "Ready for same-day relief in [City]?" |

See `references/content-templates.md` → "Progressive CTA Copy Patterns" for full copy examples per stage.

---

## Required Blocks (Always Include)

### HERO
**Purpose**: Declare service/location + surface primary CTAs  
**When**: Always  
**Layout**: 2-column asymmetric (text 60-70%, form/image 30-40%)

**Content Model**:
```yaml
HERO:
  heading:
    type: string
    max_length: 60
    formula: "[Service] in [Location]" or "[Pain Point Solved] in [Location]"
    examples:
      emergency: "Emergency Heater Repair in McKinney, TX"
      cost_focused: "Honest HVAC Repair in McKinney - No Hidden Fees"
      trust_focused: "Licensed Heater Repair in McKinney Since 1987"
  
  subhead:
    type: string
    max_length: 120
    purpose: "Value prop + differentiator + trust signal"
    examples:
      - "Certified HVAC technicians serving DFW since 1987"
      - "Same-day emergency response with upfront pricing"
  
  explanation_text:
    required: true
    length: "120-180 characters"
    formula: "[Acknowledge pain] + [Your solution] + [Why it matters]"
    example: "When your heater fails during a North Texas winter, every minute matters. Our licensed technicians carry common parts and can diagnose most issues within the first visit, meaning you're back to warmth faster."
    intent_mapping:
      emotional_driver: "Fear of prolonged discomfort, family safety anxiety"
      functional_driver: "Fast resolution, minimize downtime"
      trust_signal: "Licensed, prepared, experienced"
  
  badges:
    max_count: 3
    examples:
      - text: "Licensed & Insured"
        icon: "shield-check"
        tooltip: "TACLB00024715E"
      - text: "Same-Day Service"
        icon: "clock-fast"
      - text: "4.8★ Rating"
        icon: "star-fill"
  
  ctas:
    - text: "Call [phone]"
      variant: "primary"
      size: "lg"
      icon: "telephone-fill"
      meclabs_role: "friction_reducer"
    - text: "Schedule Online"
      variant: "outline-primary"
      size: "lg"
      icon: "calendar-check"
      meclabs_role: "convenience_option"
  
  image:
    display: optional (desktop only if text-heavy)
    type: "Technician at work or equipment close-up"
    lazy: false
    
meclabs_contribution:
  increases: [motivation_4x, value_prop_3x]
  reduces: [friction_2x (direct action)]
```

### PRIMARY_CTAS
**Purpose**: Repeat core actions at decision points
**When**: Always
**Placement**: After PROCESS_TIMELINE, before FAQ, pre-FINAL_CTA

**Content Model**:
```yaml
PRIMARY_CTAS:
  instances: multiple (3-4 per page)
  structure:
    heading: string (must vary per instance - see Progressive CTA System)
    buttons:
      - call
      - schedule
      - form
    subtext: optional reinforcement

  progressive_cta_note: |
    Each PRIMARY_CTAS instance MUST use different heading text matching
    its position in the Progressive CTA System (see table above).
    Static "Ready to Get Started?" at every instance is acceptable as
    a fallback, but progressive text is strongly recommended.

    Example progression:
      Instance 1 (after services): "Schedule Your [Specific Service] Visit"
      Instance 2 (after reviews): "No Obligation, Honest Advice"
      Instance 3 (pre-FAQ): "Join [X]+ [City] Families Who Trust Us"
```

### PROCESS_TIMELINE
**Purpose**: Set expectations, reduce uncertainty  
**When**: Always  
**Placement**: Mid-page, before FAQ

**Content Model**:
```yaml
PROCESS_TIMELINE:
  intro_text:
    required: true
    example: "From your first call to fixed and tested, here's exactly what to expect. No surprises, no pressure."
    intent_mapping:
      emotional_driver: "Uncertainty about process, loss of control"
      functional_driver: "Know what to prepare, timeline expectations"
  
  steps:
    min_count: 4
    max_count: 7
    structure:
      - step_number: 1
        title: "Call or Book Online"
        description: "We'll ask about your issue and schedule a visit, often same-day"
        icon: "telephone"
        duration: optional
    examples:
      step_1: "Call/Book" → "Schedule within your availability"
      step_2: "Diagnostic" → "Licensed tech inspects and explains ($89, waived with repair)"
      step_3: "Pricing" → "Exact costs before work begins"
      step_4: "Approval" → "You decide, no obligation"
      step_5: "Repair" → "Fixed right the first time"
      step_6: "Verify" → "Test, clean, confirm working"

meclabs_contribution:
  increases: [value_prop_3x]
  reduces: [friction_2x, anxiety_2x]
```

### FAQ
**Purpose**: Remove objections before contact
**When**: Always
**Placement**: Late-mid, before FINAL_CTA

**Content Model**:
```yaml
FAQ:
  intro_text:
    example: "We know choosing a contractor brings up questions. Here are the most common concerns we hear, answered honestly."

  questions:
    min_count: 5
    max_count: 10
    prioritization: "Match top_objections order"
    structure:
      - question: string (natural language)
        answer: string (150-300 chars, specific)
        intent_category: [price, trust, speed, insurance, warranty, process]

    examples:
      price:
        q: "How much does heater repair cost?"
        a: "Most repairs $200-800. We charge $89 diagnostic (waived with repair) and give exact pricing before starting work. If we can't fix it, you pay nothing."

      trust:
        q: "Should I repair my 12-year-old heater?"
        a: "Depends on repair cost. Under $500? Usually worth it. Over $1,000? Might replace. We'll walk you through the math with no pressure either way."

  html_pattern:
    default: "details_element"

    details_element:
      note: "Default. Simpler, more accessible, works without Bootstrap JS."
      pattern: |
        <details class="faq-item border rounded mb-3 p-3">
          <summary>
            <h3 class="d-inline h6 fw-bold mb-0">Question text here?</h3>
          </summary>
          <div class="faq-body pt-2">
            <p>Answer text here.</p>
          </div>
        </details>
      when_to_use: "WordPress embeds, standalone pages, non-Bootstrap JS contexts"

    bootstrap_accordion:
      note: "Alternative for pages already loading Bootstrap JS."
      when_to_use: "Full Bootstrap pages with other accordion/collapse components"

  structured_data:
    required: true
    type: "FAQPage"
    format: "JSON-LD"
    placement: "After the FAQ section"
    pattern: |
      <script type="application/ld+json">
      {
        "@context": "https://schema.org",
        "@type": "FAQPage",
        "mainEntity": [
          {
            "@type": "Question",
            "name": "Question text here?",
            "acceptedAnswer": {
              "@type": "Answer",
              "text": "Answer text here."
            }
          }
        ]
      }
      </script>
    note: "Generate one Question entry per FAQ item. Strip HTML from answer text in schema."

meclabs_contribution:
  reduces: [friction_2x, anxiety_2x]
```

### FINAL_CTA
**Purpose**: Last conversion opportunity  
**When**: Always  
**Placement**: Last visual band

**Content Model**:
```yaml
FINAL_CTA:
  heading: "Get Your [Service] Fixed Today"
  buttons: [call, schedule]
  subtext: Trust reinforcement
  classes: ["py-5", "bg-primary", "text-white"]
```

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

## Conditional Blocks

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

### SAFETY_NOTICE
**When**: `safety_hazard_possible == true` OR `(niche == 'hvac' AND outage_severity == 'no_heat')`
**Where**: **CRITICAL - Row 2 or 3 MAXIMUM. MUST appear before ANY diagnostic/educational content**
**Priority**: **LIFE SAFETY - Overrides all other positioning preferences**

**⚠️ CRITICAL POSITIONING RULE:**
```
SAFETY_NOTICE must appear BEFORE:
- SYMPTOM_MATRIX
- PATH_CHOICE
- Any "Common Causes" or educational content
- BRANDS_SYSTEMS (if educational)

Violation creates life-threatening risk - user may read educational
content while experiencing gas leak or CO exposure.
```

**Content Model**:
```yaml
SAFETY_NOTICE:
  alert_text:
    max_length: 80
    example: "⚠️ Smell gas or see soot? Turn off system and call immediately"

  explanation_text:
    example: "Carbon monoxide is colorless and odorless. If you notice soot buildup or burning smells, your system may have incomplete combustion: a safety hazard requiring immediate attention."
    intent_mapping:
      emotional_driver: "Fear of invisible danger, family safety"
      functional_driver: "Know when to evacuate vs troubleshoot"

  action_steps:
    max_count: 4
    examples:
      - "Turn off heating system at thermostat"
      - "Open windows if you smell gas"
      - "Check CO detectors are working"
      - "Call us or 911 if you feel lightheaded"

  styling:
    background: "rgba(220, 53, 69, 0.1)" (danger red, not brand red)
    border: "border-start border-5 border-danger"
    note: "Use Bootstrap danger color to distinguish from brand colors - this is life-critical"

meclabs_contribution:
  increases: [motivation_4x]
  reduces: [anxiety_2x (gives control)]
```

### SHORT_FORM
**When**: `intent_primary != 'research'`  
**Where**: HERO right column OR row after HERO

**Content Model**:
```yaml
SHORT_FORM:
  heading: "Get a Free Diagnosis Today"
  subheading: "We'll call you within 15 minutes"
  
  fields:
    minimal:
      - name: text, required
      - phone: tel, required, pattern
    
    standard:
      - name, phone (required)
      - issue: select dropdown
      - preferred_time: select
  
  submit:
    text: "Get Help Now"
    classes: ["btn-danger" if emergency else "btn-primary", "btn-lg", "w-100"]
  
  privacy: adjacent PRIVACY_TCPA

meclabs_contribution:
  reduces: [friction_2x (minimal fields)]
```

### STICKY_CTA
**When**: `device_mobile_pct >= 40`  
**Where**: Fixed bottom on mobile

**Content Model**:
```yaml
STICKY_CTA:
  buttons:
    - "Call Now" (tel: link)
    - "Text Us" (sms: link) (if has_sms)
  classes: ["fixed-bottom", "d-lg-none", "p-3", "bg-white", "shadow"]
```

### BRANDS_SYSTEMS
**When**: `brand_variance_matters == true`  
**Where**: Early-mid, before SYMPTOM_MATRIX

**Content Model**:
```yaml
BRANDS_SYSTEMS:
  title: "We Repair All Major Brands"
  logos:
    format: SVG or PNG grayscale
    count: 6-12
    examples: [Carrier, Trane, Lennox, Rheem, Goodman, American_Standard]
  layout: responsive grid

meclabs_contribution:
  increases: [value_prop_3x (breadth of expertise)]
```

### SYMPTOM_MATRIX
**When**: `niche in ['hvac','plumbing','dental']`  
**Where**: Mid, before PATH_CHOICE and PRICING_TABLE

**Content Model**:
```yaml
SYMPTOM_MATRIX:
  intro_text:
    example: "Is your heater acting up? Here's what those strange noises, weak airflow, or cycling issues usually mean, and what it typically costs to fix. Use this to decide if you need emergency service or can wait until morning."
    intent_mapping:
      emotional_driver: "Uncertainty about severity, DIY capability"
      functional_driver: "Self-diagnosis, urgency assessment, cost estimation"
  
  symptoms:
    type: map
    max_count: 6
    structure:
      symptom_description:
        likely_causes: [cause1, cause2]
        price_range: "$95-350"
        urgency: [wait, schedule_today, emergency]
        explanation: "What this means for you"
    
    examples:
      "Not blowing hot air":
        causes: ["Pilot light out", "Thermostat issue"]
        price: "$95-350"
        urgency: schedule_today
        note: "Usually fixable within an hour. Not dangerous, but home won't warm up."
  
  responsive:
    mobile: accordion
    tablet: card_grid
    desktop: table

meclabs_contribution:
  increases: [value_prop_3x]
  reduces: [friction_2x, anxiety_2x]
```

### PATH_CHOICE
**When**: `niche in ['hvac','roofing','dental','financial']` OR `'price' in top_objections`  
**Where**: After SYMPTOM_MATRIX, before PRICING_TABLE

**Content Model**:
```yaml
PATH_CHOICE:
  title: "Repair vs Replace?"
  
  repair:
    when: ["Under 10 years old", "First major issue", "Single component failure"]
    cost: "$200-1,200 typical"
    pros: ["Lower upfront cost", "Quick fix", "Extends life 2-5 years"]
  
  replace:
    when: ["15+ years old", "Frequent repairs", "Efficiency loss"]
    cost: "$3,500-7,000 typical"
    pros: ["10-15 year warranty", "Lower energy bills", "Modern features"]
  
  decision_support:
    text: "We'll walk you through the math with no pressure either way"

meclabs_contribution:
  increases: [value_prop_3x]
  reduces: [anxiety_2x (education, no pressure)]
```

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

### PRICING_TABLE
**When**: `'price' in top_objections` OR `niche in ['hvac','plumbing','roofing','dental','financial']`  
**Where**: After PATH_CHOICE, before PAYMENT_STRIP

**Content Model**:
```yaml
PRICING_TABLE:
  intro_text:
    required: true
    example: "No surprises. Every repair starts with a $89 diagnostic (waived if we do the work). We show you the problem, explain your options, and only proceed with your approval. If we can't fix it, you pay nothing."
    intent_mapping:
      emotional_driver: "Fear of price gouging, hidden fees"
      functional_driver: "Budget planning, informed decisions"
  
  diagnostic_fee:
    amount: "$89"
    waiver: "waived with repair"
    explanation: "Covers inspection, diagnosis, written estimate"
  
  common_repairs:
    max_count: 6
    structure:
      - service: "Filter & tune-up"
        price_range: "$95-150"
        includes: optional
        typical_time: optional
    prioritization: "Most common first, then by price"
  
  footer_note:
    required: true
    example: "Final pricing determined after diagnostic. Prices shown are typical for {area} and include parts & labor. We'll always get your approval before starting work."

meclabs_contribution:
  increases: [value_prop_3x]
  reduces: [friction_2x, anxiety_2x]
```

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

### REVIEWS_SNAPSHOT
**When**: `review_count >= 20` AND `avg_rating >= 4.5`  
**Where**: Before a CTA, can pair with CREDENTIALS in trust_row

**Content Model**:
```yaml
REVIEWS_SNAPSHOT:
  score: 4.7
  count: 127
  source: "Google Reviews"
  link: "Read all reviews"
  display: star rating + count + source logo

meclabs_contribution:
  reduces: [anxiety_2x (social proof)]
```

### TESTIMONIAL
**When**: `review_count >= 1`  
**Where**: After decision aids, before FAQ

**Content Model**:
```yaml
TESTIMONIAL:
  quote:
    max_length: 180
    must_include: [specific situation, outcome, timeframe]
    example: "Furnace died during the February freeze. They came within 2 hours and had us warm again by dinner. The tech explained everything and didn't upsell us."
  
  attribution:
    author: "First Name L." (privacy)
    location: "McKinney"
    date: "February 2024"
    image: optional (headshot or initials badge)
  
  compliance:
    disclosure_required: true (if regulatory_disclosures_required)
    text: "Individual results may vary."

meclabs_contribution:
  increases: [motivation_4x]
  reduces: [anxiety_2x]
```

### CREDENTIALS_LICENSES
**When**: `regulatory_disclosures_required == true` OR `niche in ['hvac','plumbing','roofing','dental','financial','personal_injury']`  
**Where**: Near REVIEWS_SNAPSHOT, trust_row

**Content Model**:
```yaml
CREDENTIALS_LICENSES:
  licenses: ["TACLB00024715E", "EPA Certified"]
  certifications: ["NATE Certified", "BBB A+ Rating"]
  display: badges or list

meclabs_contribution:
  reduces: [anxiety_2x (legitimacy)]
```

### INSURANCE
**When**: `insurance_involved != false`  
**Where**: Near PRICING_TABLE or FAQ

**Content Model**:
```yaml
INSURANCE:
  title: "Home Warranty & Insurance"
  text: "We work with all major home warranty companies"
  providers: [American_Home_Shield, Choice_Home_Warranty, First_American]
  process: "We'll handle the paperwork and coordination"
```

### COVERAGE_HOURS
**When**: `urgency != 'planning'`  
**Where**: ops_row (pair with SERVICE_AREA)

**Content Model**:
```yaml
COVERAGE_HOURS:
  regular: "7am-8pm Mon-Sat"
  emergency: "24/7 for no-heat emergencies"
  timezone: auto-detect
  current_status: "Open Now" or "Closed • Opens at 7am"
```

### SERVICE_AREA
**When**: `service_area_complexity != 'single_city'`  
**Where**: ops_row (pair with COVERAGE_HOURS)

**Content Model**:
```yaml
SERVICE_AREA:
  map: SVG or optimized PNG
  cities: ["McKinney", "Frisco", "Allen", "Plano"]
  display: map + chip list
```

### AFTER_HOURS
**When**: `has_after_hours == true` OR `urgency == 'emergency'`
**Where**: ops_row OR near HERO, before FAQ

**Content Model**:
```yaml
AFTER_HOURS:
  text: "No heat emergency? We're on-call 24/7 with no extra charge for evening service until 8pm"
  premium_hours: "After 8pm: +$50"
```

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

### SERVICE_AREAS_LIST
**When**: `service_area_complexity != 'single_city'` OR `urgency in ['emergency', 'soon']`
**Where**: After OPERATIONS (ops_row) OR before PRIMARY_CTAS
**Priority**: **MEDIUM - 10% bounce reduction**

**Why separate from SERVICE_AREA (map):**
Emergency buyers need fast text confirmation ("Do they serve me?"), not interactive maps. List with checkmarks answers question in 2 seconds.

**Content Model**:
```yaml
SERVICE_AREAS_LIST:
  heading: "📍 24/7 Emergency Service Throughout [Region]"
  intro: "Fast emergency [service] serving:"

  cities:
    min_count: 6
    max_count: 12
    display: "Grid with check-circle icons"
    icon: "bi-check-circle text-success"

    layout:
      desktop: 3 columns (col-md-4)
      mobile: 2 columns (col-6)

    examples:
      - McKinney
      - Frisco
      - Plano
      - Allen
      - Prosper
      - Celina
      - "+ View all areas" (link)

  sidebar:
    heading: "Not sure if we cover your area?"
    text: "We often serve surrounding communities too. Call us to confirm coverage for your location."
    cta:
      text: "Call Now"
      variant: btn-sm btn-outline-danger

    styling:
      background: "rgba(2, 33, 105, 0.05)"
      border: "1px solid rgba(2, 33, 105, 0.1)"
      layout: col-lg-4

meclabs_contribution:
  reduces: [friction_2x (geographic certainty), anxiety_2x (coverage confirmed)]

performance_data:
  bounce_reduction: "10%"
  time_to_conversion: "Faster (removes ambiguity)"
```

### MID_CTA
**When**: `urgency in ['emergency', 'soon']` OR `stakes == 'high'`
**Where**: Around block 6-7, between content sections
**Purpose**: Slim inline CTA nudge without disrupting reading flow

**Content Model**:
```yaml
MID_CTA:
  layout: "Full-width slim bar (py-3, not py-5)"
  trust_point: "One social proof data point"
  cta: "Single low-friction action"

  examples:
    - trust: "Trusted by 500+ Frisco families"
      cta: "Call (469) 555-1234"
    - trust: "4.9 stars from 200+ Google reviews"
      cta: "Schedule Your Visit"
    - trust: "Serving North Texas since 1987"
      cta: "Get Help Today"

  cta_stage: "3 - Social Proof (see Progressive CTA System)"

  note: |
    This is NOT a full PRIMARY_CTAS section. It is a slim bar similar
    to AVAILABILITY_BADGE in visual weight. One trust point + one CTA.

meclabs_contribution:
  increases: [incentive_2x (act now with social proof)]
  reduces: [friction_2x (always-visible action)]
```

---

### MEET_THE_TEAM
**When**: `niche in ['dental', 'medical', 'pediatric_medical', 'personal_injury', 'financial']` OR `stakes == 'high'`
**Where**: After CREDENTIALS_LICENSES or early-mid for high-stakes planning pages
**Purpose**: Build trust through real people with real credentials

**Content Model**:
```yaml
MEET_THE_TEAM:
  providers:
    min_count: 1
    max_count: 4
    structure:
      - name: "Dr. First Last"
        title: "Board Certified [Specialty]"
        credentials: ["Degree - Institution", "Fellowship", "Board Certification"]
        specialties: ["Specialty 1", "Specialty 2"]
        languages: ["English", "Spanish"] (optional)
        years_experience: number
        image: optional headshot

  layout:
    desktop: "col-lg-6 per provider (2-up)"
    tablet: "col-md-6"
    mobile: "col-12 stacked"

  anti_slop_note: |
    Suppress entirely if no real provider names/credentials available.
    Never use placeholder bios or stock photo headshots.
    Real names + real credentials or skip the block.

meclabs_contribution:
  increases: [value_prop_3x (named expertise, verifiable credentials)]
  reduces: [anxiety_2x (real people, not faceless company)]
```

---

### LOCAL_KNOWLEDGE
**When**: Always recommended. Suppress if no verifiable local data available.
**Where**: Mid-page, after core service content, before FAQ
**Purpose**: Connect local environmental, seasonal, or demographic factors to the service need

**Content Model**:
```yaml
LOCAL_KNOWLEDGE:
  title: "Why [City] [Audience] Need [Service]"

  local_factors:
    min_count: 2
    max_count: 4
    structure:
      - factor: "Cedar fever season (Dec-Feb)"
        connection: "Causes sinus inflammation leading to ear infections in children"
        data_point: "Collin County sees 30% spike in pediatric ENT visits during cedar season"

  layout:
    desktop: "col-lg-6 cards or timeline"
    mobile: "col-12 stacked"

  niche_examples:
    hvac: "North Texas clay soil expansion puts strain on ductwork connections"
    plumbing: "McKinney's 1990s-2000s housing boom means many homes have aging polybutylene pipes"
    dental: "Collin County's cedar season drives ear infection spikes as sinus inflammation blocks Eustachian tubes"
    roofing: "North Texas hail season (March-June) causes 40% of annual roof damage claims"
    cleaning: "High pollen counts in spring require more frequent deep cleaning for allergy sufferers"

  anti_slop_note: |
    This block lives or dies on specificity. Generic climate descriptions = suppress.
    Named allergens, specific seasonal dates, local soil types, named neighborhoods,
    verifiable local stats = include. If you can't populate 2+ specific local facts,
    suppress the block entirely.

meclabs_contribution:
  increases: [value_prop_3x (demonstrates genuine local expertise)]
  reduces: [anxiety_2x (shows they understand YOUR specific area)]
```

---

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

### TRUST_BAR
**When**: Always recommended for high-stakes niches (`stakes == 'high'` OR `niche in ['dental', 'medical', 'pediatric_medical', 'personal_injury']`)
**Where**: Immediately after HERO (row 2)
**Purpose**: Quick-scan trust signals in a slim horizontal bar

**Content Model**:
```yaml
TRUST_BAR:
  stats:
    min_count: 3
    max_count: 5
    structure:
      - number: "5.0"
        label: "Google Reviews"
        icon: "star-fill"
    examples:
      - {number: "4.9", label: "Google Rating", icon: "star-fill"}
      - {number: "15+", label: "Years Experience", icon: "calendar-check"}
      - {number: "Same Day", label: "Appointments", icon: "clock"}

  layout: "Full-width slim bar (py-2 or py-3)"

meclabs_contribution:
  increases: [value_prop_3x (instant credibility)]
  reduces: [anxiety_2x (quick proof)]
```

---

### MAP_CONTACT
**When**: Always recommended
**Where**: Late-page, before or after FAQ
**Purpose**: Business location, hours, phone, and service area zip codes

**Content Model**:
```yaml
MAP_CONTACT:
  address: string
  phone: string
  hours: string
  zip_codes: array (optional)
  map_embed: optional (suppress for emergency pages, use SERVICE_AREAS_LIST instead)

  layout:
    desktop: "col-lg-6 map + col-lg-6 contact info"
    mobile: "stacked (contact info first)"

meclabs_contribution:
  reduces: [friction_2x (easy to find), anxiety_2x (real physical location)]
```

---

### COMPLIANCE_DISCLOSURES
**When**: `regulated == true` AND `niche in ['dental', 'medical', 'pediatric_medical', 'personal_injury', 'financial']`
**Where**: Footer area or adjacent to relevant content
**Purpose**: Regulatory disclosures, disclaimers, license numbers

**Content Model**:
```yaml
COMPLIANCE_DISCLOSURES:
  disclosures:
    medical: "Individual results may vary. Consult your healthcare provider."
    legal: "Past results do not guarantee future outcomes. Every case is different."
    financial: "APR depends on creditworthiness. See terms for details."
    dental_ahpra: "This is a general dental practice. [Practitioner] is a registered general dentist (registration number)."

  note: |
    Only include disclosures relevant to the specific niche and jurisdiction.
    AHPRA disclosures apply ONLY to Australian dental/medical practices.
    HIPAA notices apply ONLY to US medical practices.
    Do NOT apply medical/legal disclaimers to home services or other non-regulated niches.

  placement: "Adjacent to testimonials, pricing, or at page footer"
  classes: ["small", "text-muted"]
```

---

## Row Patterns

### Single-Column Only
These blocks must have full row:
- HERO (though can contain 2 columns internally)
- SYMPTOM_MATRIX
- PATH_CHOICE
- PRICING_TABLE
- SCHEDULER
- FAQ
- FINAL_CTA

### Pairable Patterns

**trust_row** (2-3 columns):
- REVIEWS_SNAPSHOT
- CREDENTIALS_LICENSES
- MEET_THE_TEAM
- AWARD_BADGES
- GUARANTEE_CHIPS

**ops_row** (2 columns):
- COVERAGE_HOURS
- SERVICE_AREA / SERVICE_AREAS_LIST
- AFTER_HOURS

**decision_row** (2-3 columns):
- PROCESS_TIMELINE
- LOCAL_KNOWLEDGE
- INSURANCE

---

## ⚠️ ANTI-PATTERNS - What NOT To Do

### REDUNDANT_CONTENT - The Common Causes Mistake

**Case Study: Emergency Heater Repair Page**

**What happened:**
Added a "Common Causes of Heater Failure" section at Row 3, listing generic causes with price ranges.

**The problem:**
- **Redundancy:** Symptom Matrix (Row 6) provided same information but better organized
- **Safety violation:** Educational content appeared BEFORE Safety Notice
- **Wrong psychology:** User in emergency state doesn't want education, they want reassurance
- **Conversion killer:** Created friction instead of driving action

**The fix:**
- Removed "Common Causes" entirely
- Let Symptom Matrix handle all diagnostic needs
- Moved Safety Notice to Row 3 (proper priority)

**Result:**
- Cleaner page flow
- No information loss (Symptom Matrix was more comprehensive)
- Safety prioritized correctly
- Faster path to conversion

**Rule:**
```
NEVER create redundant content blocks that duplicate information.
If two blocks serve similar purposes, use the BETTER one and delete the other.

Better = More comprehensive + Better UX + Correct position
```

---

### SAFETY_AFTER_EDUCATION - Life-Threatening Pattern

**What NOT to do:**
```
❌ BAD ORDER:
1. Hero
2. Availability
3. Common Causes (educational)
4. Brands We Repair (educational)
5. Safety Notice

Problem: User with gas leak reads "Dirty filters cause..." while in danger
```

**Correct order:**
```
✅ GOOD ORDER:
1. Hero
2. Availability
3. Safety Notice (LIFE SAFETY FIRST)
4. Brands We Repair
5. Reviews/Educational content

Rationale: Life-threatening situations trump all other content
```

**Rule:**
```
IF safety_hazard_possible == true:
  SAFETY_NOTICE must appear in rows 2-3
  SAFETY_NOTICE must appear BEFORE all educational/diagnostic content

Violation = Legal liability + Moral failure
```

---

### SINGLE_TESTIMONIAL_ONLY - Missed Social Proof Opportunity

**What NOT to do:**
```
❌ Using only 1 testimonial buried in Trust section for emergency page

Problem:
- Emergency buyers need VOLUME of proof
- Single testimonial = "cherry-picked?"
- Low credibility impact
```

**Better approach:**
```
✅ REVIEWS_CAROUSEL (4-6 reviews) + Strategic TESTIMONIAL_CALLOUT

Result:
- 20-25% conversion lift from carousel
- Additional 5-7% from strategic callout
- Combined 25%+ total improvement
```

**Rule:**
```
IF urgency in ['emergency', 'soon'] AND review_count >= 20:
  Use REVIEWS_CAROUSEL (4-6 reviews) for volume
  PLUS TESTIMONIAL_CALLOUT for strategic placement

AVOID: Single testimonial only
```

---

### GENERIC_PAYMENT_METHODS - Missed Objection Handling

**What NOT to do:**
```
❌ Payment Strip only: "We accept Visa, MC, Amex, Discover, Check, Cash"

Problem: Doesn't address "I can't afford this" objection
```

**Better approach:**
```
✅ FINANCING_ALERT (separate block) + PAYMENT_STRIP

FINANCING_ALERT addresses objection: "Don't delay critical repairs due to cost"
PAYMENT_STRIP provides convenience: "We accept all payment methods"

Different psychological purposes = Different blocks
```

**Rule:**
```
IF avg_repair_cost >= 300:
  FINANCING_ALERT (objection handling) AFTER PRICING_TABLE
  PAYMENT_STRIP (convenience) after financing

AVOID: Burying financing in payment methods
```

---

### MAP_FOR_EMERGENCY - Wrong Tool for Urgency

**What NOT to do:**
```
❌ Using interactive map widget for service areas on emergency page

Problem:
- User wants instant text answer: "Do they serve me?"
- Maps require interaction, loading, zooming
- Adds friction during high-urgency state
```

**Better approach:**
```
✅ SERVICE_AREAS_LIST with checkmarks

8 cities listed with check icons = 2-second answer
"+ View all areas" link for edge cases
Sidebar: "Not sure? Call us" with CTA

Fast, scannable, no friction
```

**Rule:**
```
IF urgency in ['emergency', 'soon']:
  Use SERVICE_AREAS_LIST (text + icons)
  AVOID: Interactive maps, modals, or widgets

Exception: General service pages can use maps
```

---

### STATS_WITHOUT_PROOF - Hollow Claims

**What NOT to do:**
```
❌ "Trusted by thousands" with no backup

Problem: Vague claims breed skepticism
```

**Better approach:**
```
✅ AWARD_BADGES with specific numbers and visual proof

"38 Years in Business - Since 1987"
"2K+ Satisfied Customers - North Texas Area"
BBB A+ logo
NATE Certified logo

Specific + Visual = Believable
```

**Rule:**
```
AVOID: Generic trust claims ("trusted", "experienced", "reliable")
USE: Specific numbers + Visual badges + Verifiable credentials

"38 years" > "experienced"
"2,000+ customers" > "trusted by thousands"
BBB logo > "highly rated"
```

---

### CONTENT_BEFORE_TRUST - Wrong Psychology

**What NOT to do:**
```
❌ Educational content (Symptom Matrix, Pricing) before establishing ANY trust

Problem:
- User thinking: "Why should I believe you?"
- Need credibility BEFORE asking for belief in your claims
```

**Better approach:**
```
✅ Early trust signals, then content

Row 1: Hero (with trust badges)
Row 2: Availability
Row 3: Safety Notice
Row 4: Brands
Row 5: REVIEWS_CAROUSEL (establish trust)
Row 6: Symptom Matrix (now they believe your diagnosis)
```

**Rule:**
```
Social proof should appear EARLY (rows 4-6)
NOT late (after all content)

Emergency pages need trust FAST
```

---

## Pattern Summary: Emergency vs General Service Pages

### Emergency Pages (urgency = 'emergency' or 'soon')

**Critical Requirements:**
1. Safety warnings in rows 2-3 (life-critical)
2. REVIEWS_CAROUSEL for volume social proof (rows 4-6)
3. SERVICE_AREAS_LIST for fast geographic confirmation
4. FINANCING_ALERT for high-ticket objection handling
5. Multiple CTAs (hero, mid-page, sticky mobile)
6. Availability/hours prominent
7. No redundant educational content

**Flow:**
```
Hero → Availability → Safety → Brands → Reviews → Symptom Matrix →
Repair vs Replace → Testimonial Callout → Pricing → Financing →
Payment → Process → Trust/Awards → Service Areas → FAQ → Final CTA
```

### General Service Pages (urgency = 'planning')

**Different Approach:**
1. Safety notices less urgent (if at all)
2. Single testimonial may suffice (if not emergency)
3. Educational content earlier
4. Fewer CTAs (less pressure)
5. More detailed explanations
6. Service area maps acceptable

**The key difference:**
Emergency buyers are in **decision mode** (who to call NOW)
Planning buyers are in **research mode** (gather info, compare options)

Emergency = Trust + Speed + Reassurance
Planning = Education + Options + Consideration