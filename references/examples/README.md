# HTML Page Skeleton

Use this skeleton when generating Bootstrap 5 HTML output. This resolves the document structure, CDN links, CSS variable pattern, and JSON-LD placement.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>[Service] [City], [State] | [Business Name]</title>
  <meta name="description" content="[150-160 char meta description]">
  <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/css/bootstrap.min.css" rel="stylesheet">
  <link href="https://cdn.jsdelivr.net/npm/bootstrap-icons@1.11.3/font/bootstrap-icons.min.css" rel="stylesheet">
</head>
<body>

<style>
  :root {
    --brand-primary: #[brand-hex];
    --brand-primary-dark: #[darker-variant];
    --brand-primary-light: rgba([r], [g], [b], 0.1);
    --brand-accent: #[accent-hex];
    --brand-dark: #[dark-text];
    --brand-light: #[light-bg];
  }
  /* Custom button classes using brand colors */
  .btn-brand { background: var(--brand-primary); border-color: var(--brand-primary); color: #fff; font-weight: 600; }
  .btn-brand:hover { background: var(--brand-primary-dark); color: #fff; transform: translateY(-1px); box-shadow: 0 4px 8px rgba(0,0,0,0.15); }
  .btn-brand-outline { border: 2px solid var(--brand-primary); color: var(--brand-primary-dark); font-weight: 600; }
  .btn-brand-outline:hover { background: var(--brand-primary); color: #fff; }
  /* Utility classes */
  .zone-group { scroll-margin-top: 80px; }
  .step-number { width: 36px; height: 36px; border-radius: 50%; background: var(--brand-primary); color: #fff; display: inline-flex; align-items: center; justify-content: center; font-weight: 700; }
  .card-hover { transition: transform 0.2s, box-shadow 0.2s; border: none; }
  .card-hover:hover { transform: translateY(-3px); box-shadow: 0 8px 25px rgba(0,0,0,0.1); }
  .sticky-cta-mobile { position: fixed; bottom: 0; left: 0; right: 0; z-index: 1050; background: #fff; box-shadow: 0 -4px 12px rgba(0,0,0,0.1); }
  @media (min-width: 992px) { .sticky-cta-mobile { display: none !important; } }
</style>

<!-- HERO -->
<section id="hero" class="zone-group py-5" style="background: linear-gradient(...);">
  <div class="container">
    <div class="row align-items-center g-4">
      <div class="col-12 col-lg-7">
        <!-- H1, badges, explanation text, CTAs -->
      </div>
      <div class="col-12 col-lg-5">
        <!-- SHORT_FORM card or urgency checklist -->
      </div>
    </div>
  </div>
</section>

<!-- Each subsequent block follows this pattern: -->
<section id="[block-id]" class="zone-group py-5 [bg-light if alternating]">
  <div class="container">
    <h2 class="fw-bold mb-4">[Block Title]</h2>
    <!-- Block content using Bootstrap grid -->
  </div>
</section>

<!-- FAQ with JSON-LD (place script in the section, not in head) -->
<section id="faq" class="zone-group py-5">
  <div class="container" style="max-width: 800px;">
    <h2 class="fw-bold mb-4">[FAQ Title]</h2>
    <!-- details/summary elements -->
    <details class="mb-3 border-bottom pb-3">
      <summary class="fw-semibold" style="cursor: pointer;">[Question]</summary>
      <div class="mt-2 text-muted">[Answer]</div>
    </details>
  </div>
  <script type="application/ld+json">
  {
    "@context": "https://schema.org",
    "@type": "FAQPage",
    "mainEntity": [
      { "@type": "Question", "name": "...", "acceptedAnswer": { "@type": "Answer", "text": "..." } }
    ]
  }
  </script>
</section>

<!-- STICKY MOBILE CTA (outside all sections, before closing body) -->
<div class="sticky-cta-mobile d-lg-none p-3">
  <div class="d-flex gap-2">
    <a href="tel:[phone]" class="btn btn-brand w-50">Call Now</a>
    <a href="sms:[phone]" class="btn btn-brand-outline w-50">Text Us</a>
  </div>
</div>

<!-- Add bottom padding for sticky CTA clearance on mobile -->
<div class="d-lg-none" style="height: 80px;"></div>

<script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/js/bootstrap.bundle.min.js"></script>
</body>
</html>
```

## Archived Examples

Full YAML page examples (emergency HVAC, dental implants, pediatric ear infection) are in `archive/examples/` for reference but are not needed for page generation.
