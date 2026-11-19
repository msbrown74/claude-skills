---
name: "qc-sweep"
description: "Runs a rigorous 12-step quality-control review of an EXISTING document (reports, specs, proposals, memos, technical deliverables, letters) and returns a tabulated, selectable fix menu — every issue classified Critical, Major, or Minor, given a reason, and paired with a proposed fix (lettered when a fix has options) that the user picks by ID to apply. Covers editing artifacts, structure/formatting, cross-references and numbering, defined terms, content accuracy, completeness, clarity, grammar/style, data and visuals, citations (with mandatory external verification), visual rendering QA, and final compliance. Use when the user asks to \"run a QC sweep\", \"QC this document\", \"quality check this report\", \"review this document for quality\", \"do a document QC review\", \"proofread and quality-check this\", or \"run the 12-step review\". Do NOT use to CREATE or write a new document (use docx / pdf / pptx), to summarize a document's content (answer directly), or to review source code (use code-review)."
---

# QC-Sweep

A disciplined 12-step quality-control review for finished or near-finished
documents. It produces a **tabulated menu of findings** — every issue located,
classified by severity, explained, and paired with a proposed fix — then applies
exactly the fixes the user selects by ID. It never rewrites the document on
its own.

## When to Use
- The user has a drafted document and wants it checked before it ships, is
  signed, is submitted, or goes to a client/regulator.
- The user says "QC", "quality check", "review for quality", "proofread and
  check", or names the 12-step sweep.
- A technical deliverable (engineering report, spec, water-resources study,
  proposal) needs a structured pre-delivery review.

## When NOT to Use
- **Creating or writing** a new document — use docx instead (use pdf for a PDF,
  pptx for slides).
- **Summarizing** what a document says, or answering a question about it →
  answer directly; no QC report needed.
- **Reviewing source code** — use code-review instead.
- **Applying** the fixes (rather than finding them) → only after the user
  reviews this report and explicitly asks; QC is a read-and-report pass.

## Quick Start
```
User: "Run a QC sweep on this report"  (file in input/)
1. Locate the file (Glob input/**/*); read it with the right reader (docx/pdf/Read).
2. STEP 1 — Set context: confirm doc type, purpose, audience, risk tier, and the
   formatting/citation standard. If the standard is unclear, ASK. If still none,
   infer one, state it as an assumption, and confirm before enforcing.
3. STEPS 2-12 — Work the sweep in order, recording findings with severity.
4. Present a TABULATED fix menu with severity-prefixed IDs (C1, C2… M1, M2… N1, N2…):
   Critical → Major → Minor, each issue with its type (Mechanical/Substantive), reason, and proposed fix (letter the
   options — M4A/M4B/M4C — when a fix has alternatives).
5. The user replies with the IDs/letters to apply; apply only those, re-run
   rendering QA (Step 11), save the revised file, and loop if they want another round.
```

## Core Instructions

### Step 0 — Locate and load the document
- Find the file in `input/` first (`Glob input/**/*`); also check `grounding/`.
  If the message has an `<attached_files>` block, read those paths directly.
- Read with the format-appropriate path: `.docx` → the `docx` skill (so you can
  detect tracked changes/comments and render to images); `.pdf` → the `pdf`
  skill; plain text/markdown → `Read`.
- If no file is found, say so plainly and ask the user to attach it. Never QC a
  document you could not read; never invent its contents.

### Step 1 — Set context (GATE — do this before any checking)
Identify and record: **document type, purpose, intended audience, risk tier, and
the required formatting + citation standard** (APA, MLA, Chicago, AWWA, IEEE,
ASME, or a project-specific guideline). Every later check is judged against these.
- **If any of these — especially the formatting/citation standard — is unclear or
  missing, STOP and ask the user** (via `AskUserQuestion`) before proceeding.
- If, after asking, none is provided, you MAY infer a likely standard from the
  domain and available context (including the user's profession — e.g. water-
  resources engineering often implies AWWA or a project spec). You **must** state
  the inferred standard explicitly as an assumption and **confirm it with the user
  before enforcing it.**

