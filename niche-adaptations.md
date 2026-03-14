# Niche-Specific Adaptations

Industry-specific requirements, patterns, and constraints.

## Home Services (HVAC, Plumbing, Electrical, Roofing)

### Common Characteristics
- Emergency scenarios common
- Safety concerns present
- Licensing critical
- Same-day service valued
- Price anxiety high
- Brand/equipment variance matters

### Mandatory Blocks
- CREDENTIALS_LICENSES (license numbers visible)
- COVERAGE_HOURS (especially if emergency)
- PRICING_TABLE (transparency reduces anxiety)

### Recommended Blocks
- SAFETY_NOTICE (if emergency or hazard)
- SYMPTOM_MATRIX (empower self-diagnosis)
- PATH_CHOICE (repair vs replace)
- AVAILABILITY_BADGE (if same-day)
- AFTER_HOURS (if 24/7)

### HVAC-Specific
```yaml
seasonal_urgency:
  winter: "No heat emergency" (high urgency)
  summer: "AC out" (high urgency)
  spring_fall: "Maintenance, tune-ups" (planning)

common_symptoms:
  - Not heating/cooling
  - Strange noises
  - Cycling on/off
  - Weak airflow
  - High energy bills

brands_matter: true
  common: [Carrier, Trane, Lennox, Rheem, Goodman, American Standard, Bryant, York]

typical_pricing:
  diagnostic: "$75-125 (waived with repair)"
  minor_repair: "$150-500"
  major_repair: "$500-1,500"
  replacement: "$3,500-12,000"

copy_patterns:
  headline: "[Service] in [City] - Same-Day Emergency Response"
  subhead: "Licensed HVAC technicians serving [region] since [year]"
  urgency: "No heat? We're available 24/7 with fast response times"
```

### Plumbing-Specific
```yaml
emergency_types:
  - Burst pipe
  - Gas leak
  - Sewer backup
  - Water heater failure
  - Major leak

safety_critical:
  - Gas leaks (evacuate + call)
  - Sewer gas (health hazard)
  - Water damage (mold risk)

typical_pricing:
  service_call: "$85-150"
  minor_repair: "$150-400"
  major_repair: "$500-2,000"
  replacement: "$1,000-8,000"

brands_matter: partial
  water_heaters: [Rheem, Bradford White, AO Smith, Navien]
  
copy_patterns:
  headline: "Emergency Plumber [City] - Stop Water Damage Fast"
  urgency: "Burst pipe? Leak? We're on call 24/7"
```

### Roofing-Specific
```yaml
urgency_triggers:
  - Active leak
  - Storm damage
  - Missing shingles
  - Inspection before selling

seasonal: high (storm season, winter prep)

visual_proof_critical: true
  emphasize: [BEFORE_AFTER_GALLERY, TESTIMONIAL with photos]

typical_pricing:
  inspection: "$100-300 (often free)"
  repair: "$300-1,500"
  replacement: "$5,000-25,000"

insurance_common: true
  emphasize: INSURANCE block

copy_patterns:
  headline: "Roof Repair [City] - Licensed & Insured Since [year]"
  subhead: "We work directly with insurance adjusters"
```

## Medical/Dental

### Common Characteristics
- Anxiety about pain/discomfort
- Insurance complexity
- Cost concerns
- Credentials critical
- Comfort/bedside manner valued

### Mandatory Blocks
- CREDENTIALS_LICENSES (prominently)
- INSURANCE (accepted plans, filing assistance)
- FAQ (addressing pain, cost, time)
- COMPLIANCE_DISCLOSURES (if required)

### Recommended Blocks
- TESTIMONIAL (comfort/outcome focused)
- PAYMENT_STRIP (financing, payment plans)
- PROCESS_TIMELINE (what to expect)

