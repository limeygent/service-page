# Layout Schema Reference

## Bootstrap Grid System Integration

### Grid Philosophy
The layout system uses Bootstrap 5's 12-column grid as the foundation. Every block must specify column widths for each breakpoint to ensure responsive behavior.

### Breakpoint Strategy
- **xs (0-575px)**: Mobile portrait - Stack everything, full-width CTAs
- **sm (576-767px)**: Mobile landscape - Still mostly stacked
- **md (768-991px)**: Tablet - Begin side-by-side layouts
- **lg (992-1199px)**: Desktop - Full intended design
- **xl (1200px+)**: Large desktop - Same as lg, more whitespace

### Container Types
1. **container-fluid**: Edge-to-edge (hero sections, full-width backgrounds)
2. **container**: Standard responsive max-widths (most content rows)
3. **container + custom max-width**: Narrow reading content (FAQ, long-form text)

## Row Structure Specification

### Basic Row Schema
```yaml
row:
  id: string                    # Unique identifier
  container: enum               # fluid | standard | narrow
  classes: string[]             # Bootstrap utility classes
  layout:
    type: enum                  # single_column | two_column | three_column | asymmetric
    responsive_behavior:        # How layout changes per breakpoint
      xs: enum                  # stack | full | partial
      md: enum
      lg: enum
  blocks: array                 # Blocks within this row
```

### Layout Type Definitions

**single_column**
- All blocks stack vertically
- Full width (col-12) at all breakpoints
- Used for: HERO (text-only), SYMPTOM_MATRIX, FAQ, FINAL_CTA

**two_column**
- Desktop: 50/50 or custom split (e.g., 60/40, 70/30)
- Tablet: Usually 50/50 or stack
- Mobile: Always stack
- Used for: HERO (text + form), trust_row (REVIEWS + CREDENTIALS), ops_row (COVERAGE + SERVICE_AREA)

**three_column**
- Desktop: 33/33/33 or custom
- Tablet: 50/50 + stack third, or stack all
- Mobile: Stack all
- Used for: Feature trios, trust signals, guarantee chips

**asymmetric**
- Custom column widths per block
- Most flexible, requires explicit column specification
- Used for: HERO (60/40 split), mixed-weight content rows

### Block Column Specification

Every block must define:
```yaml
block:
  column:
    xs: number    # 1-12 (usually 12 on mobile)
    sm: number    # Optional, defaults to xs
    md: number    # When layout begins to split
    lg: number    # Full desktop layout
    xl: number    # Optional, defaults to lg
```

### Visual Ordering on Mobile

```yaml
block:
  order:
    xs: number    # Visual order on mobile (1, 2, 3...)
    md: number    # Desktop order (can differ)
```

**Use case**: Form appears after text on mobile, but beside text on desktop
- Text: order.xs=1, order.md=1
- Form: order.xs=2, order.md=2
- On mobile: Text first, form second
- On desktop: Side-by-side at same visual level

## Row Patterns Library

### Pattern: hero_row
```yaml
type: asymmetric
blocks: [HERO, SHORT_FORM]
desktop: 7/5 split (text/form)
mobile: stack (text first)
classes: ["py-5", "bg-gradient-light"]
```

### Pattern: trust_row
```yaml
type: two_column
blocks_any_of: [REVIEWS_SNAPSHOT, CREDENTIALS_LICENSES, PARTNERS_AFFILIATIONS, MEET_THE_TEAM, AWARD_BADGES]
desktop: 50/50 or 40/30/30 if three blocks
mobile: stack
classes: ["py-4", "bg-white", "border-top"]
```

### Pattern: ops_row
```yaml
type: two_column
blocks_any_of: [COVERAGE_HOURS, SERVICE_AREA, AFTER_HOURS]
desktop: 50/50
mobile: stack (hours first, map second)
classes: ["py-4"]
```

### Pattern: decision_row
```yaml
type: two_column or three_column
blocks_any_of: [PROCESS_TIMELINE, GUARANTEE_CHIPS, INSURANCE, LOCAL_KNOWLEDGE]
desktop: Side-by-side
mobile: stack
classes: ["py-5", "bg-light"]
```

## Bootstrap Classes Strategy