### Step 2 — Remove editing artifacts FIRST
Before any other review, detect and flag: tracked changes, comments, duplicated
text, draft/placeholder markers, and version-control leftovers. These come first
because they distort every downstream check.

### Step 3 — Structure and formatting
Verify headings, numbering, fonts, spacing, and bullet lists are consistent and
compliant with the chosen standard, and that the outline is complete — no
dangling, orphaned, or incomplete structural elements.

**Cross-references and numbering integrity.** Confirm every internal reference
resolves: "see Section 4.2", "Table 3", "Figure 5", "Appendix B", "Equation 2",
and page references must point to a target that exists and carries that number
and title. Confirm section, table, figure, equation, and appendix numbering runs
in sequence with no gaps, skips, or duplicates. In `.docx` files, also flag Word
fields (REF cross-references, SEQ captions, TOC, page numbers) whose displayed
result is stale or shows an error such as "Error! Reference source not found."
A reference to a missing target is Major; one that sends the reader to the wrong
content is Critical.

### Step 4 — Visual rendering QA (initial pass)
Render the document in its intended format (convert `.docx`/`.pdf` pages to images
and `Read` them) and verify layout integrity: page breaks, widows/orphans, table
formatting, column alignment, indentation consistency, and spacing artifacts that
plain text does not reveal.

### Step 5 — Content accuracy
Check that facts, figures, and statements are internally consistent. Flag
contradictions, obvious errors, and claims presented without adequate support.

**Defined terms and naming.** List the document's defined terms (capitalized
terms, terms introduced in quotes or parentheses, glossary and abbreviation
entries) and check each one: defined before first use, used at least once after
being defined (flag defined-but-unused), defined only once and consistently, and
capitalized consistently (Owner vs. owner, Engineer vs. engineer). Flag the same
entity called by different names (e.g., "the Plant", "the WTP", "the facility")
and acronyms used before they are spelled out or spelled out more than once.

### Step 6 — Completeness
Confirm all required sections are present and fully developed. Flag unresolved
placeholders ("TBD", "INSERT", "[ ]", "XXX") unless they are explicitly intentional.

### Step 7 — Clarity and audience fit
Ensure the document matches the defined audience, flows logically, introduces
concepts before using them, and communicates clearly.

### Step 8 — Grammar, spelling, and style
Flag grammar, spelling, tone, consistency, and readability issues; prefer clear,
direct, concise phrasing.

### Step 9 — Data and supporting content
Confirm statistics, examples, tables, and visuals align with the text, are
internally consistent, and are clearly explained and relevant.

### Step 10 — Citations and references (EXTERNAL VERIFICATION REQUIRED)
For every claim requiring support, perform **mandatory external verification**
using `web_search` (or the `deep-research` agent for heavier verification) against
approved source types. **Never rely on training data to confirm a citation.**
Then confirm: each citation complies with the chosen standard, each claim is
properly supported, each citation matches a valid reference, and each reference is
cited at least once. Flag any claim you cannot externally verify.

### Step 11 — Visual rendering QA (post-edit recheck)
If revisions were made (by you or the user) after Step 4, **re-render** and verify
no new layout issues were introduced: page-break shifts, table reflow, alignment
drift, or new spacing inconsistencies.

### Step 12 — Compliance and final read-through
Verify the document meets all requirements for scope, format, and constraints,
then read it once from the intended reader's perspective to judge whether it
effectively achieves its purpose.

## Severity Classification (apply to EVERY finding)
Tag each finding exactly one level:
- **Critical (C)** — blocks delivery: factual/data errors, missing required sections,
  unresolved placeholders, citation/verification failures, compliance violations,
  or anything that misleads the reader.
- **Major (M)** — significant quality problem that should be fixed before delivery:
  structural inconsistency, unsupported claims, broken citation–reference matches,
  rendering breakage, audience mismatch.
- **Minor (N)** — polish: wording, tone, cosmetic spacing, non-blocking style nits.
  (Prefixed `N`, not `m`, so Minor IDs are never confused with Major IDs by case.)

