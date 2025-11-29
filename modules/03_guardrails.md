Change Log (2025-11-29):
– Confirmed default strict_evidence_mode=true; added explicit WARNING templates for unsupported claims and missing/short sections.

### Module 3 — Guardrails (internal)

**Goal:** Catch problems early (missing/short sections, hallucinations) and enforce strict evidence rules.

**Inputs from Module 2:** sections_summaries[], config

**Modes:**
- strict_evidence_mode: true/false (default: true)
  - When true: every claim in summaries must be traceable to the provided text.
  - If not traceable → add a WARNING and move the claim to notes, not to the main bullets.

**Checks (run for each section entry):**
1) Missing / Short
   - If section status=MISSING → add WARNING: "Section missing (no content provided)."
   - If section status=SHORT → add NOTE: "Section unusually short; limited summarization."

2) Hallucination & Unsupported Claims
   - Scan bullets for numbers, named entities, references.
   - If not present in source text → move to notes[], add WARNING: "Possible unsupported claim; needs citation or remove."

3) Consistency & Duplicates
   - If two sections repeat the same point verbatim → keep in the more relevant section; add NOTE in the other: "Duplicate content trimmed."

4) Length Controls
   - If summary_bullets > 10 in detailed mode → trim to 10, add NOTE: "Trimmed for readability."
   - If short mode and bullets > 5 → trim to 5.

5) Long Paper Chunking (if provided as large text blob)
   - If any single section > ~1200 words → mark chunking_required=true for that section; add NOTE: "Chunking recommended."

**Outputs:**
- sections_summaries_clean[]: cleaned/trimmed bullets and notes
- flags_global[]: any cross-section warnings found
- config: unchanged (plus strict_evidence_mode carried through)
