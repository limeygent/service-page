# Service Page Builder

A Claude Code skill that generates conversion-optimized service pages for local and professional service businesses.

## What It Does

Generates complete, production-ready Bootstrap 5 HTML service pages with:

- **Conditional block logic** - Blocks appear only when their conditions are met (safety notices for emergencies, financing alerts for high-ticket services, etc.)
- **Intent-driven content** - Three-layer intent analysis maps emotional drivers, functional needs, and trust heuristics to page structure
- **MECLABS conversion optimization** - Every block is tagged with its contribution to the conversion formula (C = 4m + 3v + 2(i-f) - 2a)
- **Niche-specific adaptations** - Different patterns for HVAC, plumbing, dental, legal, financial, pediatric, cleaning, lawn care, pest control, and more
- **Anti-slop content rules** - No vague adjectives without evidence, 2+ local references per page, quantify-or-kill on every claim, falsifiability test on every sentence
- **Progressive CTA system** - CTA text evolves across 5 positions as the reader accumulates trust
- **Compliance support** - AHPRA (Australian medical/dental), bar rules (legal), TCPA (forms), regulatory disclosures (financial)

## Supported Niches

| Category | Niches |
|----------|--------|
| Home Services | HVAC, plumbing, roofing, electrical |
| Medical | Dental, pediatric, general medical |
| Professional | Personal injury law, financial services |
| Recurring | Cleaning, lawn care, pest control |

## Installation

Copy the skill folder to your Claude Code skills directory:

```
~/.claude/skills/service-page/
```

Or clone this repo directly:

```bash
git clone https://github.com/limeygent/service-page.git ~/.claude/skills/service-page
```

## Usage

Invoke with `/service-page` or let Claude auto-detect when you ask for a service page:

```
/service-page

Create a service page for my HVAC company, ABC Heating in McKinney TX.
Emergency heater repair, 24/7 service, licensed since 1987.
```

### Minimum Required Inputs

- Business name
- City and state
- Niche (HVAC, dental, legal, etc.)
- Primary intent (emergency, schedule soon, research)

Everything else is inferred from sensible defaults or gathered through follow-up questions.

## Skill Structure

```
service-page/
├── skill.md                          # Main skill instructions
├── block-catalog.md                  # All blocks with conditional logic
├── intent-methodology.md             # Three-layer intent analysis
├── meclabs-principles.md             # Conversion optimization formula
├── niche-adaptations.md              # Industry-specific patterns
├── input-parameters.md               # Complete input schema
├── evals/
│   └── evals.json                    # Test cases for skill evaluation
├── references/
│   ├── layout-schema.md              # Bootstrap grid and responsive rules
│   ├── content-templates.md          # Copy patterns per niche
│   ├── emergency-page-patterns.md    # Emergency service page architecture
│   └── examples/
│       ├── emergency-hvac-winter.yaml
│       ├── dental-cosmetic-implants.yaml
│       └── pediatric-ear-infection.yaml
└── output/
    └── ear-infection-treatment-frisco-preview.html  # Example output
```

## Key Design Principles

### Emergency vs Planning Pages

Emergency pages prioritize speed, trust volume (4+ reviews), and safety notices in rows 2-3. Planning pages prioritize education, decision support, and softer CTAs.

### Block Selection

Each block has a `WHEN` condition evaluated against inputs:

```
IF safety_hazard_possible == true → Include SAFETY_NOTICE
IF review_count >= 20 AND avg_rating >= 4.5 → Include REVIEWS_SNAPSHOT
IF urgency == 'emergency' → Include STICKY_CTA, AVAILABILITY_BADGE
IF recurring == true → Plan pricing emphasis
```

### Content Quality Rules

1. **Block suppression over generic content** - Missing is better than generic
2. **Ban vague adjectives** without evidence backing
3. **2+ local references** per page (named neighborhoods, climate data, local codes)
4. **Quantify or kill** every claim
5. **Falsifiability test** - If a competitor could copy the sentence unchanged, rewrite it
6. **No em-dashes or en-dashes** - AI writing tell

## Eval Results

Tested across 3 diverse scenarios with 10 assertions each:

| Eval | Score |
|------|-------|
| Emergency plumbing (Austin, TX) | 10/10 |
| Cosmetic veneers (Sydney, AHPRA-regulated) | 10/10 |
| Recurring lawn care (Charlotte, NC) | 10/10 |

Skill outperforms baseline (no skill) by +13% average pass rate, with +40% on emergency pages.

## License

MIT
