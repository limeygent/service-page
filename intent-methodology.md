# Intent Methodology

Three-layer intent analysis adapted from the intent-analyzer skill for service page optimization.

## The Three Layers

### Layer 1: Observable Intent
**What users type** - The literal search query
- "heater repair mckinney"
- "emergency plumber near me"
- "how much does roof repair cost"

### Layer 2: Inferred Intent
**Search objective** - The type of information sought
- **Transactional**: Ready to hire/buy ("emergency plumber near me")
- **Commercial**: Comparing options ("best hvac company mckinney")
- **Informational**: Learning/researching ("how much does heater repair cost")
- **Navigational**: Finding specific business ("abc hvac mckinney")

Maps to our `intent_primary`:
- Transactional → `fix_now`
- Commercial → `schedule_soon`
- Informational → `research`

### Layer 3: Hidden Intent
**The WHY** - Underlying emotional and functional drivers

This is what your page MUST address to win the click and conversion.

## Emotional Drivers

### Fear
- Cost escalation: "What if it gets worse?"
- Wrong choice: "What if I hire the wrong contractor?"
- Safety: "Is my family in danger?"
- Time: "What if I can't get it fixed fast enough?"

**Page Response**:
- Transparent pricing (PRICING_TABLE)
- Credentials prominently displayed (CREDENTIALS_LICENSES)
- Safety guidance (SAFETY_NOTICE)
- Availability indicators (AVAILABILITY_BADGE)

### Hope
- Solution: "Can this be fixed quickly?"
- Improvement: "Will this make things better?"
- Relief: "Will this end my stress?"

**Page Response**:
- Outcome-focused headlines
- TESTIMONIAL showing specific results
- PROCESS_TIMELINE showing path to resolution

### Uncertainty
- Confusion: "I don't understand what's wrong"
- Overwhelm: "Too many options to choose from"
- Doubt: "Can I trust this person?"

**Page Response**:
- SYMPTOM_MATRIX for self-diagnosis
- PATH_CHOICE to simplify decisions
- Education-focused content
- Clear PROCESS_TIMELINE

### Urgency
- Time pressure: "It's cold NOW"
- Crisis: "This is getting worse"
- Deadlines: "Before winter hits"

**Page Response**:
- AVAILABILITY_BADGE prominently
- Emergency CTAs (call button primary)
- AFTER_HOURS information
- Fast response promises

## Functional Drivers

### Problem Resolution
- Fix: "Make it work again"
- Prevent: "Stop this from happening again"
- Minimize: "Reduce the damage/cost"

**Page Response**:
- Clear service description
- Warranty information (GUARANTEE_CHIPS)
- Preventive maintenance options

### Decision Support
- Compare: "Who's the best option?"
- Evaluate: "Is this the right choice?"
- Validate: "Am I making a good decision?"

**Page Response**:
- PATH_CHOICE (repair vs replace)
- REVIEWS_SNAPSHOT (social proof)
- FAQ addressing common concerns
- Transparent pros/cons

### Resource Optimization
- Save money: "Most affordable option"
- Save time: "Fastest solution"
- Maximize value: "Best bang for buck"

**Page Response**:
- PRICING_TABLE with value explanation
- PAYMENT_STRIP (financing options)
- Time estimates in PROCESS_TIMELINE
- Efficiency benefits explained

### Capability Building
- Learn: "Understand the issue"
- Expertise: "Know what questions to ask"
- Achieve: "Get this handled right"

**Page Response**:
- Educational SYMPTOM_MATRIX
- Explanation text in every block
- Resources/downloads (if deep intent)
- "What to ask your contractor" content

## Trust Heuristics

### Social Proof
- Reviews: "127 five-star reviews"
- Testimonials: "Specific outcome stories"
- Case studies: "Similar situations resolved"

**Page Blocks**: REVIEWS_SNAPSHOT, TESTIMONIAL

### Authority
- Credentials: "Licensed, certified, experienced"
- Experience: "Serving McKinney since 1987"
- Recognition: "BBB A+ rated"

**Page Blocks**: CREDENTIALS_LICENSES, HERO subhead

### Scarcity
- Limited availability: "3 techs available today"
- Time-sensitive: "Call by 2pm for same-day"
- Seasonal: "Before winter demand peaks"

**Page Blocks**: AVAILABILITY_BADGE (use legitimately only)

### Risk Mitigation
- Guarantees: "No repair = No charge"
- Insurance: "Fully insured"
- Warranties: "90-day warranty on all work"

**Page Blocks**: GUARANTEE_CHIPS, INSURANCE, CREDENTIALS

## Niche-Specific Emotional Patterns

### HVAC/Plumbing (Emergency)
**Primary Emotions**: Fear (damage, safety), Urgency (discomfort)
**Primary Functions**: Problem resolution (fast), Resource optimization (minimize damage)
**Key Heuristics**: Authority (licensed), Scarcity (availability)

**Page Emphasis**:
- SAFETY_NOTICE if hazard possible
- AVAILABILITY_BADGE prominent
- Speed promises in HERO
- Emergency CTA primary

### Dental
**Primary Emotions**: Fear (pain), Uncertainty (procedure unknowns)
**Primary Functions**: Decision support (is this necessary?), Problem resolution (pain relief)
**Key Heuristics**: Authority (credentials), Risk mitigation (insurance, payment plans)

