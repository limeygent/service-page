---
name: service-page-builder
description: Intelligent service page builder for local/professional service businesses (HVAC, plumbing, roofing, dental, legal, etc). Use when users need to create conversion-optimized landing pages, service pages, or need to generate page layouts with conditional block logic. Generates Bootstrap 5 page structures with intent-driven content, MECLABS conversion principles, and niche-specific adaptations. Use for queries like "create a service page for my HVAC business," "build a landing page for emergency plumbing," or "generate a dental practice page." Always use this skill when users ask to build, create, or generate any page for a service business, even if they just say "I need a page for my business" without explicitly mentioning "service page." Covers all service niches: home services, medical, dental, pediatric, legal, financial, cleaning, lawn care, pest control, and more.
---

# Service Page Builder

Build conversion-optimized service pages using conditional block logic, intent analysis, and Bootstrap 5 layouts.

## Quick Start Workflow

1. **Gather inputs** - Collect business parameters (see input-parameters.md)
2. **Analyze intent** - Map user's emotional/functional drivers (see intent-methodology.md)
3. **Select blocks** - Evaluate conditional logic to determine which blocks to include
4. **Generate layout** - Create Bootstrap 5 page structure with proper ordering
5. **Populate content** - Fill blocks with intent-driven, MECLABS-optimized copy

## Core Execution Steps

### Step 1: Input Collection

Ask the user for required parameters. Minimum viable inputs:
- `niche` (hvac, plumbing, roofing, electrical, dental, medical, pediatric_medical, personal_injury, financial, cleaning, lawn_care, pest_control, other)
- `intent_primary` (fix_now, schedule_soon, research)
- `urgency` (emergency, soon, planning)
- Location (city, state)
- Business name

For comprehensive page generation, collect additional parameters from input-parameters.md

#### Step 1a: Load Client Profile (if available)

Check for a client profile at `~/.claude/config/clients/{slug}/`:
- `profile.json` for business name, city, niche, brand color, phone, providers
- `background.md` for comprehensive business knowledge (services, team, differentiators)
- `page-templates/*.json` for pre-defined block selections and ordering per service type

If a client profile exists, auto-populate business_profile fields and skip redundant questions.

**Page templates shortcut:** If a matching page template exists (e.g., `sick-visit.json` for ear infections/strep/flu, `preventive.json` for well-child visits), use it to skip Step 2 entirely. The template provides the block list, order, modifiers, and per-block notes. When `skip_block_index: true`, go straight to Step 3 using the template's block list instead of reading block-catalog.md.

#### Step 1c: City Research (WebSearch)

Run 2-4 parallel WebSearches to gather local data for LOCAL_KNOWLEDGE and service area blocks:
- `"{city} {state} demographics population neighborhoods"`
- `"{city} {niche} common issues seasonal patterns"` (e.g., "McKinney HVAC common issues seasonal patterns")
- `"{business_name} {city} reviews"` (if not already known)
- Climate, soil, environmental factors relevant to the niche

#### Step 1b: Determine Page-Level Modifiers

After collecting niche and urgency, set 4 modifiers (auto-detected from niche, can be overridden):

| Modifier | Auto-Detection | Effect |
|----------|----------------|--------|
| `stakes` | high: cosmetic dentist, legal, surgeon; low: cleaning, lawn care | high = deeper CREDENTIALS, MEET_THE_TEAM, PROCESS; sticky TOC |
| `regulated` | hvac, plumbing, electrical, dental, legal, financial, medical | CREDENTIALS_LICENSES mandatory; compliance disclosures |
| `high_ticket` | roofing, remodel, cosmetic dentist, dental implants, solar | PRICING with ranges + financing |
| `recurring` | cleaning, lawn care, pest control, pool, general dentist | Plan pricing emphasis; consistency messaging |

See `references/input-parameters.md` → "Page-Level Modifiers" for full schema.

### Step 2: Block Selection and Ordering

Read block-catalog.md (the slim index). It contains WHEN conditions and ordering rules for all blocks.

1. Evaluate each block's WHEN condition against collected inputs + page-level modifiers
2. Select 10-15 blocks appropriate for this niche/urgency/intent
3. Order them using the priority-based sequencing and decision tree in the index

Do NOT read individual block detail files yet. Selection and ordering uses only the index.

### Step 3: Layout Generation

Apply ordering constraints from references/layout-schema.md:
- HERO always first
- SAFETY_NOTICE within first 2 rows if present
- SYMPTOM_MATRIX → PATH_CHOICE → PRICING_TABLE sequence
- FAQ before FINAL_CTA
- FINAL_CTA last

Generate Bootstrap 5 row structure with responsive column definitions.

### Step 4: Content Population

