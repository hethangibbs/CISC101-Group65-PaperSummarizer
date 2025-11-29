### Module 5 — Citation Extractor (internal)

**Goal:** Collect explicit citations/references from the paper and flag issues.

**Inputs:** paper text (full or per-section), sections_summaries_clean[]

**Steps:**
1) Scan for citation patterns:
   - Bracketed styles: [12], [3–5], (Smith, 2021), (Smith & Lee, 2020).
   - Reference list headers: “References”, “Bibliography”, “Works Cited”.
2) Extract entries:
   - Build citations[] with raw strings + guessed fields {authors?, year?, title?}.
3) Cross-check:
   - If a section mentions a citation number/name not in citations[] → add WARNING: "In-text citation not found in reference list."
   - If a reference appears but is never cited → add NOTE: "Uncited reference."
4) Completeness:
   - If any entry is missing author/year/title → add WARNING on that entry: "Incomplete reference."
5) Output object:
   - citations[] (parsed best-effort)
   - citation_flags[] (warnings/notes)

**Output to Module 4 (merge into Checks & Warnings):**
- Attach citation_flags[] to flags_global[].
- Provide citations[] for optional appendix, if requested.
