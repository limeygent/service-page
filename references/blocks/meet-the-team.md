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
