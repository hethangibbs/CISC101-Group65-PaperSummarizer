### Module 4 — Rendering & Refinement (internal)

**Goal:** Assemble the final user-facing output with consistent formatting and two audience variants.

**Inputs:** sections_summaries_clean[], flags_global[], config {audience, min_words_per_section, strict_evidence_mode?, summary_level?}

**Assemble Outputs (in this order):**
1) Paper Summary
   - 4–6 bullet overview of the whole paper (problem, method, key results, limits, takeaway).
   - No unsupported claims; if unsure → move to Checks & Warnings.

2) Section-by-Section Table
   - Columns: Section | 3–6 bullets | Notes/Flags
   - Use sections_summaries_clean[]. Merge any per-section NOTES/WARNINGS into the last column.

3) Expert Summary + Lay Summary
   - Expert: method details, assumptions, limits, key numbers.
   - Lay: plain language, what it means, why it matters.
   - Keep both concise (≤150 words each unless summary_level=detailed).

4) Mini-Glossary
   - 5–10 key terms: **Term:** short, plain-language definition.
   - Only terms appearing in the paper.

5) Checks & Warnings
   - List items from flags_global[] and any per-section WARNINGs.
   - Include strict_evidence_mode notes: “Unsupported claims moved to notes.”

**Formatting Rules:**
- Use Markdown headings and short bullet lists.
- No internal labels (modules, flags variable names) in the final text.
- Keep tone consistent with system_prompt.md (clear, supportive, no jargon overload).

**Output (final payload):**
- Paper Summary
- Section-by-Section Table
- Expert Summary
- Lay Summary
- Mini-Glossary
- Checks & Warnings
