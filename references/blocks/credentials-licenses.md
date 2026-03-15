### CREDENTIALS_LICENSES
**When**: `regulatory_disclosures_required == true` OR `niche in ['hvac','plumbing','roofing','dental','financial','personal_injury']`
**Where**: Near REVIEWS_SNAPSHOT, trust_row

**Content Model**:
```yaml
CREDENTIALS_LICENSES:
  licenses: ["TACLB00024715E", "EPA Certified"]
  certifications: ["NATE Certified", "BBB A+ Rating"]
  display: badges or list

meclabs_contribution:
  reduces: [anxiety_2x (legitimacy)]
```