### Dental-Specific
```yaml
common_concerns:
  - Pain during procedure
  - Cost (often not emergency)
  - Insurance coverage
  - Time commitment
  - Anxiety about dentist

services_separate_pages:
  emergency: "Toothache, broken tooth" (urgent)
  cosmetic: "Whitening, veneers" (planning, high consideration)
  routine: "Cleaning, checkup" (low urgency)
  major: "Implants, root canal" (high anxiety, high cost)

copy_voice:
  tone: Gentle, reassuring, empathetic
  avoid: Clinical jargon, aggressive urgency
  emphasize: Comfort, pain management, gentle care

typical_content:
  hero_subhead: "Gentle dental care for [city] families since [year]"
  testimonial_focus: "No pain, explained everything, felt comfortable"
  faq: "Does it hurt?", "Do you take my insurance?", "How long will it take?"

ahpra_compliance:
  trigger_condition: "ONLY apply when BOTH conditions are true: (1) niche is dental or medical AND (2) business is located in Australia. If either condition is false, skip this entire section."
  restricted_words: ["pain-free", "painless", "gentle" (as minimiser), "specialist" (unless registered), "expert", "expertise", "perfect", "guarantee"]
  restricted_titles: ["Cosmetic Dentist", "Orthodontist" (reserved for registered specialists)]
  safe_alternatives:
    - "less bleeding and a smoother recovery" (instead of "painless")
    - "no tooth preparation required" (instead of "reversible")
    - "General Dentist with a focus on cosmetic procedures" (instead of "Cosmetic Dentist")
  disclaimer_wording: |
    Avoid using restricted words even in disclaimers or negation (e.g., do NOT write "She is not a registered specialist").
    Instead, state the positive: "Dr. [Name] is a registered general dentist (AHPRA [number])."
    The word "specialist" should not appear anywhere on the page unless the practitioner holds specialist registration.
```

## Legal Services

### Common Characteristics
- High consideration (slow decision)
- Trust critical
- Contingency fee common
- Regulatory restrictions
- Process complexity

### Mandatory Blocks
- COMPLIANCE_DISCLOSURES (heavily regulated)
- PROCESS_TIMELINE (legal process is mystery)
- FAQ (address concerns proactively)
- TESTIMONIAL_DISCLOSURE (adjacent to testimonial)

### Recommended Blocks
- CREDENTIALS (bar admissions, case results)
- PRICING_TABLE (fee structure transparent)
- TESTIMONIAL (outcome-focused but disclaimed)

### Personal Injury-Specific
```yaml
common_case_types:
  - Car accident
  - Slip and fall
  - Medical malpractice
  - Workplace injury
  - Wrongful death

fee_structure:
  contingency: "No fee unless we win" (33-40%)
  costs: "Case costs advanced by firm"
  transparency: Critical for trust

copy_restrictions:
  cannot_say:
    - "Guaranteed results"
    - "We'll win your case"
    - Specific settlement amounts without disclosure
  
  must_say:
    - "Past results don't guarantee future outcomes"
    - "Every case is different"
    - Fee structure clearly

compliance_heavy:
  every_testimonial: Requires disclosure
  every_case_result: Requires disclaimer
  pricing_discussion: Must clarify contingency
  consultation: "Free" must be genuinely free

blocks_different:
  BRANDS_SYSTEMS → CASE_TYPES_WE_HANDLE
  PRICING_TABLE → FEE_STRUCTURE_EXPLANATION
  SYMPTOM_MATRIX → CASE_EVALUATION_QUIZ

copy_voice:
  tone: Assertive but supportive, empowering
  avoid: Ambulance chaser vibe, pressure tactics
  emphasize: Your rights, our expertise, no pressure

typical_content:
  hero: "Personal Injury Lawyer [City] - No Fees Unless We Win"
  subhead: "Fighting for accident victims since [year]"
  cta: "Free case evaluation" (not "free consultation" if requires commitment)
```

## Financial Services

### Common Characteristics
- Heavily regulated
- High consideration
- Trust paramount
- Numbers-driven
- Conservative expectations

### Mandatory Blocks
- COMPLIANCE_DISCLOSURES (every page, multiple placements)
- CREDENTIALS (licenses, registrations)
- PRICING_TABLE (APR, fees transparent)
- FAQ (address concerns thoroughly)

### Cannot Include
- Guaranteed returns
- Testimonials (in many states without heavy disclaimers)
- False urgency
- Misleading comparisons

### Mortgage/Lending-Specific
```yaml
required_disclosures:
  - NMLS number (if applicable)
  - Equal Housing Lender
  - APR explanation
  - Rate lock terms
  - Fee schedule

copy_restrictions:
  must_show:
    - APR (not just rate)
    - All fees itemized
    - "Your rate depends on creditworthiness"
    - Terms clearly stated
  
  cannot_show:
    - "Lowest rates guaranteed"
    - "Best deal in town"
    - Teaser rates without full disclosure

blocks_adapt:
  PRICING_TABLE → APR_COMPARISON_TABLE
  GUARANTEE_CHIPS → COMPLIANCE_BADGES
  TESTIMONIAL → CASE_STUDY (with disclosures)

copy_voice:
  tone: Professional, conservative, educational
  avoid: Hype, pressure, emotion
  emphasize: Transparency, education, long-term thinking

typical_content:
  hero: "Mortgage Lender [City] - Transparent Rates Since [year]"
  subhead: "NMLS #XXXXX | Equal Housing Lender"
  cta: "Get rate quote" (not "Apply now" if pre-qualification)
```

