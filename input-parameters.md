# Input Parameters Schema

Complete parameter set for service page generation. Required inputs marked with *.

## Business Profile

```yaml
business_profile:
  name: string *                           # "ABC HVAC Services"
  founded_year: number                     # 1987
  location:
    city: string *                         # "McKinney"
    state: string *                        # "TX"
    region: string                         # "Dallas-Fort Worth"
  license_numbers: array                   # ["TACLB00024715E"]
  phone: string                            # "972-XXX-XXXX"
  service_radius_miles: number             # 30
```

## Service Context

```yaml
niche: enum *
  options: [hvac, plumbing, roofing, electrical, dental, medical, pediatric_medical, personal_injury, financial, cleaning, lawn_care, pest_control, other]

intent_primary: enum *
  options: [fix_now, schedule_soon, research]
  
urgency: enum *
  options: [emergency, soon, planning]
  derivation: "Infer from query + season + time_of_day"

audience_role: enum
  options: [homeowner, renter, business_owner, patient, claimant, investor]
  default: homeowner

season: enum
  options: [winter, spring, summer, fall]
  
climate_zone: enum
  options: [cold, temperate, hot_humid, hot_dry]

# HVAC/Plumbing specific
outage_severity: enum
  options: [no_heat, not_keeping_up, intermittent, noisy, other]
  when: "niche in ['hvac', 'plumbing']"

risk_level: enum
  options: [low, medium, high]
  definition: "Safety/legal/medical risk if delayed"

safety_hazard_possible: boolean
  examples: "gas/CO leak, infection risk, structural danger"
```

## User Demographics

```yaml
demographics:
  prefers_call: boolean
    default: true
    
  language_primary: string
    default: "en"
    options: [en, es]
    
  reading_level: enum
    options: [basic, standard, advanced]
    default: standard
    
  device_mobile_pct: number
    range: 0-100
    default: 60
```

## Business Capabilities

```yaml
capabilities:
  has_scheduler: boolean
    default: false
    
  has_after_hours: boolean
    default: false
    
  has_chat: boolean
    default: false
    
  has_financing: boolean
    default: false
    
  offering_tiers: boolean
    description: "Good/Better/Best packages"
    default: false
    
  pricing_unknown: boolean
    description: "Exact prices cannot be shown (varies by job)"
    default: true
    
  brand_variance_matters: boolean
    description: "Different brands/systems require different expertise"
    default: false
```

## Trust Signals

```yaml
trust_signals:
  review_count: number
    default: 0
    
  avg_rating: number
    range: 0.0-5.0
    default: 0.0
    
  years_in_business: number
    derivation: "current_year - founded_year"
    
  insurance_involved: enum
    options: [true, false, optional]
    default: false
```

## Objections Priority

```yaml
top_objections: array
  description: "Ordered by importance"
  options:
    - price
    - speed
    - trust
    - insurance
    - paperwork
    - warranty
  default: ["price", "trust", "speed"]
  max_count: 4
```

## Complexity Factors

```yaml
complexity:
  service_area_complexity: enum
    options: [single_city, multi_city, regional]
    default: single_city
    
  regulatory_disclosures_required: boolean
    when: "niche in ['dental', 'medical', 'pediatric_medical', 'personal_injury', 'financial']"
    default: false
    
  page_length: enum
    options: [short, standard, deep]
    default: standard
    derivation: "Based on intent_primary (research = deep, fix_now = short)"
```

## Page-Level Modifiers

Binary modifiers that refine block selection and content beyond niche + urgency. Auto-detected from niche but can be overridden.

```yaml
modifiers:
  stakes:
    type: enum
    options: [low, medium, high]
    default: medium
    auto_detection:
      high: "niche in [cosmetic_dentist, dental_implants, personal_injury, financial, surgeon, major_remodel]"
      low: "niche in [cleaning, lawn_care, car_detailing, junk_removal]"
      medium: "everything else"
    effects:
      high: "Deeper CREDENTIALS_LICENSES, MEET_THE_TEAM, PROCESS_TIMELINE; add sticky TOC"
      low: "Brief trust signals, skip MEET_THE_TEAM"

  regulated:
    type: boolean
    default: false
    auto_detection: "niche in [hvac, plumbing, electrical, roofing, dental, personal_injury, financial, medical, pediatric_medical]"
    effects: "CREDENTIALS_LICENSES mandatory; compliance disclosures rendered"

  high_ticket:
    type: boolean
    default: false
    auto_detection: "niche in [roofing, kitchen_remodel, cosmetic_dentist, dental_implants, solar, personal_injury]"
    effects: "PRICING_TABLE shows ranges + financing; FINANCING_ALERT rendered"

  recurring:
    type: boolean
    default: false
    auto_detection: "niche in [cleaning, lawn_care, pest_control, pool_service, general_dentist]"
    effects: "Plan/subscription pricing emphasis; consistency messaging in copy"
```

## Dynamic Data (Optional)

```yaml
dynamic_data:
  technicians_available_now: number
    description: "Live from dispatch system"
    
  next_available_slot: datetime
    description: "From scheduling system"
    
  current_wait_time_hours: number
    description: "Average response time right now"
```

## Minimal Viable Input Set

For quick page generation, collect only:

```yaml
minimal_inputs:
  - niche *
  - intent_primary *
  - urgency *
  - location.city *
  - location.state *
  - business_profile.name *
```

All other parameters use defaults or intelligent inference.

## Input Collection Strategy

### Progressive Disclosure
1. Start with minimal inputs (6 required fields)
2. Infer defaults based on niche
3. Ask clarifying questions only when they materially change output
4. Offer to "dig deeper" for more customized page

### Example Conversation Flow

```
Claude: "I'll help you build a service page. I need a few details:
1. What type of business? (HVAC, plumbing, roofing, dental, legal, etc)
2. What's the main user intent? (Emergency repair, schedule service, research options)
3. Business name?
4. City and state?

From there I can generate a page and we can refine it."

User: "HVAC, emergency heater repair, ABC Heating, McKinney TX"

Claude: [Generates page with inferred defaults]

Claude: "I've created an emergency heater repair page. Would you like to customize:
- Review count/rating (I assumed you don't have many yet)
- Pricing transparency (I showed ranges, can make more specific)
- Available hours (I assumed standard hours, do you have 24/7?)
- Or just review the page as-is?"
```

## Defaults by Niche

```yaml
hvac:
  urgency: emergency (if winter) or soon
  top_objections: [price, speed, trust]
  brand_variance_matters: true
  safety_hazard_possible: true (if no_heat)
  has_after_hours: true (assumed for emergencies)

plumbing:
  urgency: emergency (if leak/burst) or soon
  top_objections: [speed, price, trust]
  safety_hazard_possible: true (if gas/sewer)
  has_after_hours: true

dental:
  urgency: soon (rarely emergency)
  top_objections: [trust, insurance, price]
  insurance_involved: true
  regulatory_disclosures_required: true

personal_injury:
  urgency: planning
  top_objections: [trust, price, paperwork]
  insurance_involved: optional
  regulatory_disclosures_required: true

financial:
  urgency: planning
  top_objections: [trust, price]
  regulatory_disclosures_required: true
  offering_tiers: true

pediatric_medical:
  urgency: soon (rarely emergency)
  top_objections: [trust, speed, insurance]
  insurance_involved: true
  regulatory_disclosures_required: true
  stakes: high
  regulated: true
  audience_role: parent
  copy_voice: warm, reassuring, parent-empathetic
```