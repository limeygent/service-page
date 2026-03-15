### PRIMARY_CTAS
**Purpose**: Repeat core actions at decision points
**When**: Always
**Placement**: After PROCESS_TIMELINE, before FAQ, pre-FINAL_CTA

**Content Model**:
```yaml
PRIMARY_CTAS:
  instances: multiple (3-4 per page)
  structure:
    heading: string (must vary per instance - see Progressive CTA System)
    buttons:
      - call
      - schedule
      - form
    subtext: optional reinforcement

  progressive_cta_note: |
    Each PRIMARY_CTAS instance MUST use different heading text matching
    its position in the Progressive CTA System (see table above).
    Static "Ready to Get Started?" at every instance is acceptable as
    a fallback, but progressive text is strongly recommended.

    Example progression:
      Instance 1 (after services): "Schedule Your [Specific Service] Visit"
      Instance 2 (after reviews): "No Obligation, Honest Advice"
      Instance 3 (pre-FAQ): "Join [X]+ [City] Families Who Trust Us"
```
