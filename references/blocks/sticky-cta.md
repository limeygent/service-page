### STICKY_CTA
**When**: `device_mobile_pct >= 40`
**Where**: Fixed bottom on mobile

**Content Model**:
```yaml
STICKY_CTA:
  buttons:
    - "Call Now" (tel: link)
    - "Text Us" (sms: link) (if has_sms)
  classes: ["fixed-bottom", "d-lg-none", "p-3", "bg-white", "shadow"]
```
