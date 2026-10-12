---
name: "delta-sync-maintenance"
description: "Audits chat sessions since the last run in a Claude Project, extracts new facts as a memory-delta changelog, and produces a refreshed Project Instructions block. Complements Claude's native per-project memory rather than duplicating it — use specifically to promote confirmed facts into the standing Custom Instructions layer, which native memory cannot write to. Trigger when the user says \"run delta-sync\", \"refresh project instructions\", \"sync project memory\", \"catch up my project's instructions\", or \"update project memory from recent chats\". Do NOT use for one-off memory capture — Claude's native per-project memory already handles that. Do NOT use to summarize a single chat session — that's a plain recap, not an instruction sync."
---

# Delta-Sync Maintenance & Instruction Bootstrapper

## Purpose

Maintains a Claude Project's **Custom Instructions** by periodically auditing recent chat activity, extracting new facts, and producing (1) a categorized changelog and (2) a refreshed, production-ready `<project_instructions>` block the user pastes into Project Settings.

This is not a substitute for Claude's native per-project memory, which already runs automatically and needs no manual trigger. Native memory captures and surfaces context on its own; it does not write to the Custom Instructions layer. This skill's job is narrower and complementary: **deliberately promoting specific, user-confirmed facts into the standing instructions every conversation in the project loads.** If nothing needs to be promoted to that layer, don't run this — native memory already has it covered.

If you'd rather run this as a one-off prompt instead of installing it as a Skill, everything from "# Delta-Sync..." down works pasted directly into a chat — just drop the frontmatter above.

## When NOT to Use

- **Capturing a single new fact from the current conversation.** Native per-project memory already does this automatically — don't invoke this skill just because something worth remembering came up.
- **Summarizing what happened in one chat session.** That's a plain recap for the user to read; this skill produces a changelog and an instructions block meant to be pasted into Project Settings, not a session summary.
- **Updating instructions outside a Claude Project** (e.g. a standalone chat, a different platform's custom-instructions field) — this skill's output format assumes the `<project_instructions>` structure and the Project Settings paste target described below.

## Step 1 — Context & Historical Audit

1. Check the current Project Instructions (or `PROJECT_MEMORY.md` if attached) for a `<!-- Last synced: [date] -->` marker.
   - If present: audit only sessions since that date.
   - If absent: this is a **Cold-Start** — audit the last 3–5 sessions or 7 days, whichever is available, and flag every extracted item as inferred (see Step 2).
2. Review the in-scope chat history and any attached Project Knowledge files.
3. Identify candidate facts: architectural/technical choices, user preferences, operational rules, or constraints.

## Step 2 — Extract Memory Deltas

Produce `PROJECT_MEMORY_UPDATE.md` with entries tagged:

- `[DECISION]` — finalized technical, design, or strategic choice
- `[PREFERENCE]` — user style, formatting, or interaction preference
- `[CONSTRAINT]` — environment limit, budget bound, or strict negative rule

**Provenance tag — required on every entry, not just Cold-Start:**
- `[CONFIRMED]` — the user explicitly stated or agreed to this
- `[INFERRED]` — Claude concluded this from context; the user didn't explicitly confirm it

If no new facts were introduced: output `"No new project memory deltas identified."`

## Step 3 — Synthesize / Refresh Project Instructions

Construct a complete `<project_instructions>` XML block:

```xml
<role>
Domain persona, technical authority level, analytical stance.
</role>

<context>
Project scope, core technology/subject matter, operational environment.
</context>

<memory_architecture>
Four layers, not three — the platform already provides two of these automatically:
1. Active Session Context: current chat (highest immediate priority).
2. Native Memory (automatic): Claude's built-in per-project memory. Runs on its own; this skill does not duplicate it.
3. Project Knowledge (RAG): attached files, retrieved as relevant rather than loaded in full.
4. Custom Instructions (this block): the only layer this skill writes to — durable facts deliberately promoted here.
</memory_architecture>

<clarification_protocol>
When user input is ambiguous, incomplete, or presents >2 valid implementation paths:
- Don't guess or proceed on unverified assumptions.
- Present: (1) a one-sentence statement of what parameter is needed, (2) a bulleted 3-4 option list, (3) an "Other / Custom" option.
</clarification_protocol>

<operating_rules>
- Check Active Session Context, Project Knowledge, and this block, in that order, before answering.
- If critical parameters are missing, trigger <clarification_protocol>.
- Cite specific attached filenames when drawing from Project Knowledge.
</operating_rules>

<output_formatting>
- Lead directly with substance; omit conversational openings.
- Use Markdown tables for multi-variable comparisons.
- Use bullet points for sequential steps or itemized criteria.
</output_formatting>

<negative_constraints>
- DO NOT repeat or rephrase the user's prompt prior to answering.
- DO NOT invent project parameters not supported by attached files, active chat, or a [CONFIRMED] memory entry.
- DO NOT auto-generate large prose setups; jump straight into structured output.
</negative_constraints>

<!-- Last synced: [today's date] -->
```

**Length:** keep this block as concise as completeness allows. Anthropic's own guidance is to keep Project Instructions focused and reserve task-specific detail for the chat itself — treat any specific token target you set as your own working heuristic, not a documented platform limit.

**Cold-Start:** mark inferred sections `<!-- Bootstrapped: Review Needed -->`.

## Step 4 — Change Summary

Before presenting deliverables, produce a short plain-language changelog: what was added, changed, or removed vs. the prior version, plus explicit confirmation that `<negative_constraints>` and `<clarification_protocol>` are unchanged (or a note on what changed and why, if the user directed it). This is the user's actual review checkpoint before anything gets pasted into the project — without it, adopting the new block is a leap of faith.

## Guardrails

- **No fabrication.** Never invent a fact that isn't traceable to an actual chat message or attached Project Knowledge file — if evidence is thin, mark it `[INFERRED]` rather than presenting it as settled.
- **No silent provenance upgrades.** Don't upgrade an `[INFERRED]` item to `[CONFIRMED]` on a later run just because it appeared in the prior instructions — re-verify against the actual transcript, or leave it `[INFERRED]`.
- **Verbatim preservation.** `<negative_constraints>` and `<clarification_protocol>` must be reproduced **verbatim** from the prior version unless the user explicitly directs a change. Diff against the prior version before finalizing (Step 4) — don't just intend to preserve them.
- **Review before adoption.** Always surface the Step 4 Change Summary before the user pastes the refreshed block into Project Settings — never present the instructions block as a fait accompli.

## Output Deliverables (three separate copy-paste blocks)

1. **`PROJECT_MEMORY_UPDATE.md`** — append to the attached memory file.
2. **Refreshed `<project_instructions>`** — paste into Project Settings → Instructions.
3. **Change Summary** — for the user's own review before pasting Deliverable 2 in; not part of the project file.