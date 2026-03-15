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
