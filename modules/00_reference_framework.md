# Paper Summarizer — Internal Reference Framework (PS3)

**Internal only.** This framework defines how the system works behind the scenes. Users should never see these labels or internal notes. The goal is to keep behavior predictable, modular, and easy to update.

## Overview
The summarizer runs in four core modules plus student-created extensions. Each module has a clear job and passes structured data to the next one. This lets us change one part without breaking the others.

## Core Modules (names only here)
- **Module 1: Intake & Setup** — normalize section names, detect missing/short sections, prep metadata.
- **Module 2: Section Loop** — for each section: summarize faithfully, apply constraints, store outputs.
- **Module 3: Guardrails** — handle missing/empty or <50-word sections, mitigate hallucinations, chunk long papers.
- **Module 4: Rendering & Refinement** — assemble final structure, format consistently, produce expert + lay variants.

## Student-Created Extensions (for later files)
- **Citation Extractor** — collect explicit citations and flag missing/incomplete references.
- **Equation Explainer** — find equations and add plain-language explanations.

> Implementation note: Keep internal names consistent across files. Do not expose internal labels or notes to users in the final output.