## Output — a tabulated, selectable fix menu
Present findings as an **actionable menu the user can choose from**, not a static
report. **Always render the findings table inline** so the user can select from
it — it is never hidden inside a file. What accompanies it inline, and whether a
file is saved, depends on the **size of the document under review**, not the
number of findings (rule of thumb: treat it as large at about 10+ pages of
content; otherwise small):

- **Small document** → render the whole thing inline as markdown — header,
  severity summary, and the findings table. Save no file unless the user asks.
- **Large document** → render inline a **concise summary** (header + severity
  summary) followed by the **full findings table**, THEN save the complete,
  detailed report (every finding with its location, evidence, citation
  verification log, and fix rationale) as a separate Markdown file in `output/`,
  named per the file-naming rules below. Glob-confirm the file exists before
  telling the user where it is.
- **Never put the QC report inside the document** — no appended pages or
  sections, comment blocks, or inserted tables, regardless of document size or
  the tool in use. The report lives only in chat and, for large documents, in the
  separate file. The only changes to the document are the fixes the user selects.

Whether shown inline or written to the saved file, use this structure:
1. **Header** — document name, type, audience, risk tier, and the formatting/
   citation standard used (note "assumed, confirmed" if inferred).
2. **Severity summary** — counts of Critical / Major / Minor and an overall
   **go / no-go** verdict.
3. **Findings table (the fix menu)** — one table with the columns
   `ID | Severity | Type | Location | Finding | Reason | Proposed fix`.
   - **IDs are severity-prefixed and sequential within each group:** `C1, C2, C3…`
     then `M1, M2, M3…` then `N1, N2, N3…`. Rows run Critical first, then Major,
     then Minor. Never reuse an ID.
   - **Finding** = what is wrong, stated factually. **Reason** = why it matters
     (the standard, requirement, or reader impact it violates). **Proposed fix** =
     the concrete change.
   - **When a finding has more than one reasonable fix, letter the options** inside
     the Proposed fix cell — `M4A`, `M4B`, `M4C` — each a distinct, self-contained
     alternative (e.g. M4A reword, M4B delete the sentence, M4C add a supporting
     citation). The user picks at most one letter per finding.
   - **Type** is `Mechanical` or `Substantive`. Mechanical = changes form, not
     meaning: spelling, punctuation, capitalization, spacing, numbering
     sequence, a defined term's spelling made consistent with its definition.
     Substantive = could change what the document says or requires: any number,
     unit, date, or threshold; a defined term's definition; requirement language
     (shall/should/may); a technical statement; adding or deleting a sentence.
     When in doubt, mark it Substantive.
   - **Batch row for bulk mechanical fixes.** When there are about 5 or more
     Minor, Mechanical fixes of the same kind (e.g., spelling and punctuation),
     group them into ONE row with a single ID (e.g., `N7` — 27 spelling/
     punctuation fixes) instead of one row each. Itemize them as `N7.1`,
     `N7.2`… with location and before → after text: directly under the table for
     a small document, in the saved report for a large one. Never batch a
     Substantive fix or a Critical/Major finding — those always get their own row.
4. **Citation verification log** — each checked claim, the source consulted, and
   verified / unverified. (Belongs in the QC report only — never in the document.)
5. **Selection prompt** — tell the user exactly how to choose: reply with the IDs
   they want applied, adding a letter for any lettered finding — e.g.
   `C1, M3, M4B, N2`. Also accept ranges within one group (`C1-C3`), `all critical`,
   `all major`, `all minor`, `all`, or `none`. For a batch row, accept the
   whole batch (`N7`) or the batch minus items (`N7 except N7.3, N7.12`).

### File naming (defaults; the user's stated convention overrides)
- **Saved QC report:** `YYYY-MM-DD QC Report - <Document Subject>.md`, using the
  user's local date. If another file shares that date, append a lowercase suffix in
  creation order to the date (`YYYY-MM-DDa`, `YYYY-MM-DDb`), omitted for a single file.
