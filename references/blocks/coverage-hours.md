### COVERAGE_HOURS
**When**: `urgency != 'planning'`
**Where**: ops_row (pair with SERVICE_AREA)

**Content Model**:
```yaml
COVERAGE_HOURS:
  regular: "7am-8pm Mon-Sat"
  emergency: "24/7 for no-heat emergencies"
  timezone: auto-detect
  current_status: "Open Now" or "Closed • Opens at 7am"
```