### Spacing (Padding/Margin)
- **py-5**: Large vertical padding (48px) for major sections
- **py-4**: Medium vertical padding (24px) for subsections
- **py-3**: Small vertical padding (16px) for tight rows
- **mb-3, mb-4**: Bottom margin for element spacing
- **pe-lg-4**: End padding (right in LTR) on large screens only

### Background Colors
- **bg-white**: Clean white background
- **bg-light**: Very light gray (#f8f9fa)
- **bg-gradient-light**: Subtle gradient (custom)
- **bg-primary**: Brand color background (use sparingly)

### Borders & Shadows
- **border-top**: 1px top border for visual separation
- **shadow-sm**: Subtle box shadow
- **rounded**: 4px border radius

### Text Utilities
- **text-center**: Center align text
- **text-muted**: Gray text (#6c757d) for supporting info
- **small**: Smaller font size (0.875em)

## Visual Weight System

### Purpose
Determine loading priority and above-the-fold budget.

### Weight Categories
- **light**: Minimal resources (text, simple forms, icons)
  - Examples: SHORT_FORM (just HTML), GUARANTEE_CHIPS, text-only blocks
  
- **medium**: Moderate resources (1-2 images, embedded components)
  - Examples: HERO with image, BRANDS_SYSTEMS (logos), TESTIMONIAL, MEET_THE_TEAM (may include photos), REVIEWS_CAROUSEL, AWARD_BADGES (logos/images)

- **heavy**: High resources (maps, schedulers, galleries, videos)
  - Examples: SERVICE_AREA (map), SCHEDULER (embed), BEFORE_AFTER_GALLERY

**Additional weight classifications:**
- MID_CTA: light
- LOCAL_KNOWLEDGE: light
- FINANCING_ALERT: light
- SERVICE_AREAS_LIST: light
- TESTIMONIAL_CALLOUT: light

### Loading Strategy by Weight
```yaml
light:
  lazy: false
  priority: high
  above_fold: allow

medium:
  lazy: conditional (not if above fold)
  priority: medium
  above_fold: allow if critical

heavy:
  lazy: true (almost always)
  priority: low
  above_fold: avoid
```

## Responsive Behavior Per Block Type

### Text-Heavy Blocks
(FAQ, TESTIMONIAL, EXPLANATION_TEXT)
- Mobile: Full width, readable line length (max 65 characters)
- Desktop: May constrain to 8-10 columns for readability
- Never lazy load

### Data Blocks
(SYMPTOM_MATRIX, PRICING_TABLE)
- Mobile: Alternative rendering (accordion, cards, scrollable)
- Desktop: Full table or grid layout
- CSS handles transformation, not JS

### Form Blocks
(SHORT_FORM, SCHEDULER)
- Mobile: Full width, large touch targets (min 48px)
- Desktop: May be sidebar, can use standard sizing
- Validation and error states explicit

### Image Blocks
(HERO image, SERVICE_AREA map, BRANDS_SYSTEMS logos)
- Mobile: Often suppressed or deferred
- Desktop: Visible, lazy loaded if below fold
- WebP format with fallback

### Media Blocks
(VIDEO, BEFORE_AFTER_GALLERY)
- Mobile: Poster/thumbnail only, play on tap
- Desktop: May autoplay (muted), full interactivity
- Heavy lazy loading

## Container Width Strategy

### Standard Container Breakpoints
```css
container max-widths:
  sm: 540px
  md: 720px
  lg: 960px
  xl: 1140px
  xxl: 1320px
```

### When to Override
**Narrow content** (reading text):
```yaml
container: standard
custom_max_width: 800px  # Easier to read
apply_to: [FAQ, long_form_content, blog_style_sections]
```

**Full-width visuals**:
```yaml
container: fluid
apply_to: [HERO with background, maps, full-bleed images]
nested_content: Use inner container for text overlay
```

## Common Layout Patterns

### Pattern 1: Hero with Sidebar Form
```yaml
row:
  container: standard
  layout: asymmetric
  blocks:
    - HERO: {xs: 12, lg: 7, order: {xs: 1}}
    - SHORT_FORM: {xs: 12, lg: 5, order: {xs: 2}}
```

### Pattern 2: Full-Width Alert + Two-Column Content
```yaml
row_1:
  container: fluid
  layout: single_column
  blocks: [SAFETY_NOTICE]
  classes: ["alert-danger", "py-3"]

row_2:
  container: standard
  layout: two_column
  blocks: [AVAILABILITY_BADGE, explanation_text]
```

### Pattern 3: Three-Column Trust Row
```yaml
row:
  container: standard
  layout: three_column
  blocks:
    - REVIEWS_SNAPSHOT: {xs: 12, md: 6, lg: 4}
    - CREDENTIALS: {xs: 12, md: 6, lg: 4}
    - PARTNERS: {xs: 12, md: 12, lg: 4}  # Note: Full width on md
```

### Pattern 4: Asymmetric Process + Guarantees
```yaml
row:
  container: standard
  layout: asymmetric
  blocks:
    - PROCESS_TIMELINE: {xs: 12, lg: 8}
    - GUARANTEE_CHIPS: {xs: 12, lg: 4}  # Sidebar on desktop
```

## Performance Considerations

### Above-the-Fold Budget
- Target: First 1-2 rows only
- Max weight: 1 medium + 2 light blocks
- Critical CSS inline
- Defer non-critical blocks

### Image Loading Strategy
```yaml
hero_image:
  loading: eager (if above fold)
  fetchpriority: high
  
other_images:
  loading: lazy
  fetchpriority: low
```

### Third-Party Embeds
(Calendly, review widgets, chat)
- Always lazy load
- Activate on scroll or interaction
- Provide loading placeholder

## Accessibility Requirements

### Every Row Must Have
- Proper heading hierarchy (h1 → h2 → h3, no skips)
- Sufficient color contrast (4.5:1 minimum)
- Keyboard navigation support
- Screen reader-friendly structure

### Block-Specific
- Forms: Associated labels, error states, ARIA
- Tables: th elements, scope attributes
- Images: Descriptive alt text (not decorative)
- Interactive: Focus states visible

## Mobile-First Defaults

### When in Doubt
1. Stack vertically on mobile (xs: 12)
2. Allow side-by-side on desktop (lg: 6 or less)
3. Put most important content first (order: 1)
4. Suppress decorative images on mobile
5. Use large touch targets (min 48px height)

### Mobile CTA Strategy
- Primary CTA: Full width, fixed bottom (sticky)
- Secondary CTAs: Full width, stacked
- Tertiary CTAs: Text links, grouped

## Block Ordering Algorithm

### Priority-Based Sequencing

Blocks must appear in this order to optimize conversion flow:

**Priority 1: MUST BE FIRST**
- HERO (always row 1)

**Priority 2: EARLY ROWS (rows 2-3)**
- AVAILABILITY_BADGE (if present, immediately after HERO)
- SAFETY_NOTICE (if present, must be within first 2-3 rows)

**Priority 3: EARLY-MID (rows 3-6)**
- BRANDS_SYSTEMS (if present)
- REVIEWS_CAROUSEL (if present, before SYMPTOM_MATRIX for emergency trust-building)
- SYMPTOM_MATRIX (if present)
- PATH_CHOICE (must follow SYMPTOM_MATRIX if both present)
- TESTIMONIAL_CALLOUT (after PATH_CHOICE, before PRICING_TABLE)
- PRICING_TABLE (must follow PATH_CHOICE if present, otherwise after SYMPTOM_MATRIX)
- FINANCING_ALERT (immediately after PRICING_TABLE, before PAYMENT_STRIP)
- PAYMENT_STRIP (immediately after PRICING_TABLE/FINANCING_ALERT if present)

**Priority 4: MID (rows 6-9)**
- MID_CTA (after main content blocks, around row 6-7)
- GUARANTEE_CHIPS (near pricing content)
- PROCESS_TIMELINE
- trust_row blocks (REVIEWS_SNAPSHOT, CREDENTIALS_LICENSES, TESTIMONIAL, MEET_THE_TEAM, AWARD_BADGES)
- LOCAL_KNOWLEDGE (after core service content, before FAQ)
- ops_row blocks (COVERAGE_HOURS, SERVICE_AREA, AFTER_HOURS)
- SERVICE_AREAS_LIST (after ops_row, geographic confidence)
- SCHEDULER (if present)
- PRIMARY_CTAS (after major content blocks)

**Priority 5: LATE (rows 9-11)**
- INSURANCE (if present)
- Additional TESTIMONIAL (if not in trust_row)
- FAQ (must come before FINAL_CTA)

**Priority 6: MUST BE LAST**
- FINAL_CTA (always last row)

**Priority FLOATING (Can Appear Multiple Times)**
- PRIMARY_CTAS (after major decision points - 2-3 instances)
- PRIVACY_TCPA (adjacent to every form)
- STICKY_CTA (fixed position mobile, not a row)

### Sequencing Rules

```yaml
dependencies:
  PATH_CHOICE:
    requires_before: SYMPTOM_MATRIX (optional but recommended)
    requires_after: PRICING_TABLE (if both present)

  PRICING_TABLE:
    requires_after: [SYMPTOM_MATRIX, PATH_CHOICE] (if present)

  PAYMENT_STRIP:
    requires_after: PRICING_TABLE

  TESTIMONIAL_CALLOUT:
    requires_before: PRICING_TABLE (strategic placement)

  FINANCING_ALERT:
    requires_after: PRICING_TABLE
    requires_before: PAYMENT_STRIP

  REVIEWS_CAROUSEL:
    preferred_position: before SYMPTOM_MATRIX (early trust for emergency)

  MID_CTA:
    preferred_position: around row 6-7 (after main content, before trust section)

  FAQ:
    requires_before: FINAL_CTA

  SAFETY_NOTICE:
    max_row: 3

conflicts:
  - SHORT_FORM in HERO column + SCHEDULER in separate row (redundant, choose one)
  - Multiple instances of same block (except PRIMARY_CTAS, PRIVACY_TCPA)
```

### Ordering Decision Tree

```
1. Start with HERO
2. If urgency == emergency AND (SAFETY_NOTICE or AVAILABILITY_BADGE exists)
   → Insert immediately after HERO
3. If REVIEWS_CAROUSEL exists AND urgency == emergency
   → Place early for trust-building (before SYMPTOM_MATRIX)
4. If SYMPTOM_MATRIX exists
   → Place in early-mid
   → If PATH_CHOICE exists, place immediately after
   → If TESTIMONIAL_CALLOUT exists, place after PATH_CHOICE
   → If PRICING_TABLE exists, place after TESTIMONIAL_CALLOUT or PATH_CHOICE or SYMPTOM_MATRIX
   → If FINANCING_ALERT exists, place immediately after PRICING_TABLE
5. Insert MID_CTA around row 6-7 (after main content, before trust section)
6. Insert PROCESS_TIMELINE in mid section
7. Group trust blocks into trust_row if 2+ present
   → Include MEET_THE_TEAM and AWARD_BADGES with CREDENTIALS_LICENSES
8. Insert LOCAL_KNOWLEDGE after core service content, before FAQ
9. Group ops blocks into ops_row if 2+ present
   → If SERVICE_AREAS_LIST exists, place after ops_row
10. Place FAQ after all content, before FINAL_CTA
11. End with FINAL_CTA
```

## Bootstrap Component Classes Reference

### Buttons
```yaml
button_classes:
  base: "btn"
  variants:
    - btn-primary      # Brand color
    - btn-danger       # Emergency/urgent (red)
    - btn-success      # Positive action (green)
    - btn-outline-primary  # Secondary action
    - btn-outline-danger   # Secondary urgent

  sizes:
    - btn-lg           # Large (hero, primary CTAs)
    - btn-sm           # Small (secondary actions)

  widths:
    - w-100            # Full width (mobile CTAs)

  states:
    - disabled         # Disabled state
    - active          # Active/pressed state

usage_patterns:
  primary_cta: "btn btn-danger btn-lg"
  secondary_cta: "btn btn-outline-danger btn-lg"
  form_submit: "btn btn-primary w-100"
  mobile_sticky: "btn btn-danger w-100"
```

### Cards
```yaml
card_classes:
  structure:
    - card             # Container
    - card-body        # Main content area
    - card-header      # Optional header
    - card-footer      # Optional footer
    - card-title       # Title within body
    - card-text        # Text within body

  styling:
    - shadow           # Default shadow
    - shadow-sm        # Subtle shadow
    - shadow-lg        # Heavy shadow
    - border-0         # Remove border
    - rounded          # Rounded corners

usage_patterns:
  sidebar_form: "card shadow"
  testimonial: "card border-0 shadow-sm"
  pricing_card: "card shadow-lg"
```

### Alerts
```yaml
alert_classes:
  base: "alert"
  variants:
    - alert-warning    # Yellow (safety notices)
    - alert-danger     # Red (critical alerts)
    - alert-info       # Blue (informational)
    - alert-success    # Green (confirmation)

  features:
    - alert-dismissible  # Can be closed
    - fade show         # Fade in animation

usage_patterns:
  safety_notice: "alert alert-warning border-start border-warning border-5"
  availability: "alert alert-info mb-0"
```

### Forms
```yaml
form_classes:
  inputs:
    - form-control     # Text inputs, textareas, selects
    - form-label       # Labels
    - form-select      # Dropdowns
    - form-check       # Checkboxes/radios
    - form-check-input # Checkbox/radio input
    - form-check-label # Checkbox/radio label

  validation:
    - is-valid         # Valid state (green)
    - is-invalid       # Invalid state (red)
    - valid-feedback   # Success message
    - invalid-feedback # Error message

  sizing:
    - form-control-lg  # Large inputs
    - form-control-sm  # Small inputs

usage_patterns:
  standard_input: "form-control"
  error_input: "form-control is-invalid"
  mobile_input: "form-control form-control-lg"
```

### Badges
```yaml
badge_classes:
  base: "badge"
  variants:
    - bg-primary       # Brand color badge
    - bg-secondary     # Gray badge
    - bg-success       # Green badge
    - bg-warning       # Yellow badge
    - bg-danger        # Red badge
    - bg-info          # Blue badge

  shapes:
    - rounded-pill     # Pill-shaped

  sizing:
    - p-2, p-3        # Padding for larger badges

usage_patterns:
  trust_signal: "badge bg-primary p-3"
  guarantee: "badge rounded-pill bg-success"
  credential: "badge bg-light text-dark"
```

### Lists
```yaml
list_classes:
  groups:
    - list-group              # Container
    - list-group-item         # Individual item
    - list-group-item-action  # Clickable item

  styling:
    - list-group-flush        # Remove borders
    - list-unstyled          # Remove bullets/numbers

  variants:
    - list-group-item-primary  # Colored items
    - list-group-item-success

usage_patterns:
  features_list: "list-unstyled"
  steps_list: "list-group list-group-flush"
```

### Tables
```yaml
table_classes:
  base: "table"
  variants:
    - table-striped    # Zebra striping
    - table-bordered   # Add borders
    - table-hover      # Hover effect

  responsive:
    - table-responsive # Horizontal scroll on mobile
    - table-responsive-md # Responsive below md breakpoint

usage_patterns:
  pricing_table: "table table-striped"
  symptom_matrix: "table table-hover d-none d-md-table"  # Hide on mobile
```

### Spacing Utilities (Comprehensive)
```yaml
spacing:
  margin:
    all: m-0, m-1, m-2, m-3, m-4, m-5
    top: mt-0 through mt-5
    bottom: mb-0 through mb-5
    start: ms-0 through ms-5  # Left in LTR
    end: me-0 through me-5    # Right in LTR
    x_axis: mx-0 through mx-5
    y_axis: my-0 through my-5

  padding:
    all: p-0 through p-5
    top: pt-0 through pt-5
    bottom: pb-0 through pb-5
    start: ps-0 through ps-5
    end: pe-0 through pe-5
    x_axis: px-0 through px-5
    y_axis: py-0 through py-5

  responsive:
    - py-3 py-md-4 py-lg-5  # Increase padding at larger breakpoints
    - mb-4 mb-lg-0          # Remove margin on desktop

scale:
  0: 0rem
  1: 0.25rem  (4px)
  2: 0.5rem   (8px)
  3: 1rem     (16px)
  4: 1.5rem   (24px)
  5: 3rem     (48px)
```

### Display Utilities
```yaml
display:
  visibility:
    - d-none           # Hide
    - d-block          # Display block
    - d-inline         # Display inline
    - d-flex           # Display flex
    - d-grid           # Display grid

  responsive_visibility:
    - d-none d-md-block      # Hide on mobile, show on tablet+
    - d-block d-lg-none      # Show on mobile, hide on desktop
    - d-md-flex              # Flex only on tablet+

usage_patterns:
  mobile_only: "d-block d-lg-none"
  desktop_only: "d-none d-lg-block"
  hide_on_mobile: "d-none d-md-block"
```

### Flexbox Utilities
```yaml
flex:
  direction:
    - flex-row         # Horizontal (default)
    - flex-column      # Vertical
    - flex-row-reverse
    - flex-column-reverse

  justify:
    - justify-content-start
    - justify-content-center
    - justify-content-end
    - justify-content-between
    - justify-content-around

  align:
    - align-items-start
    - align-items-center
    - align-items-end
    - align-items-stretch

  wrap:
    - flex-wrap
    - flex-nowrap

  gap:
    - gap-2, gap-3, gap-4  # Space between flex items

usage_patterns:
  center_content: "d-flex justify-content-center align-items-center"
  button_row: "d-flex flex-wrap gap-3"
  mobile_stack_desktop_row: "d-flex flex-column flex-md-row gap-3"
```

### Text Utilities
```yaml
text:
  alignment:
    - text-start       # Left in LTR
    - text-center
    - text-end         # Right in LTR
    - text-md-start    # Responsive alignment

  colors:
    - text-primary
    - text-secondary
    - text-muted       # Gray
    - text-white
    - text-dark

  sizing:
    - fs-1 through fs-6    # Font sizes
    - small               # Smaller text
    - lead                # Larger intro text

  weight:
    - fw-light
    - fw-normal
    - fw-bold
    - fw-bolder

  decoration:
    - text-decoration-none  # Remove underline from links

usage_patterns:
  muted_disclaimer: "small text-muted"
  hero_headline: "display-4 fw-bold"
  subhead: "lead text-muted"
```

### Background & Border Utilities
```yaml
backgrounds:
  colors:
    - bg-primary
    - bg-secondary
    - bg-light         # Very light gray
    - bg-white
    - bg-warning
    - bg-danger

  opacity:
    - bg-opacity-10    # 10% opacity
    - bg-opacity-25
    - bg-opacity-50
    - bg-opacity-75

borders:
  sides:
    - border           # All sides
    - border-top
    - border-bottom
    - border-start
    - border-end

  colors:
    - border-primary
    - border-warning
    - border-danger

  width:
    - border-0         # No border
    - border-1 through border-5

  radius:
    - rounded          # 4px corners
    - rounded-circle   # Fully round
    - rounded-pill     # Pill shape

usage_patterns:
  safety_alert: "bg-warning bg-opacity-10 border-start border-warning border-5"
  card: "bg-white rounded shadow"
```

### Custom Classes

Define these in your project CSS:

```css
/* Gradient backgrounds */
.bg-gradient-light {
  background: linear-gradient(135deg, #f8f9fa 0%, #e9ecef 100%);
}

.bg-gradient-primary {
  background: linear-gradient(135deg, var(--bs-primary) 0%, var(--bs-primary-dark) 100%);
}

/* Custom button hover states */
.btn-danger:hover {
  background-color: #bb2d3b;
  transform: translateY(-1px);
  box-shadow: 0 4px 8px rgba(0,0,0,0.15);
}

/* Fixed mobile CTA */
.sticky-cta-mobile {
  position: fixed;
  bottom: 0;
  left: 0;
  right: 0;
  z-index: 1030;
  background: white;
  box-shadow: 0 -2px 10px rgba(0,0,0,0.1);
}

/* Card hover effects */
.card-hover {
  transition: transform 0.2s, box-shadow 0.2s;
}

.card-hover:hover {
  transform: translateY(-4px);
  box-shadow: 0 8px 16px rgba(0,0,0,0.1);
}
```

## Complete Page Structure Example

See `references/examples/` for full page implementations. Basic structure:

```yaml
page:
  meta:
    title: "Emergency Heater Repair McKinney TX | ABC Heating"
    description: "24/7 emergency heater repair in McKinney..."
    niche: hvac
    intent: fix_now
    urgency: emergency

  rows:
    - id: hero
      container: standard
      layout: asymmetric
      classes: ["py-5", "bg-light"]
      blocks:
        - type: HERO
          column: {xs: 12, lg: 7}
          order: {xs: 1, lg: 1}
        - type: SHORT_FORM
          column: {xs: 12, lg: 5}
          order: {xs: 2, lg: 2}

    - id: safety
      container: fluid
      layout: single_column
      classes: ["py-4", "bg-warning", "bg-opacity-10", "border-start", "border-warning", "border-5"]
      blocks:
        - type: SAFETY_NOTICE
          column: {xs: 12}

    # ... additional rows
```

This is the core layout methodology. For specific block content models and conditional logic, see block-catalog.md. For complete examples, see references/examples/.