# Service Page Examples

Complete page implementations showing different niches, intents, and urgency levels.

## Available Examples

### 1. emergency-hvac-winter.yaml
**Scenario**: Winter heater failure, emergency repair needed
- **Niche**: HVAC
- **Intent**: fix_now (transactional)
- **Urgency**: emergency
- **Key Features**:
  - SAFETY_NOTICE for CO/gas hazards
  - SYMPTOM_MATRIX for self-diagnosis
  - PATH_CHOICE (repair vs replace)
  - Multiple availability indicators
  - SHORT_FORM + STICKY_CTA for mobile

**Use this as reference for**:
- Emergency home services (HVAC, plumbing, electrical)
- High-urgency scenarios
- Safety-critical situations
- Same-day service emphasis

### 2. emergency-plumbing-burst-pipe.yaml
**Scenario**: Burst pipe, water damage prevention
- **Niche**: Plumbing
- **Intent**: fix_now (transactional)
- **Urgency**: emergency
- **Key Features**:
  - Damage prevention messaging
  - Insurance coordination block
  - 24/7 emergency emphasis
  - Water shut-off instructions

**Use this as reference for**:
- Emergency plumbing
- Damage-prevention scenarios
- Insurance-involved repairs

### 3. dental-cosmetic-implants.yaml
**Scenario**: Dental implant research and planning
- **Niche**: Dental
- **Intent**: research (informational)
- **Urgency**: planning
- **Key Features**:
  - Extensive FAQ
  - Cost breakdown transparency
  - Process timeline (multi-month)
  - Insurance and financing emphasis
  - Before/after emphasis
  - Comfort/anxiety messaging

**Use this as reference for**:
- High-consideration services
- Research intent
- Medical/dental procedures
- Multi-step processes
- Anxiety reduction focus

## How to Use These Examples

1. **Find similar scenario**: Match niche, intent, and urgency to your use case
2. **Review block selection**: See which blocks were included and why
3. **Study copy patterns**: Note headline structure, explanation text, CTA language
4. **Check layout choices**: See how blocks are sequenced and grouped
5. **Adapt for your needs**: Use as template, modify for your specific situation

## Comparing Examples

| Feature | HVAC Emergency | Plumbing Emergency | Dental Research |
|---------|---------------|-------------------|-----------------|
| Blocks | 14 rows | 13 rows | 12 rows |
| SAFETY_NOTICE | Yes (CO hazard) | Yes (water damage) | No |
| SYMPTOM_MATRIX | Yes | Yes | No (single procedure) |
| PATH_CHOICE | Yes (repair/replace) | Yes (repair/repipe) | Yes (implant types) |
| PRIMARY_CTAS | 3 instances | 3 instances | 2 instances |
| FAQ count | 8 questions | 7 questions | 12 questions |
| Copy tone | Urgent, direct | Urgent, damage-focused | Gentle, educational |
| SCHEDULER | No (emergency) | No (emergency) | Yes (consultation) |

## Block Patterns Across Examples

### Common to All
- HERO (always first)
- PROCESS_TIMELINE (sets expectations)
- CREDENTIALS_LICENSES (builds trust)
- FAQ (reduces friction)
- FINAL_CTA (always last)

### Emergency-Specific
- AVAILABILITY_BADGE
- SAFETY_NOTICE
- AFTER_HOURS
- SHORT_FORM (not scheduler)
- STICKY_CTA for mobile

### Research-Specific
- Deep FAQ (10+ questions)
- Detailed PROCESS_TIMELINE (6+ steps)
- SCHEDULER (not urgent form)
- Educational PATH_CHOICE
- TESTIMONIAL with outcomes focus

### Niche-Specific
- Home services: SYMPTOM_MATRIX, BRANDS_SYSTEMS
- Dental: INSURANCE block, comfort messaging, BEFORE_AFTER
- Legal: CASE_TYPES, contingency fee structure, compliance disclosures

## Missing Example Scenarios

Future examples to add:
- **Personal injury car accident** (legal, compliance-heavy)
- **Roofing storm damage** (insurance coordination, visual proof)
- **Financial services mortgage** (regulatory disclosures, calculator tools)
- **Dental routine cleaning** (low urgency, maintenance focus)
- **HVAC tune-up** (preventive, seasonal, planning intent)