For each selected block in order, read its detailed spec from `references/blocks/{block-name}.md`, then generate content using:
- **Block spec** - Follow the content model, layout, and MECLABS tags from the block file
- **Intent mapping** - Address emotional/functional drivers (see intent-methodology.md)
- **MECLABS principles** - Optimize for motivation, value prop, incentive while reducing friction/anxiety (see meclabs-principles.md)
- **Copy templates** - Use niche-specific language patterns (see references/content-templates.md)

Read each block file only when you're ready to write that section. Do not pre-read all block files.

#### Step 4a: Per-Block SEO Checklist

Before writing each section, answer these 5 questions:
1. **What question does this section answer?** The H2 and first sentence should satisfy that query as a standalone passage.
2. **What's the one thing here a competitor page won't have?** Local data, quantified claims, practitioner-specific detail, or actionable specifics.
3. **Which named entities belong in this section?** Doctor names, hospitals, license numbers, school districts, neighborhoods. At least one per section where natural.
4. **Is there a list, table, or comparison that makes this scannable?** Front-load key info, use structured content for multi-item data.
5. **Can the first sentence stand alone as a featured snippet answer?** Write it as if Google will pull just that sentence.

#### Step 4b: Apply Anti-Slop Content Rules

Before finalizing content, enforce all 5 anti-slop rules (see `references/content-templates.md` → "Anti-Slop Content Rules"):
1. **Block suppression** over generic content (missing > generic)
2. **Ban vague adjectives** without evidence
3. **2+ local references** per page (landmarks, codes, neighborhoods)
4. **Quantify or kill** every claim
5. **Falsifiability test** on every sentence

#### Step 4c: Apply Progressive CTA System

Ensure CTA text evolves across the page. Each PRIMARY_CTAS instance and FINAL_CTA must use different text matching the progressive stage for its position. See `references/block-catalog.md` → "Progressive CTA System" and `references/content-templates.md` → "Progressive CTA Copy Patterns".

### Step 5: Output Generation

Create complete Bootstrap 5 HTML or YAML page structure. Include:
- Proper Bootstrap grid classes (col-xs-12, col-lg-6, etc)
- Responsive behavior annotations
- Intent mapping metadata for each block
- MECLABS contribution tags
- Image placeholders where appropriate

**Always write the output to a file.** Never return the full HTML/YAML in your response text. Save it to the specified output path (or `output/` by default), then return only a brief summary of what was built (sections, block count, key compliance notes). This keeps context usage efficient when running as a subagent.

## Critical Rules

1. **Bootstrap 5 Only** - All layouts use Bootstrap grid system
2. **Intent-Driven** - Every block addresses specific emotional/functional needs
3. **Conditional Logic** - Blocks appear only when WHEN conditions met
4. **Ordering Constraints** - Follow strict sequence rules (HERO first, FAQ before FINAL_CTA, etc)
5. **Mobile-First** - Define responsive behavior for each block
6. **No Generic Copy** - All content specific to niche, location, urgency
7. **MECLABS Explicit** - Tag each block with formula contribution
8. **Images Strategic** - Only include when functional (trust, proof, visualization)
9. **🚨 SAFETY FIRST** - Life safety warnings MUST appear in rows 2-3, BEFORE any educational content
10. **No Redundancy** - If two blocks serve same purpose, use BETTER one, delete the other
11. **Social Proof Volume** - Emergency pages need 4+ reviews (carousel), not single testimonial
12. **Strategic Testimonials** - Place honesty/transparency testimonials BEFORE pricing sections
13. **Progressive CTAs** - CTA text and tone must evolve as reader scrolls; never repeat the same CTA verbatim top-to-bottom. Phone number CTAs count: vary the surrounding text (e.g., "Call (512) 555-0147" first, then "Speak to Our Team at (512) 555-0147", then "Ready? Call (512) 555-0147 Now"). Bare phone number buttons should appear at most once.
14. **Anti-Slop Enforcement** - Block suppression over generic content; ban vague adjectives; quantify or kill; falsifiability test on every claim
15. **FAQ Schema Markup** - Implement FAQPage JSON-LD structured data whenever FAQ block is rendered
16. **No Em-Dashes or En-Dashes** - No — (U+2014) or – (U+2013) characters anywhere in the output. Use colons, commas, periods, or parentheses instead (AI writing tell)

## Niche-Specific Adaptations

Different niches require different approaches:

**HVAC/Plumbing/Roofing** (Home Services):
- Emphasize speed, availability, licensing
- Include SAFETY_NOTICE for emergencies
- SYMPTOM_MATRIX for self-diagnosis
- PATH_CHOICE (repair vs replace)

**Dental/Medical**:
- Emphasize credentials, insurance, patient comfort
- Include testimonials with outcomes
- FAQ addresses anxiety about pain, cost, time

**Pediatric/Family Medical**:
- Parent is decision-maker, child is patient
- MEET_THE_TEAM mandatory (board certifications, languages)
- LOCAL_KNOWLEDGE for seasonal health patterns
- Warm, reassuring copy voice

