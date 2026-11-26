# qc-sweep-xlsx changelog

Earlier version history was not recorded in the skill folder; this file starts at v2.1.0.

## v2.1.1 (2026-11-26)

Administrative fix. Version is PATCH.

### Fixed
- **Repo sync.** The GitHub repo copy (msbrown74/claude-skills) was still at v2.0.0. It now matches this folder. The v2.1.0 note below that the repo copy "was not read or changed" is superseded.
- **Frontmatter.** `metadata: version` is now "2.1.1".

## v2.1.0 (2026-11-26)

Internal-defect fixes from an audit of v2.0.0. Version is MINOR because severity and selection behavior changed.

### Fixed
- **Duplicate Color convention block (Step 3).** The second copy contradicted the first: it proposed vermillion (#D55E00) for links, which the first copy's "Reserve reddish-orange for errors" rule forbids. The second copy was deleted; the first (bluish green #009E73 for links, with the reserve rule) is kept.
- **Report inside the workbook.** Guardrails allowed a QC tab if the user asked; Output forbade it regardless. Guardrails now match Output: the report never goes into the workbook.
- **"Remove hidden artifacts" wording.** Step 2 title and the Order guardrail now say detect and flag, matching a read-and-report pass.
- **When NOT to Use.** "Applying the fixes" entry reworded to "applying fixes the user has not selected by ID", since the skill applies selected fixes.
- **Frontmatter.** Added `metadata: version: "2.1.0"`. Description now lists clarity and grammar steps.
- **Severity wording.** Critical now says "formula/value errors (including error values already displayed)". Step 5 now separates latent unguarded divisions (Major; Critical if they reach a design output) from error values already displayed (Critical).
- **Unprotected cells.** "Unprotected inputs that invite corruption" (Critical) is replaced by "unprotected formula cells that invite overwriting", now listed as Major, matching Step 3. This is a judgment on the intent of the old wording and lowers that case from Critical to Major.
- **Environment caveats.** Quick Start, batch itemization, Step 4, Step 12, and the data-analysis reference now say what applies standalone and what applies in the Claude for Excel add-in. Whether the add-in can screenshot is unverified.
- **Bulk selection.** `all`, `all critical/major/minor`, and ranges now skip lettered findings and `destructive` fixes; those must be named explicitly (with the letter). Previously the behavior was unspecified.

### Not changed
- Cosmetic hard-wrapping in a few lines; Step 1 and Step 5 both stating the design-basis rule (consistent, so left).
- The GitHub repo copy (msbrown74/claude-skills) was not read or changed.
