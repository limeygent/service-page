### MAP_CONTACT
**When**: Always recommended
**Where**: Late-page, before or after FAQ
**Purpose**: Business location, hours, phone, and service area zip codes

**Content Model**:
```yaml
MAP_CONTACT:
  address: string
  phone: string
  hours: string
  zip_codes: array (optional)
  map_embed: optional (suppress for emergency pages, use SERVICE_AREAS_LIST instead)

  layout:
    desktop: "col-lg-6 map + col-lg-6 contact info"
    mobile: "stacked (contact info first)"

meclabs_contribution:
  reduces: [friction_2x (easy to find), anxiety_2x (real physical location)]
```
