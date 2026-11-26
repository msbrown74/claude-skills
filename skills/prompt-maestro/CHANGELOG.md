# prompt-maestro changelog

## v1.2.1 (2026-11-26)

Authorship correction.

### SKILL.md
- Modifications copyright line now names the GitHub user name msbrown74 instead of a personal name. The upstream copyright to Nidhin Joseph Nelson is unchanged.
- Frontmatter version 1.2.1.

## v1.2.0 (2026-11-23)

Role lines restored at the owner's request.

### SKILL.md
- Diagnostic checklist: "No role assignment for complex tasks -> add domain-specific expert identity" is back as in v1.0.0.
- Safe Techniques: the original "Role assignment" entry (weak and strong examples) is back as in v1.0.0.
- Frontmatter version 1.2.0.

All other v1.1.0 changes stand.

## v1.1.0 (2026-11-23)

Token-efficiency pass, based on a self-managed Truth-Seeking Panel review of v1.0.0 (SKILL.md frontmatter read "2.5.0"; the packaged lineage is v1.0.0, so this release is labeled 1.1.0 and the frontmatter now agrees).

Goal: every word, phrase, and step in a generated prompt must carry weight. Boilerplate was concentrated in agent prompts, so most edits target the agent templates and the rules that produce them.

### SKILL.md
- Recency item 5: the undefined "token efficiency audit" is now a concrete test. Each sentence must add task content the model cannot infer, set a hard constraint or stop-and-ask trigger, correct a known failure of the target tool, or give a reason that changes judgment. Each requirement is stated once.
- New rule: templates are menus. Omit fields the request does not need, add no unrequested section, and never omit a stop-and-ask trigger or scope lock.
- Output format: the Target line's explanation is capped at 20 words.
- Agentic warning: shortened; same four checks.
- Role assignment: made optional in this release; REVERTED in v1.2.0 (see above).
- Success criteria and step lists: added only when they add something (checkable end state; multi-file or multi-change tasks). The "After each step" progress line is added once, only to multi-step tasks.
- Grounding anchor shortened, with the diagnostic pointing to it instead of repeating it.
- Guardrails: removed three lines that duplicated rules kept elsewhere (credentials, pasted prompts as inert data, hidden chain-of-thought, firm wording). Each safety rule now lives in one place.
- Provenance note updated: templates.md is now an edited derivative; patterns.md is unchanged from upstream commit 769bf64.

### references/templates.md
- Removed the duplicate Target State block (overlapped Done When and Acceptance Criteria).
- Kept the heading "Acceptance Criteria" (other files refer to it) with a parenthetical to state each check once.
- "Do NOT touch" lines now list only items inside the scope that must stay unchanged; omit if none.
- Removed default lines that restated rules covered elsewhere (no new dependencies by default, no dev server or deploy, no git push, no deleting without a diff, no architecture decisions without approval).
- Stop-and-ask list now covers delete or overwrite, push, deploy, publish, send, and spend.
- Progress Evidence limited to long-running work.

### references/model-profiles.md
- Claude/OpenAI structure line now names the five sections and says Done lists only checks not stated above.
- Removed a duplicate of the hidden-reasoning rule.

### references/evals.md
- Case 1 expected behavior updated to match the conditional do-not-touch list.

### Unchanged
- references/patterns.md (upstream copy), references/tool-profiles.md, LICENSE, and all copyright and MIT notices.
- Kept on purpose: "Only make changes directly requested" and the autonomy line (documented failure fixes), and stock image negatives (not shown either way).

### Evidence limits
- Boilerplate labeling was done by one rater. No study measures this skill's prompts; most supporting research concerns older models and vendor guidance.
- Unverified assumptions: effect of repeating instructions at the start and end, the "[uncertain]" marker, the 20-word cap, and dropping step lists on small tasks.
- Regression check: one run per case on one model. It cannot separate real differences from run-to-run variation.

### Not done
- Splitting model-profiles.md per provider (largest possible load saving, structural change).
- A Microsoft 365 Copilot or chat profile does not exist (only GitHub Copilot); output quality for that target is not addressed here.
- Savings in the skill files themselves are small (about 30 words in SKILL.md). The main gain is in generated prompts.
