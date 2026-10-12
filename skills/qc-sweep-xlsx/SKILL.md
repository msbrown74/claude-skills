---
name: "qc-sweep-xlsx"
description: "Runs a rigorous 12-step quality-control review of an EXISTING spreadsheet/workbook (.xlsx, .xlsm, .xltx, .csv) and returns a numbered, selectable fix menu — every issue classified Critical, Major, or Minor and paired with a proposed fix (lettered when a fix has options) that the user picks by number to apply. Covers hidden artifacts (hidden sheets/rows/columns, filters, comments, defined names, stale links), structure/layout, rendering QA, formula/value accuracy, completeness, data integrity and input controls, clarity, label/note grammar and style, cell/sheet dependency validation, external links and data sources, and a final compliance read-through. Use for \"run a QC sweep on this workbook/spreadsheet\", \"QC this spreadsheet\", \"quality check this Excel file\", \"audit this model\", or \"run the 12-step spreadsheet review\". Do NOT use to build a new spreadsheet (use xlsx), to summarize its contents (answer directly), or to QC a Word/PDF/PPT document (use qc-sweep)."
---

# QC-Sweep-XLSX

A disciplined 12-step quality-control review for finished or near-finished
spreadsheets and workbooks. It produces a **numbered menu of findings** — every
issue located, explained, classified by severity, and paired with a proposed
fix — then applies exactly the fixes the user selects by number. It never
rewrites the workbook on its own.

## When to Use
- The user has a built workbook (financial model, tracker, calculator, data
  extract, report workbook) and wants it checked before it ships, is signed
  off, or goes to a client/regulator/internal stakeholder.
- The user says "QC", "quality check", "audit this model", "review for
  quality", "proofread and check this spreadsheet", or names the 12-step sweep.
- A technical deliverable built in Excel (engineering calc sheet, cost
  estimate, capacity model, water/wastewater design spreadsheet) needs a
  structured pre-delivery review.

## When NOT to Use
- **Creating or building** a new spreadsheet from scratch — use xlsx instead.
- **Summarizing** what a workbook contains, or answering a question about its
  data → answer directly (or use data-analysis); no QC report needed.
- **QCing a Word/PDF/PowerPoint document** — use qc-sweep instead.
- **Applying** the fixes (rather than finding them) → only after the user
  reviews this report and explicitly asks; QC is a read-and-report pass.

## Quick Start
```
User: "Run a QC sweep on this workbook"  (file in input/)
1. Locate the file (Glob input/**/*); open it with the xlsx skill.
2. STEP 1 — Set context: confirm workbook type, purpose, audience, risk tier,
   platform, and feature scope (formulas, PivotTables, Power Query, macros/VBA,
   external links). If unclear, ASK. If still none, infer, state the
   assumption, and confirm before enforcing.
3. STEPS 2-12 — Work the sweep in order, recording findings with severity.
4. Present a NUMBERED fix menu: Critical → Major → Minor, each issue paired
   with a proposed fix (letter the options — 4A/4B/4C — when a fix has
   alternatives).
5. The user replies with the numbers/letters to apply; apply only those,
   re-run rendering QA (Step 12), save the revised file, and loop if they want
   another round.
```

## Core Instructions

### Step 0 — Locate and load the workbook
- Find the file in `input/` first (`Glob input/**/*`); also check `grounding/`.
  If the message has an `<attached_files>` block, read those paths directly.
- Open and inspect it with the `xlsx` skill so formulas, defined names, hidden
  sheets/rows/columns, comments, and data validation rules are all visible —
  not just displayed values.
- If no file is found, say so plainly and ask the user to attach it. Never QC
  a workbook you could not read; never invent its contents.

### Step 1 — Set context (GATE — do this before any checking)
Identify and record: **workbook type, purpose, intended audience, risk tier,
platform, and feature scope** (formulas, PivotTables, Power Query, macros/VBA,
external links) and any applicable standard (a project spec, firm template, or
industry convention). Every later check is judged against these.
- **If any of these — especially risk tier or feature scope — is unclear or
  missing, STOP and ask the user** before proceeding.
