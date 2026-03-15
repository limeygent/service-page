# Block Catalog

Complete catalog of page blocks with conditional logic and ordering rules. For detailed content models, read the relevant file from `references/blocks/`.

## Progressive CTA System

CTAs must evolve as the reader scrolls and accumulates trust. Never use the same CTA text twice on a page.

| Stage | Position | Reader State | CTA Strategy | Example |
|-------|----------|-------------|--------------|---------|
| 1. Intent-Matching | HERO | Just arrived, zero trust | Match dominant intent | Emergency: "Call Now". Planning: "Schedule Free Consultation" |
| 2. Service-Specific | After SYMPTOM_MATRIX or condition content | Knows your scope | Narrow to their likely need | "Schedule Your [Specific Service] Visit" |
| 3. Social Proof | MID_CTA bar (block 6-7) | Has differentiation + some trust | Trust-leveraging nudge | "Join 500+ [City] families who trust us" |
| 4. Objection-Handling | After REVIEWS | Seen peer validation | Address remaining barrier | "No obligation, no pressure" |
| 5. Closing Argument | FINAL_CTA | Consumed everything | Reference specific value prop from page | "Ready for same-day relief in [City]?" |

See `references/content-templates.md` -> "Progressive CTA Copy Patterns" for full copy examples per stage.

---

## Block Selection Index

| Block | When | Purpose | File |
|-------|------|---------|------|
| HERO | Always | Declare service/location + surface primary CTAs | `references/blocks/hero.md` |
| PRIMARY_CTAS | Always | Repeat core actions at decision points | `references/blocks/primary-ctas.md` |
| PROCESS_TIMELINE | Always | Set expectations, reduce uncertainty | `references/blocks/process-timeline.md` |
| FAQ | Always | Remove objections before contact | `references/blocks/faq.md` |
| FINAL_CTA | Always | Last conversion opportunity | `references/blocks/final-cta.md` |
| PRIVACY_TCPA | Any form or click-to-text present | Legal consent for forms/SMS | `references/blocks/privacy-tcpa.md` |
| AVAILABILITY_BADGE | `urgency in ['emergency','soon']` OR `'speed' in top_objections` | Confirm technician availability | `references/blocks/availability-badge.md` |
| SAFETY_NOTICE | `safety_hazard_possible == true` OR HVAC no-heat | Life safety warning (MUST be rows 2-3) | `references/blocks/safety-notice.md` |
| SHORT_FORM | `intent_primary != 'research'` | Lead capture form | `references/blocks/short-form.md` |
| STICKY_CTA | `device_mobile_pct >= 40` | Fixed bottom mobile CTA | `references/blocks/sticky-cta.md` |
| BRANDS_SYSTEMS | `brand_variance_matters == true` | Show brand expertise breadth | `references/blocks/brands-systems.md` |
| SYMPTOM_MATRIX | `niche in ['hvac','plumbing','dental']` | Self-diagnosis + cost estimation | `references/blocks/symptom-matrix.md` |
| PATH_CHOICE | `niche in ['hvac','roofing','dental','financial']` OR price objection | Repair vs Replace decision aid | `references/blocks/path-choice.md` |
| GUARANTEE_CHIPS | `'price' in top_objections` OR `'trust' in top_objections` | Risk reversal badges | `references/blocks/guarantee-chips.md` |
| PRICING_TABLE | `'price' in top_objections` OR applicable niches | Transparent pricing display | `references/blocks/pricing-table.md` |
| PAYMENT_STRIP | `has_financing == true` OR price objection | Payment method logos | `references/blocks/payment-strip.md` |
| FINANCING_ALERT | `avg_repair_cost >= 300` OR price objection OR `has_financing` | Objection-handling for cost barrier (12-15% lift) | `references/blocks/financing-alert.md` |
| SCHEDULER | `has_scheduler == true` AND `intent_primary != 'research'` | Online booking embed | `references/blocks/scheduler.md` |
| REVIEWS_SNAPSHOT | `review_count >= 20` AND `avg_rating >= 4.5` | Aggregate rating display | `references/blocks/reviews-snapshot.md` |
| REVIEWS_CAROUSEL | `review_count >= 20` AND `avg_rating >= 4.5` AND emergency/soon | Volume social proof (20-25% lift) | `references/blocks/reviews-carousel.md` |
| TESTIMONIAL | `review_count >= 1` | Single strategic quote | `references/blocks/testimonial.md` |
| TESTIMONIAL_CALLOUT | `review_count >= 3` AND `has_pricing_transparency` | Pre-pricing honesty quote (5-7% lift) | `references/blocks/testimonial-callout.md` |
| CREDENTIALS_LICENSES | Regulated niches or required disclosures | License/certification badges | `references/blocks/credentials-licenses.md` |
| AWARD_BADGES | `review_count >= 50` OR `years_in_business >= 10` OR BBB | Authority signal badges (8-10% lift) | `references/blocks/award-badges.md` |
| MEET_THE_TEAM | High-stakes niches (dental, medical, legal, financial) | Provider bios with credentials | `references/blocks/meet-the-team.md` |
| LOCAL_KNOWLEDGE | Always recommended (suppress if no verifiable data) | Local factors connected to service need | `references/blocks/local-knowledge.md` |
| INSURANCE | `insurance_involved != false` | Warranty/insurance provider info | `references/blocks/insurance.md` |
| COVERAGE_HOURS | `urgency != 'planning'` | Business hours + emergency availability | `references/blocks/coverage-hours.md` |
| SERVICE_AREA | `service_area_complexity != 'single_city'` | Map + city chip list | `references/blocks/service-area.md` |
| SERVICE_AREAS_LIST | Multi-city OR emergency/soon urgency | Text list for fast geo confirmation (10% bounce reduction) | `references/blocks/service-areas-list.md` |
| AFTER_HOURS | `has_after_hours == true` OR emergency | After-hours availability info | `references/blocks/after-hours.md` |
| MID_CTA | `urgency in ['emergency','soon']` OR `stakes == 'high'` | Slim inline CTA nudge | `references/blocks/mid-cta.md` |
| TRUST_BAR | High-stakes niches | Quick-scan trust signals after HERO | `references/blocks/trust-bar.md` |
| MAP_CONTACT | Always recommended | Business location, hours, phone | `references/blocks/map-contact.md` |
| COMPLIANCE_DISCLOSURES | Regulated niches (dental, medical, legal, financial) | Regulatory disclaimers | `references/blocks/compliance-disclosures.md` |