**Personal Injury/Legal**:
- Compliance-heavy (no guaranteed outcomes)
- Contingency fee transparency
- Case types instead of brands/systems
- Statute of limitations urgency

**Financial Services**:
- Regulatory disclosures required
- Cannot use certain testimonials
- APR/fee transparency critical
- Conservative language, avoid urgency tactics

See references/niche-adaptations.md for complete patterns.

---

## ⚡ Emergency vs General Service Pages

**CRITICAL: Emergency and general service pages require DIFFERENT patterns.**

### Emergency Pages (`urgency == 'emergency'` or `'soon'`)

**User State:** Decision mode - "Who do I call RIGHT NOW?"
**Psychology:** Anxious, stressed, needs reassurance + speed
**Goal:** Drive immediate action (call/text)

**Required Blocks:**
1. **SAFETY_NOTICE** - Row 2-3 (life-critical priority)
2. **REVIEWS_CAROUSEL** - 4-6 reviews for volume social proof (rows 4-6)
3. **AVAILABILITY_BADGE** - Create urgency ("3 techs available today")
4. **SERVICE_AREAS_LIST** - Fast geographic confirmation (text list, not map)
5. **FINANCING_ALERT** - Remove cost objection (after pricing)
6. **TESTIMONIAL_CALLOUT** - Strategic honesty quote (before pricing)
7. **AWARD_BADGES** - Visual credibility (BBB, years, customer count)
8. **STICKY_CTA** - Mobile persistent call/text buttons

**Optimal Flow:**
```
Hero + SHORT_FORM →
AVAILABILITY_BADGE →
SAFETY_NOTICE (if hazard possible) →
BRANDS_SYSTEMS →
REVIEWS_CAROUSEL (trust volume) →
SYMPTOM_MATRIX →
PATH_CHOICE (repair vs replace) →
TESTIMONIAL_CALLOUT (honesty) →
PRICING_TABLE →
FINANCING_ALERT →
PAYMENT_STRIP →
MID_CTA (trust nudge) →
PROCESS_TIMELINE + GUARANTEE_CHIPS →
MEET_THE_TEAM (if high-stakes) →
TRUST + AWARD_BADGES →
LOCAL_KNOWLEDGE (if verifiable data) →
SERVICE_AREAS_LIST →
OPERATIONS + AFTER_HOURS →
PRIMARY_CTAS →
FAQ →
FINAL_CTA
```

**Performance Data (from emergency heater repair page):**
- REVIEWS_CAROUSEL: +20-25% conversion
- FINANCING_ALERT: +12-15% on high-ticket
- AWARD_BADGES: +8-10% trust
- SERVICE_AREAS_LIST: -10% bounce
- **Combined lift: 25-35% total improvement**

**What to AVOID:**
- ❌ Single testimonial only (need volume for emergency)
- ❌ Educational content before safety warnings
- ❌ Redundant diagnostic content (one comprehensive section beats two half-versions)
- ❌ Interactive maps (too slow, use text list)
- ❌ Buried financing (make it prominent)

---

### General Service Pages (`urgency == 'planning'`)

**User State:** Research mode - "Comparing options, gathering info"
**Psychology:** Methodical, wants to understand, less time pressure
**Goal:** Educate, build consideration, capture lead

**Different Approach:**
- Single testimonial may suffice
- Educational content can come earlier
- Fewer CTAs (less aggressive)
- Maps acceptable (user has time to interact)
- More detailed explanations
- Service menu/catalog focus

**Key Difference:**
```
Emergency = Trust + Speed + Reassurance → Call NOW
Planning = Education + Options + Consideration → Schedule Later
```

---

## Output Format

Generate one of:
- **YAML page structure** - For review/editing before implementation
- **Bootstrap 5 HTML** - For direct deployment
- **Content brief** - For human copywriter to implement

Default to YAML structure unless user requests HTML.

## Reference Files

Load these during execution. Read each file **once only** (do not re-read files you have already loaded):

- **input-parameters.md** - Complete input schema with defaults
- **block-catalog.md** - All blocks with conditional logic and content models (large file: read in full, do not re-read)
- **references/layout-schema.md** - Bootstrap grid system and responsive rules
- **intent-methodology.md** - Three-layer intent analysis from intent-analyzer skill
- **meclabs-principles.md** - Conversion optimization formula
- **references/content-templates.md** - Copy patterns and examples per niche
- **niche-adaptations.md** - Industry-specific requirements
- **references/emergency-page-patterns.md** - Emergency service page architecture. **ONLY read this file if urgency is 'emergency'. Skip entirely for 'soon' or 'planning' urgency.**

## HTML Skeleton

See references/examples/README.md for the HTML page skeleton template (DOCTYPE, CDN links, CSS variables, JSON-LD placement, sticky CTA pattern).