- If, after asking, none is provided, you MAY infer a likely context from
  domain cues (including the user's profession). You **must** state the
  inferred context explicitly as an assumption and **confirm it with the user
  before enforcing it.**

### Step 2 — Remove hidden artifacts FIRST
Before any other review, detect and flag: hidden worksheets, hidden rows or
columns, active filters, comments/annotations, defined names, embedded
objects, workbook/document metadata, stale external links, and any
collaboration or version-control artifacts (e.g. leftover "v2", "OLD",
"DELETE ME" tabs). These come first because they distort every downstream
check.

### Step 3 — Structure and organization
Verify worksheet naming, ranges, tables, and layout are consistent and
logically organized; confirm inputs, calculations, and outputs are separated
and clearly labeled as such; flag redundant, conflicting, or incomplete
elements.

### Step 4 — Visual rendering QA (initial pass)
Review the workbook in its intended viewing state (open/screenshot the actual
tabs) and verify layout integrity: column widths, alignment, formatting
consistency, table usage, visibility of key inputs/outputs, and visual
artifacts not apparent from raw formulas or values alone.

### Step 5 — Content accuracy
Check that formulas, values, assumptions, and stated information are
internally consistent. Identify contradictions, errors, or unsupported
assumptions, and confirm calculations reflect the intended logic.

### Step 6 — Completeness
Confirm all required inputs, calculations, outputs, and supporting elements
are present and fully developed. Flag missing data, broken logic chains,
unexplained gaps, or unresolved placeholders unless explicitly intentional.

### Step 7 — Data integrity and controls
Ensure inputs are valid, appropriately constrained, and clearly separated from
calculated values; confirm data types/formats are consistent; check that data
validation rules or sheet/workbook protections are applied where needed to
prevent invalid or inconsistent inputs.

### Step 8 — Clarity and audience fit
Ensure the workbook matches the defined audience, follows a logical flow,
clearly labels assumptions/inputs/outputs, introduces concepts before use, and
communicates calculations and results in an understandable, usable manner.

### Step 9 — Grammar, spelling, and style
Flag grammar, spelling, tone, consistency, and readability issues in any
user-visible text — labels, headers, notes, assumptions, and instructions.
Prefer clear, direct, concise phrasing.

### Step 10 — Validate data and dependencies
Confirm calculations correctly reference the intended inputs; verify
dependencies between cells, sheets, and ranges are accurate and complete; flag
any unintended or hidden dependencies; confirm tables, charts, PivotTables,
and summaries accurately reflect the underlying data.

### Step 11 — External links and sources
Verify all links, connections, and referenced files are valid, current, and
appropriate. Confirm data sources are identifiable and consistent with the
outputs derived from them, and flag any broken or unintended external
dependencies (linked workbooks, Power Query connections, ODBC/database
sources).

### Step 12 — Visual rendering QA (post-edit recheck) and final read-through
If revisions were made after Step 4, **re-review** and verify no layout or
visibility issues were introduced: formatting drift, hidden elements changing
state, or misalignment. Then do a final read-through: confirm the workbook
meets all requirements for purpose, structure, and integrity, and evaluate it
from the intended user's perspective to judge whether it can be confidently
used without introducing risk.

## Severity Classification (apply to EVERY finding)
Tag each finding exactly one level:
- **Critical** — blocks delivery: formula/value errors, broken or circular
  references, missing required inputs/outputs, unresolved placeholders,
  unprotected inputs that invite corruption, or anything that would mislead
  the user of the workbook.
- **Major** — significant quality problem that should be fixed before
  delivery: structural inconsistency, unsupported assumptions, broken
  dependency chains, rendering breakage, audience mismatch, missing data
  validation on a key input.
- **Minor** — polish: wording, tone, cosmetic formatting, non-blocking style
  nits.

## Output — a numbered, selectable fix menu
Present findings as an **actionable menu the user can choose from**, not a
static report. **Always render the numbered fix options list inline** so the
user can select from it — it is never hidden inside a file. What accompanies
it inline, and whether a file is saved, depends on the QC report's length
(rule of thumb: treat it as long once the list runs past ~10-12 findings or
the detail won't sit comfortably in a chat reply):

- **Short report** → render the whole thing inline as markdown — header,
  severity summary, and the numbered fix options list. Save no file.
- **Long report** → render inline a **concise summary** (header + severity
  summary) followed by the **full numbered fix options list**, THEN save the
  complete, detailed report (every finding with its location — sheet!cell or
  range — evidence, and fix rationale) as a Markdown file in `output/`, named
  `<original_workbook>-QC-<YYYY-MM-DD>-<HHMM>.md` from the user's local date
  and time (filename-safe, no colons). Glob-confirm the file exists before
  telling the user where it is.

Whether shown inline or written to the saved file, use this structure:
1. **Header** — workbook name, type, audience, risk tier, platform, and
   feature scope (note "assumed, confirmed" if inferred).
2. **Severity summary** — counts of Critical / Major / Minor and an overall
   **go / no-go** verdict.
3. **Numbered findings (the fix options list)** — ONE continuously numbered
   list (1, 2, 3 …) running through the severity groups in order: **Critical
   first, then Major, then Minor.** Number every issue uniquely (never restart
   numbering inside a group) so each can be selected. Format each entry as:
   `N. [SEVERITY] Sheet!Location — the issue → proposed fix`
   - **When a finding has more than one reasonable fix, letter the options**
     under that number — `4A`, `4B`, `4C` — each a distinct, self-contained
     alternative (e.g. 4A correct the formula, 4B add a data-validation rule,
     4C flag the cell for manual review). The user picks at most one letter
     for that finding.
4. **Selection prompt** — tell the user exactly how to choose: reply with the
   numbers they want applied, adding a letter for any lettered finding — e.g.
   `1, 3, 4B, 7`. Also accept ranges (`1-5`), `all`, `all critical`, or `none`.

## Applying the selected fixes (selection loop)
After the user replies with their selection:
1. Map each chosen number to its finding; for a lettered finding, apply only
   the chosen option. Ignore every finding the user did not select.
2. Apply the fixes with the `xlsx` skill. Change only what the selected fixes
   specify — nothing else (don't "clean up" unrelated cells or formatting).
3. Re-run **Step 12 (visual rendering QA + final read-through)** and re-verify
   the edited formulas/ranges so no fix introduced a new problem (broken
   reference, formatting drift, validation gap).
4. Save the revised workbook to `output/` under a new name (e.g.
   `<original>-QC-revised.xlsx`); never overwrite the user's original.
5. Report back: which numbered fixes were applied, which were skipped, and any
   new issue the recheck found — re-listed in the same numbered format so the
   user can run another selection round.

## Guardrails
- **Context gate (Step 1) is mandatory.** If workbook type/purpose/
  audience/risk/feature scope is unclear, ask before reviewing. An inferred
  context must be stated as an assumption and confirmed before it is enforced.
- **Protect sensitive content.** If the workbook contains PII, credentials,
  pricing, or confidential data, never reproduce it verbatim in the findings
  report — reference it by sheet/cell location instead, and respect the
  workbook's privacy.
- **Every finding gets a severity.** No unclassified issues; always classify.
- **Never fabricate.** Do not invent the workbook's contents, formulas, or
  values. If a file cannot be read, say so and ask for a re-attach — never
  substitute sample or placeholder content.
- **Apply only what the user selects.** Present the numbered fix menu and
  wait; edit the workbook only for the findings (and lettered options) the
  user picks. Never apply an unselected fix, and never auto-rewrite the whole
  workbook.
- **Preserve the original.** Save revisions as a new file in `output/`; never
  overwrite the user's uploaded workbook, and re-run rendering QA after
  applying fixes.
- **Order matters.** Remove hidden artifacts (Step 2) before other checks, and
  re-run rendering QA (Step 12) after any revisions.
