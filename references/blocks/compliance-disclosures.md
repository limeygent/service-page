### COMPLIANCE_DISCLOSURES
**When**: `regulated == true` AND `niche in ['dental', 'medical', 'pediatric_medical', 'personal_injury', 'financial']`
**Where**: Footer area or adjacent to relevant content
**Purpose**: Regulatory disclosures, disclaimers, license numbers

**Content Model**:
```yaml
COMPLIANCE_DISCLOSURES:
  disclosures:
    medical: "Individual results may vary. Consult your healthcare provider."
    legal: "Past results do not guarantee future outcomes. Every case is different."
    financial: "APR depends on creditworthiness. See terms for details."
    dental_ahpra: "This is a general dental practice. [Practitioner] is a registered general dentist (registration number)."

  note: |
    Only include disclosures relevant to the specific niche and jurisdiction.
    AHPRA disclosures apply ONLY to Australian dental/medical practices.
    HIPAA notices apply ONLY to US medical practices.
    Do NOT apply medical/legal disclaimers to home services or other non-regulated niches.

  placement: "Adjacent to testimonials, pricing, or at page footer"
  classes: ["small", "text-muted"]
```
