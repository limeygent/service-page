### FAQ
**Purpose**: Remove objections before contact
**When**: Always
**Placement**: Late-mid, before FINAL_CTA

**Content Model**:
```yaml
FAQ:
  intro_text:
    example: "We know choosing a contractor brings up questions. Here are the most common concerns we hear, answered honestly."

  questions:
    min_count: 5
    max_count: 10
    prioritization: "Match top_objections order"
    structure:
      - question: string (natural language)
        answer: string (150-300 chars, specific)
        intent_category: [price, trust, speed, insurance, warranty, process]

    examples:
      price:
        q: "How much does heater repair cost?"
        a: "Most repairs $200-800. We charge $89 diagnostic (waived with repair) and give exact pricing before starting work. If we can't fix it, you pay nothing."

      trust:
        q: "Should I repair my 12-year-old heater?"
        a: "Depends on repair cost. Under $500? Usually worth it. Over $1,000? Might replace. We'll walk you through the math with no pressure either way."

  html_pattern:
    default: "details_element"

    details_element:
      note: "Default. Simpler, more accessible, works without Bootstrap JS."
      pattern: |
        <details class="faq-item border rounded mb-3 p-3">
          <summary>
            <h3 class="d-inline h6 fw-bold mb-0">Question text here?</h3>
          </summary>
          <div class="faq-body pt-2">
            <p>Answer text here.</p>
          </div>
        </details>
      when_to_use: "WordPress embeds, standalone pages, non-Bootstrap JS contexts"

    bootstrap_accordion:
      note: "Alternative for pages already loading Bootstrap JS."
      when_to_use: "Full Bootstrap pages with other accordion/collapse components"

  structured_data:
    required: true
    type: "FAQPage"
    format: "JSON-LD"
    placement: "After the FAQ section"
    pattern: |
      <script type="application/ld+json">
      {
        "@context": "https://schema.org",
        "@type": "FAQPage",
        "mainEntity": [
          {
            "@type": "Question",
            "name": "Question text here?",
            "acceptedAnswer": {
              "@type": "Answer",
              "text": "Answer text here."
            }
          }
        ]
      }
      </script>
    note: "Generate one Question entry per FAQ item. Strip HTML from answer text in schema."

meclabs_contribution:
  reduces: [friction_2x, anxiety_2x]
```