- **Revised document:** a new file; never overwrite or rename the original. If the
  original carries a version `(vMAJOR.MINOR.PATCH)`, increment it (MAJOR =
  structural/procedural/technical, MINOR = substantive content, PATCH =
  editorial/formatting/admin/error fixes). If it is unversioned, keep its name and
  append `(QC revised)`. Tell the user the prior version can be prefixed `delete_me-`
  at their discretion; do not rename it, issue reminders, or delete anything.
- Use spaces as primary separators, hyphens for hierarchy, parentheses for
  metadata; avoid OS-disallowed characters.

## Applying the selected fixes (selection loop)
After the user replies with their selection:
1. Map each chosen ID to its finding; for a lettered finding, apply only the
   chosen option. Ignore every finding the user did not select.
2. Apply the fixes with the format-appropriate editor (`docx` for Word, `pdf` for
   PDF). Change only what the selected fixes specify — nothing else.
   - **Preserve fields.** Word cross-references, captions, TOC entries, and page
     numbers are live fields that read as plain text. Edit only the text runs
     around a field; never replace a whole paragraph or run that contains one,
     which flattens it to static text. If a fix renumbers anything, update the
     dependent fields rather than retyping their results.
   - **Tracked changes only when asked.** If the user's prompt asks for tracked
     changes (redlines, revisions), write each applied fix as a native Word
     tracked change, never a simulated redline (colored or struck-through text).
     Attribute every tracked change and comment to the user's name as given in
     their preferences or profile — never "Claude", overriding the docx skill's
     default author; if the name is unknown, ask. Otherwise apply fixes directly.
   - **Leave existing review marks alone.** Never accept or reject tracked
     changes already in the document, or delete its comments, as clean-up —
     only when a selected finding says to.
3. **Read back every edited range** from the saved file and confirm it holds the
   intended text, font, and paragraph style; check the paragraphs on either side
   for collateral changes (formatting spilling into a neighbor, a flattened
   field, a list merged with the next one). Then re-run **Step 11 (visual
   rendering QA)** so no fix introduced a new problem (layout shift, table
   reflow, broken citation).
4. Save the revised document to `output/` under a new name (see File naming);
   never overwrite the user's original.
5. Report back: which IDs were applied, which were skipped, and any new issue the
   recheck found — re-listed in the same table format so the user can run another
   selection round. Report only what you actually changed and read back; say
   "all" or "every" only if you verified every instance (e.g., "applied 25 of 27
   items in N7; N7.3 and N7.12 not found at the stated location").

## Guardrails
- **Context gate (Step 1) is mandatory.** If type/purpose/audience/risk/standard
  is unclear, ask before reviewing. An inferred standard must be stated as an
  assumption and confirmed before it is enforced.
- **Citations require external verification** (`web_search` / `deep-research`).
  Never confirm a reference from training data; flag whatever you cannot verify.
- **Protect sensitive content.** If the document contains PII, credentials, or
  confidential data, never reproduce it verbatim in the findings report — redact
  it or reference it by location instead, and respect the document's privacy.
- **Every finding gets a severity and a reason.** No unclassified or unexplained issues.
- **The report never goes into the document.** No QC pages, comments, or inserted
  sections unless the user explicitly asks for one.
- **Never fabricate.** Do not invent the document's contents, sources, or quotes.
  If a file cannot be read, say so and ask for a re-attach — never substitute
  sample or placeholder content.
- **Apply only what the user selects.** Present the findings table and wait;
  edit the document only for the findings (and lettered options) the user picks.
  Never apply an unselected fix, and never auto-rewrite the whole document.
- **Preserve the original.** Save revisions as a new file in `output/`; never
  overwrite or rename the user's uploaded document, and re-run rendering QA after applying.
- **Never flatten fields or clear review marks.** Preserve Word fields when
  applying fixes, and never accept, reject, or delete existing tracked changes or
  comments unless a selected fix calls for it.
- **Order matters.** Remove editing artifacts (Step 2) before other checks, and
  re-run rendering QA (Step 11) after any revisions.