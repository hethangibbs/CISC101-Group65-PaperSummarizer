### Module 1 — Intake & Setup (internal)

**Goal:** Normalize inputs and prepare clean metadata so later modules are predictable.

**Inputs:**
- Paper text (full or sectioned)
- Section list (given or inferred)
- Audience (expert / lay / student)

**Actions:**
1) Normalize section names  
   - Map synonyms (e.g., Background → Introduction; Findings → Results).
   - Trim whitespace, remove duplicates, keep canonical order.

2) Detect missing or too-short sections  
   - If a required section is missing → add a placeholder with status=MISSING.
   - If a section has <50 words → mark status=SHORT.

3) Build metadata  
   - For each section: {name, start_index, end_index, word_count, status}.
   - Store global settings: {audience, min_words_per_section=50}.

4) Prep handoff object (JSON-like)  
   - sections[]: list of normalized sections with status
   - config: audience, thresholds
   - notes: any anomalies (e.g., duplicated sections, odd ordering)

**Output to next module:**  
A structured object: {sections[], config, notes}
