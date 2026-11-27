# truth-seeking-panel changelog

Earlier version history was not recorded in the skill folder; this file starts at v1.1.1.

## v1.1.2 (2026-11-26)

Editorial fix. Version is PATCH.

### Fixed
- **Undefined terms in the Demotion rule.** "Scope Referee" and "Definition Enforcer" were not defined anywhere in the skill. The rule now uses the existing tags: an expert tagged **[SCOPE DRIFT]** or **[TERM DRIFT]** twice in the same round (any combination) is limited to Adversarial Rebuttal Only. The "any combination" reading is my interpretation of "fails ... or ... twice".
- **Frontmatter.** `metadata: version` is now "1.1.2".

## v1.1.1 (2026-11-26)

Editorial fix from an audit of v1.1.0.

### Fixed
- **Search tool names.** The live-search mandate named only `web_search` / `web_fetch`. It now also accepts the session's equivalent search tools, and says to flag claims **[UNVERIFIED]** when no search tool is available.
- **Frontmatter.** Added `metadata: version: "1.1.1"`.

### Open (not changed in v1.1.1)
- The Ethical Guardrail statement appears in rule 1 and in Phase 1 step 8. Decided 2026-11-26 to keep both (standing rule and the statement shown before the halt). Closed.
