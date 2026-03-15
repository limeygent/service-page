### SERVICE_AREAS_LIST
**When**: `service_area_complexity != 'single_city'` OR `urgency in ['emergency', 'soon']`
**Where**: After OPERATIONS (ops_row) OR before PRIMARY_CTAS
**Priority**: **MEDIUM - 10% bounce reduction**

**Why separate from SERVICE_AREA (map):**
Emergency buyers need fast text confirmation ("Do they serve me?"), not interactive maps. List with checkmarks answers question in 2 seconds.

**Content Model**:
```yaml
SERVICE_AREAS_LIST:
  heading: "24/7 Emergency Service Throughout [Region]"
  intro: "Fast emergency [service] serving:"

  cities:
    min_count: 6
    max_count: 12
    display: "Grid with check-circle icons"
    icon: "bi-check-circle text-success"

    layout:
      desktop: 3 columns (col-md-4)
      mobile: 2 columns (col-6)

    examples:
      - McKinney
      - Frisco
      - Plano
      - Allen
      - Prosper
      - Celina
      - "+ View all areas" (link)

  sidebar:
    heading: "Not sure if we cover your area?"
    text: "We often serve surrounding communities too. Call us to confirm coverage for your location."
    cta:
      text: "Call Now"
      variant: btn-sm btn-outline-danger

    styling:
      background: "rgba(2, 33, 105, 0.05)"
      border: "1px solid rgba(2, 33, 105, 0.1)"
      layout: col-lg-4

meclabs_contribution:
  reduces: [friction_2x (geographic certainty), anxiety_2x (coverage confirmed)]

performance_data:
  bounce_reduction: "10%"
  time_to_conversion: "Faster (removes ambiguity)"
```