**Page Emphasis**:
- Comfort/anxiety reduction messaging
- INSURANCE block prominent
- Gentle, empathetic copy
- TESTIMONIAL about pain-free experience

### Personal Injury
**Primary Emotions**: Hope (compensation), Uncertainty (process complexity), Fear (financial)
**Primary Functions**: Decision support (should I hire?), Capability building (understand rights)
**Key Heuristics**: Authority (case wins), Social proof (testimonials), Risk mitigation (no fee unless win)

**Page Emphasis**:
- Contingency fee transparency
- PROCESS_TIMELINE for legal process
- CREDENTIALS (bar admissions, case results)
- Empowerment messaging

### Financial Services
**Primary Emotions**: Uncertainty (right choice?), Fear (wrong decision consequences)
**Primary Functions**: Decision support (compare options), Resource optimization (best rate)
**Key Heuristics**: Authority (credentials, experience), Risk mitigation (transparency)

**Page Emphasis**:
- Conservative, professional tone
- APR transparency (PRICING_TABLE variant)
- Regulatory compliance visible
- Educational approach

## Intent-to-Block Mapping

```yaml
if emotional_driver == "fear_of_cost":
  emphasize: [PRICING_TABLE, GUARANTEE_CHIPS, PAYMENT_STRIP]
  copy_focus: "Transparency, no surprises, risk reversals"

if emotional_driver == "fear_of_safety":
  emphasize: [SAFETY_NOTICE, CREDENTIALS_LICENSES, PROCESS_TIMELINE]
  copy_focus: "Expertise, caution, proper procedures"

if emotional_driver == "uncertainty_about_problem":
  emphasize: [SYMPTOM_MATRIX, FAQ, PATH_CHOICE]
  copy_focus: "Education, empowerment, decision support"

if emotional_driver == "urgency_time_pressure":
  emphasize: [AVAILABILITY_BADGE, AFTER_HOURS, STICKY_CTA]
  copy_focus: "Speed, availability, immediate response"

if functional_driver == "problem_resolution_fast":
  emphasize: [PROCESS_TIMELINE, AVAILABILITY_BADGE]
  copy_focus: "Efficiency, same-day service, prepared technicians"

if functional_driver == "decision_support_compare":
  emphasize: [REVIEWS_SNAPSHOT, PATH_CHOICE, FAQ]
  copy_focus: "Transparency, education, no pressure"

if functional_driver == "resource_optimization_cost":
  emphasize: [PRICING_TABLE, PAYMENT_STRIP, GUARANTEE_CHIPS]
  copy_focus: "Value, financing, money-back guarantees"
```

## Copy Voice by Intent

### Transactional (fix_now)
**Voice**: Direct, confident, action-oriented
**Tone**: Reassuring but urgent
**Structure**: Short sentences, clear CTAs
**Example**: "Heater down? We're on it. Call now for same-day emergency repair in McKinney."

### Commercial (schedule_soon)
**Voice**: Professional, helpful, slightly warmer
**Tone**: Balanced urgency with service
**Structure**: Medium-length, benefit-focused
**Example**: "Need your heater fixed this week? Our certified technicians are ready. Schedule your appointment today."

### Informational (research)
**Voice**: Educational, patient, comprehensive
**Tone**: Helpful expert, no pressure
**Structure**: Longer explanations, thorough
**Example**: "Wondering if your heater needs repair or replacement? Here's how to decide. We'll walk you through the costs, benefits, and typical timelines for each option."

## Explanation Text Formula

Every block's explanation text should map to intent:

```
[Acknowledge emotional driver] + [Address functional driver] + [Apply trust heuristic]

HERO example (emergency HVAC):
"When your heater fails during winter [fear: discomfort, safety],
our licensed technicians carry parts for same-visit repairs [function: fast resolution],
meaning you're back to warmth within hours [outcome + authority signal]."

PRICING_TABLE example (cost anxiety):
"We know unexpected repairs create stress [fear: cost escalation].
Every repair includes upfront pricing and your approval before we start [function: control + decision support].
If we can't fix it, you pay nothing [risk mitigation]."

SYMPTOM_MATRIX example (uncertainty):
"Not sure what's wrong or how urgent it is? [uncertainty: diagnosis]
Use this guide to understand common issues and costs [function: capability building].
This helps you decide whether you need emergency service or can wait [empowerment: decision support]."
```

## Warning: What NOT to Do

### Don't Manufacture Emotional Drivers
Bad: Generic fear-mongering ("Your family could be in danger!")
Good: Legitimate safety guidance when hazard exists

### Don't Oversell When Intent is Research
Bad: Aggressive CTAs and urgency on educational queries
Good: Valuable content with soft invitation to contact

### Don't Ignore Functional Drivers
Bad: All emotion, no practical information
Good: Balance emotional validation with functional solutions

### Don't Mismatch Heuristics to Niche
Bad: Scarcity tactics for financial services
Good: Authority and transparency for financial services

## Intent Analysis Checklist

For every page, answer:
1. **What emotional driver** is primary? (fear, hope, uncertainty, urgency)
2. **What functional driver** matters most? (resolution, decision support, optimization, capability)
3. **What trust heuristic** will reduce anxiety? (social proof, authority, scarcity, risk mitigation)
4. **Does the HERO** address these explicitly?
5. **Are the right blocks** emphasized/de-emphasized?
6. **Does the copy voice** match the intent type?
7. **Is explanation text** following the formula?

If you can't answer these clearly, the page won't convert well.