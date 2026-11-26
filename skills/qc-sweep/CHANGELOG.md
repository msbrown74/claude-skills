# qc-sweep changelog

Earlier version history was not recorded in the skill folder; this file starts at v1.3.0.

## v1.3.0 (2026-11-26)

Internal-defect fixes from an audit of v1.2.0. Version is MINOR because selection and report-placement behavior changed. The same three defects were fixed in qc-sweep-xlsx v2.1.0.

### Fixed
- **Report inside the document.** Guardrails allowed QC pages, comments or inserted sections if the user explicitly asked; Output forbade it regardless of document size or tool. Guardrails now match Output: the report never goes into the document.
- **"Remove editing artifacts" wording.** Step 2 title and the Order guardrail now say detect and flag, matching a read-and-report pass.
- **When NOT to Use.** The "Applying the fixes" entry now reads "applying fixes the user has not selected by ID", since the skill applies the fixes the user selects.
- **Environment fallbacks.** Step 0 now says what to do when there is no `input/` folder; `AskUserQuestion` falls back to plain chat; saves to `output/` fall back to the session's working folder when there is no `output/`.
- **Frontmatter.** Added `metadata: version: "1.3.0"`.
