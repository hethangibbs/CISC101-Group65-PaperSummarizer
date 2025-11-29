### Module 2 — Section Loop (internal)

**Goal:** For each section, create a faithful summary that meets constraints and fits the audience.

**Inputs from Module 1:** {sections[], config, notes}
- sections[]: normalized list with {name, text?, status, word_count}
- config: {audience, min_words_per_section=50, summary_level?}

**Controls:**
- summary_level (optional): "short" (~3–5 bullets) or "detailed" (~6–10 bullets + 2–3 sentences).

**Per-Section Steps:**
1) If status=MISSING → write: “Section missing (no content provided).”
2) Else if status=SHORT (<50 words) → write: “Section is very short; summarization may be limited.”
3) Summarize faithfully:
   - Extract the core claim, method, evidence, and key numbers if present.
   - Avoid speculation; no invented citations, figures, or equations.
4) Audience fit:
   - expert → allow domain terms; focus on methods/results limits.
   - lay/student → plain language; define terms briefly.
5) Apply summary_level:
   - short → 3–5 bullets max.
   - detailed → 6–10 bullets + 2–3 connective sentences.
6) Store structured output for this section:
   - {name, summary_bullets[], notes[], flags[]}

**Output to next module:**  
sections_summaries[] with structured entries for each section.