## Pediatric/Family Medical

### Common Characteristics
- Parent is decision-maker, child is patient
- High trust threshold (child's safety)
- Insurance complexity
- Provider credentials critical (board certifications, training institutions)
- Seasonal condition patterns (ear infections, allergies, flu)
- Walk-in/same-day availability highly valued
- Multilingual staff is a differentiator

### Mandatory Blocks
- MEET_THE_TEAM (providers with board certifications, languages, training)
- CREDENTIALS_LICENSES (prominently displayed)
- INSURANCE (accepted plans, filing assistance)
- FAQ (addressing parent concerns: wait times, what to expect, when to come in)

### Recommended Blocks
- LOCAL_KNOWLEDGE (connecting local environmental factors to conditions)
- PROCESS_TIMELINE (what happens during the visit)
- PAYMENT_STRIP (co-pays, financing)
- MID_CTA (trust-leveraging mid-page nudge)

### Pediatric-Specific
```yaml
common_conditions:
  - Ear infections
  - Strep throat
  - Allergies/asthma
  - Well-child visits
  - Sports physicals
  - Vaccinations

seasonal_patterns:
  winter: "Flu, RSV, ear infections"
  spring: "Allergies, cedar fever (TX), hay fever"
  summer: "Sports injuries, bug bites, heat illness"
  fall: "Back-to-school physicals, flu shots"

copy_voice:
  tone: Warm, reassuring, parent-empathetic
  avoid: Clinical jargon, condescension, fear-mongering
  emphasize: Speed of care, provider warmth, child comfort
  framing: "'Your child' not 'the patient'"

audience_framing:
  decision_maker: parent
  patient: child
  messaging: "Your child" not "the patient"
  trust_angle: "These are real parents bringing their kids here"
  urgency_cues: "same-day sick visits", "call before 4pm"

local_knowledge_focus:
  - Seasonal allergens specific to area (cedar, ragweed, mold)
  - Daycare/school density and illness transmission
  - Local hospital affiliations
  - Area demographics (family-heavy neighborhoods)
```

---

## Industry Comparison Matrix

```yaml
trust_signal_priority:
  home_services: [Licensing, Availability, Reviews]
  medical: [Credentials, Insurance, Comfort]
  pediatric_medical: [Board_Certifications, Languages, Insurance, Provider_Bios]
  legal: [Case_Results, Bar_Admissions, No_Fee_Unless_Win]
  financial: [Licenses, Transparency, Conservative_Language]

urgency_approach:
  home_services: High (emergency scenarios common)
  medical: Medium (some emergency, mostly planned)
  pediatric_medical: Medium-High (sick visits are urgent, well-child is planned)
  legal: Low (high consideration, slow decision)
  financial: Low (major financial decisions)

price_transparency:
  home_services: Ranges acceptable, exact after diagnosis
  medical: Ranges + insurance complexity
  legal: Fee structure must be crystal clear
  financial: APR + all fees must be disclosed

compliance_burden:
  home_services: Low (basic licensing)
  medical: High (HIPAA, professional regulations)
  legal: Very High (bar rules, advertising regulations)
  financial: Very High (federal + state regulations)

testimonial_approach:
  home_services: Specific outcomes, minimal restrictions
  medical: Comfort-focused, some restrictions
  legal: Heavy disclaimers required
  financial: Often not allowed or heavily restricted

form_strategy:
  home_services: Minimal fields (name + phone)
  medical: Standard (name, phone, insurance)
  legal: Medium (name, phone, case type, brief description)
  financial: Progressive (start minimal, build profile)
```

## Adaptation Checklist

When building page for specific niche:

1. **Check compliance requirements**
   - Are disclosures required?
   - Are there copy restrictions?
   - What credentials must be displayed?

2. **Identify trust signals**
   - What matters most to this audience?
   - What reduces anxiety in this industry?

3. **Assess urgency legitimacy**
   - Is urgency appropriate for this niche?
   - What creates legitimate urgency here?

4. **Review testimonial rules**
   - Can we use testimonials freely?
   - What disclaimers are required?

5. **Adapt copy voice**
   - What tone does this audience expect?
   - What language patterns are appropriate?

6. **Select appropriate blocks**
   - Which blocks are mandatory?
   - Which blocks don't apply?
   - Do any blocks need custom variants?

7. **Set pricing transparency**
   - How much detail can/should we show?
   - What disclaimers are needed?

8. **Review form requirements**
   - What fields are necessary?
   - Are there legal requirements (TCPA, etc)?