---

## Priority-Based Sequencing

### Priority Levels

1. **LIFE SAFETY** (overrides everything): SAFETY_NOTICE must be rows 2-3, BEFORE any educational content
2. **Required blocks**: HERO, PRIMARY_CTAS, PROCESS_TIMELINE, FAQ, FINAL_CTA, PRIVACY_TCPA
3. **High priority conditional**: AVAILABILITY_BADGE, SHORT_FORM, REVIEWS_CAROUSEL, FINANCING_ALERT, STICKY_CTA
4. **Medium priority conditional**: BRANDS_SYSTEMS, SYMPTOM_MATRIX, PATH_CHOICE, PRICING_TABLE, TESTIMONIAL_CALLOUT, AWARD_BADGES, SERVICE_AREAS_LIST, MID_CTA
5. **Standard conditional**: GUARANTEE_CHIPS, PAYMENT_STRIP, SCHEDULER, REVIEWS_SNAPSHOT, TESTIMONIAL, CREDENTIALS_LICENSES, MEET_THE_TEAM, LOCAL_KNOWLEDGE, INSURANCE, COVERAGE_HOURS, SERVICE_AREA, AFTER_HOURS, TRUST_BAR, MAP_CONTACT, COMPLIANCE_DISCLOSURES

### Emergency Page Flow

```
Hero -> Availability -> Safety -> Brands -> Reviews Carousel ->
Symptom Matrix -> Repair vs Replace -> Testimonial Callout ->
Pricing -> Financing -> Payment -> Process -> Trust/Awards ->
Service Areas -> FAQ -> Final CTA
```

### General/Planning Page Flow

```
Hero -> Trust Bar -> Brands -> Meet the Team -> Local Knowledge ->
Symptom Matrix -> Path Choice -> Pricing -> Process ->
Testimonial -> Credentials -> FAQ -> Map/Contact -> Final CTA
```

### Decision Tree

```
IF safety_hazard_possible:
  SAFETY_NOTICE at rows 2-3 (BEFORE all educational content)

IF urgency in ['emergency', 'soon']:
  Prioritize: AVAILABILITY_BADGE, REVIEWS_CAROUSEL, SERVICE_AREAS_LIST
  Use: STICKY_CTA, MID_CTA, FINANCING_ALERT
  Avoid: Interactive maps, excessive education

IF urgency == 'planning':
  Prioritize: Education (SYMPTOM_MATRIX, PATH_CHOICE), MEET_THE_TEAM
  Use: SERVICE_AREA (map OK), LOCAL_KNOWLEDGE
  Fewer CTAs, less pressure
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

## Anti-Patterns

### REDUNDANT_CONTENT
Never create blocks that duplicate information already covered by another block. If two blocks serve similar purposes, use the better one (more comprehensive + better UX + correct position) and delete the other.

### SAFETY_AFTER_EDUCATION
SAFETY_NOTICE must appear BEFORE all educational/diagnostic content. Violation creates life-threatening risk.

### SINGLE_TESTIMONIAL_ONLY
For emergency pages with `review_count >= 20`: use REVIEWS_CAROUSEL (4-6 reviews) for volume PLUS TESTIMONIAL_CALLOUT for strategic placement. Single testimonial only = missed opportunity.

### GENERIC_PAYMENT_METHODS
If `avg_repair_cost >= 300`: use separate FINANCING_ALERT (objection handling) AFTER PRICING_TABLE, then PAYMENT_STRIP (convenience). Do not bury financing in payment methods.

### MAP_FOR_EMERGENCY
If `urgency in ['emergency', 'soon']`: use SERVICE_AREAS_LIST (text + icons) instead of interactive maps. Maps add friction during high-urgency state.

### STATS_WITHOUT_PROOF
Avoid generic trust claims ("trusted", "experienced"). Use specific numbers + visual badges + verifiable credentials via AWARD_BADGES.

### CONTENT_BEFORE_TRUST
Social proof should appear early (rows 4-6) for emergency pages. Establish credibility BEFORE asking users to believe your claims.

---

## Pattern Summary: Emergency vs General

**Emergency** (urgency = 'emergency' or 'soon'): Trust + Speed + Reassurance
- Safety warnings rows 2-3
- REVIEWS_CAROUSEL for volume social proof
- SERVICE_AREAS_LIST for fast geo confirmation
- FINANCING_ALERT for high-ticket objection handling
- Multiple CTAs (hero, mid-page, sticky mobile)

**General/Planning** (urgency = 'planning'): Education + Options + Consideration
- Educational content earlier
- Single testimonial may suffice
- Service area maps acceptable
- Fewer CTAs, less pressure
- More detailed explanations
