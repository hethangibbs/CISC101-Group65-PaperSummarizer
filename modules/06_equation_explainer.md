### Module 6 — Equation Explainer (internal)

**Goal:** Detect equations and give short, plain-language explanations for each.

**Inputs:** paper text (full or per-section), sections_summaries_clean[]

**Detect:**
- Inline math like: E = mc^2, y = mx + b, p < 0.05
- LaTeX blocks: $...$, $$...$$, \[...\], \(...\)

**For each equation found:**
1) Capture the raw equation string.
2) Identify variables/symbols that appear (e.g., E, m, c).
3) Draft plain-language meaning (1–2 lines): what the equation shows and how it’s used here.
4) If any symbol seems undefined in the paper → add NOTE: "Symbol not defined in text."

**Output object:**
- equations[]: {raw, variables:[...], meaning, notes?}

**Pass to Module 4 (optional appendix / glossary support):**
- Provide short entries the renderer can place after the glossary, or fold key symbols into the glossary if appropriate.
