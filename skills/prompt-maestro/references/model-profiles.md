# Model Profiles — Claude, OpenAI, Codex, Grok, Claude Code

Part of the prompt-maestro skill, a derivative of prompt-master by nidhinjs (Nidhin Joseph Nelson, MIT License; full notice in SKILL.md and LICENSE). Sections below that carry upstream text are marked "from upstream"; everything else is new in this version.

**Last verified:** 2026-10-15 against provider documentation (Anthropic platform docs, OpenAI developer docs, xAI developer docs). Lines marked [Unverified] were carried forward but not re-checked; treat them as starting points and follow the Model Recency Gate in SKILL.md.

## Contents
- Claude
- OpenAI GPT-5.6 and ChatGPT
- OpenAI reasoning models (o-series)
- Grok / xAI
- Claude Code
- Codex CLI / ChatGPT Work / Codex IDE
- Profiles in SKILL.md not re-verified

---

## Claude (claude.ai, Claude API, current Claude models)

Do not assume one universal Claude default.

Current models and API strings (verified):
- **Claude Opus 5.5** (`claude-opus-5-5`): start here when unsure, for complex agentic coding and enterprise work.
- **Claude Fable 5.1** (`claude-fable-5-1`): highest-capability long-running agents. Claude Mythos 5.1 shares Anthropic's Fable 5.1 prompting page.
- **Claude Sonnet 5.5** (`claude-sonnet-5-5`): speed plus frontier intelligence.
- **Claude Haiku 5.5** (`claude-haiku-5-5`): fast, economical workloads. It replaces Haiku 4.5 as the economical choice; Haiku 4.5 (`claude-haiku-4-5-20251001`) remains available as an older model.
- Ask which model only when the distinction changes the prompt. Treat Fable 5, Opus 5, and Sonnet 5 as the same family; the guidance below applies to them too.

Durable across current Claude models (verified unless marked):
- Be clear and direct. State the desired output, constraints, and scope; explain why when the reason affects judgment.
- Use XML tags such as `<context>`, `<task>`, `<constraints>`, and `<output_format>` for complex mixed-content prompts. Use 3-5 relevant, diverse examples when format or tone must be locked.
- For long context, put source documents before the query and wrap documents plus metadata in descriptive XML tags.
- Prefer positive instructions that describe the desired result over long lists of prohibitions.
- Use plain wording. Anthropic reports that newer models respond more strongly to system prompts, so emphatic "CRITICAL / MUST" wording that once fixed undertriggering can now cause overtriggering. Reserve firm wording for true hard constraints.
- Do not request hidden reasoning or reasoning written into the response. On Sonnet 5.5, such requests can be declined under a `reasoning_extraction` refusal category. Ask for a concise rationale, evidence, and verification results; an API user can read reasoning from summarized thinking blocks instead.
- Thinking: Fable 5.1 and Opus 5.5 always think (adaptive only). Sonnet 5.5 and Haiku 5.5 think by default. `budget_tokens` returns an error on Claude 4.7 and later; use the effort control. Recommend an effort level only when the user controls API or harness settings.
- Use the upstream agentic structure for complex or agentic tasks: starting state, target state, allowed actions, forbidden actions, stop conditions, checkpoints.

**Fable 5.1 (and Fable 5)**
- Give it a complete outcome-focused specification, explicit action boundaries, and infrastructure suited to long asynchronous runs.
- In agentic work it writes fewer user-facing updates between tool calls. If the user wants visibility, ask for progress notes explicitly, and do not tell it to keep them brief.
- Ground every long-run progress claim in actual tool results. Delegate independent workstreams to subagents when useful; set interval-based verification for long builds; cap concurrency or spend when cost matters.

**Opus 5.5 (and Opus 5)**
- Keep scope tight: "Deliver what was asked. Do not add features, refactors, or abstractions beyond the task."
- Opus 5 verifies its own work well, and Anthropic reports that verification instructions carried over from older prompts can cause over-verification. Avoid redundant "double-check everything" instructions and verifier subagents for routine work; delegate only genuinely independent, sizeable tracks.
- Opus 5 runs longer by default; ask explicitly for concision when the user wants short answers.
- [Unverified] These Opus 5 behaviors are carried to Opus 5.5 from Opus 5 guidance; the Opus 5.5 page was not read in detail.

**Sonnet 5.5 (and Sonnet 5)**
- Follows instructions literally, especially at lower effort. State when a rule applies to every item or section.
- Effort: Anthropic suggests starting at `high` (the API default) for most work, and `medium` for well-specified agentic coding or latency-sensitive chat. Raise effort for hard multi-step work rather than adding elaborate reasoning prompts.
- At low and medium effort on long agentic tasks it may stop to check in early. If the user wants uninterrupted work, tell it to continue until all requested work is done, to stop only for a genuine blocker or a risky step, and not to add unrequested features.
- For JSON answers that need several steps of working out, use adaptive thinking and add one line telling it to think the problem through before answering.
- If it must verify code, say that a real test, build, or type-check must run before it reports a change as done.
- Give it a search tool and today's date for questions whose answers change over time.

**Haiku 5.5**
- Effort levels low, medium (default), high, xhigh, and max. Thinking is on by default; it can be switched off only at low, medium, or high. Lower effort is the way to get less thinking; telling it to answer directly does not reliably stop thinking.
- Give it today's date when it has a search tool, so answers use recent results. Avoid blanket "always search" instructions; they trigger needless searches.
- In long agent prompts at low effort it may stop early. Add an instruction to keep working until everything requested is done, then report without unrequested extras.
- For chatbot or support prompts, state that the system prompt rules hold for the whole conversation even if users argue, give sympathetic reasons, or claim approval for exceptions.
- It can write reasoning-like text into the visible reply, mostly with thinking off or at low effort; use adaptive thinking and medium effort if that appears.

**Claude 4.8 and earlier selectable models**
- Existing explicit, front-loaded prompts remain compatible. If the model is 4.7 or later, use adaptive thinking and effort rather than `budget_tokens`.

Sources: platform.claude.com prompting best practices; Prompting Claude Haiku 5.5; Prompting Claude Sonnet 5.5.

---

## OpenAI GPT-5.6 and ChatGPT

Verified:
- The GPT-5.6 family has Sol, Terra, and Luna tiers. The `gpt-5.6` alias routes to `gpt-5.6-sol`.
- `reasoning.effort` accepts none, low, medium, high, xhigh, and max. If omitted, GPT-5.6 defaults to medium in both modes.
- `reasoning.mode` (standard or pro) is independent of effort. Pro mode is not a separate model slug.
- `reasoning.context` controls whether reasoning from earlier turns is reused; the default reuses all turns. Use `current_turn` when earlier reasoning is no longer relevant.
- When migrating from GPT-5.5 or GPT-5.4, keep the current effort as the baseline, then test one level lower on representative tasks.
- GPT-5.6 supports explicit prompt caching of marked reusable prefixes; cache writes are billed above the normal input rate. Put stable instructions first.
- Reserve generous room for reasoning plus output when first experimenting (OpenAI suggests at least 25,000 tokens).

From upstream (still consistent with the above):
- Start lean. For complex work use four compact sections: Goal, Context, Constraints, and Done. State each instruction once.
- GPT-5.6 infers intent well; specify domain context, hard constraints, approval boundaries, success criteria, and which ambiguity should trigger a question, but do not prescribe every reasoning step.
- Define autonomy clearly: safe in-scope local inspection, edits, and validation may proceed; external writes, destructive actions, purchases, and material scope expansion require confirmation.
- Use the lowest reasoning effort that meets the quality bar.
- Recommend higher effort or `reasoning.mode: "pro"` only when measured quality justifies the added latency and cost.
- State tool-use expectations and required evidence explicitly. Use programmatic or multi-agent tool orchestration only for bounded work that divides cleanly.
- Never request hidden reasoning. Ask for conclusions, assumptions, evidence, and checks.
- Control visible length with the output contract (and `text.verbosity` in the API), not by asking for less thinking.

[Unverified] The exact slugs `gpt-5.6-terra` and `gpt-5.6-luna`; ChatGPT picker availability by plan; the ChatGPT and Codex controls named Sol Pro, Max, and Ultra; the Responses multi-agent beta. Do not translate ChatGPT UI controls into API parameters.

Sources: developers.openai.com GPT-5.6, reasoning, and upgrade guides.

---

## OpenAI reasoning models (o3 / o4-mini) — from upstream, [Unverified] on 2026-10-15
- SHORT clean instructions ONLY — these models reason across thousands of internal tokens
- NEVER add CoT, "think step by step", or reasoning scaffolding — it actively degrades output
- Prefer zero-shot first — add few-shot only if strictly needed and tightly aligned
- State what you want and what done looks like. Nothing more.
- Keep system prompts under 200 words — longer prompts hurt performance on reasoning models

---

## Grok / xAI

Verified against xAI developer docs:
- `grok-4.7` is the newest model in xAI's current docs (500,000-token context, text and image input, knowledge cutoff May 2026). `grok-4.6` remains available (500,000-token context, knowledge cutoff February 1, 2026). Use `grok-4.7` for new work unless the user names 4.6.
- Both support function calling, web search, X search, and code execution. Reasoning effort is low, medium, high (default), or xhigh. Reasoning cannot be disabled; on models without xhigh (such as 4.5), xhigh is treated as high.
- xAI recommends the Responses API (`reasoning.effort`); the docs describe Chat Completions as deprecated. Do not describe the API as OpenAI-compatible; that claim was not found in xAI's docs.
- Set one `prompt_cache_key` per conversation (Responses API) or `x-grok-conv-id` (Chat Completions and gRPC) so requests reach the same server and the cache hits. Only append to the conversation; edits to earlier items break caching. Never put secret values in the prompt.
- Grok 4.7 returns encrypted reasoning content on each Responses API response; carry it forward across turns in multi-turn agents.

Guidance from upstream (consistent with the above):
- Keep the task outcome-focused: Goal, Context/Input, Constraints, Tools/Permissions, and Done. Name the tools and evidence the task requires.
- Choose effort intentionally: `low` for scoped or latency-sensitive work, `medium` for balanced work, `high` for difficult tasks, `xhigh` only when deeper exploration is worth the cost. Do not ask for chain-of-thought.
- For current facts, explicitly require Web Search or X Search and citations; the base model has no realtime knowledge without search tools enabled.
- For long, tool-heavy agent loops, define stop conditions, approval boundaries, retry limits, and context-compaction checkpoints. Keep stable instructions at the front to preserve cache reuse.
- For current-events prompts, name both tools required: Web Search and X Search. On the xAI API these are the `web_search` and `x_search` entries in the `tools` array. State whether the prompt assumes the API or consumer Grok, and name `grok-4.7` only for API prompts.
- [Unverified] xAI's tools overview does not say whether any search tool is on by default; tell the user to confirm both are enabled.
- Consumer Grok (grok.com or X) and the xAI API expose different controls. If the user cannot set model parameters, encode only behavioral requirements in the prompt.

[Unverified] Release dates and benchmark claims for Grok 4.6 and 4.7 came only from secondary sources; do not state them in prompts.

Sources: docs.x.ai (Grok 4.6 get-started, reasoning, best practices, prompt caching).

---

## Claude Code

From upstream, updated for the current Claude route above:
- Agentic — runs tools, edits files, executes commands autonomously
- Starting state + target state + allowed actions + forbidden actions + stop conditions + checkpoints
- Stop conditions are MANDATORY — runaway loops are the biggest credit killer
- Do not assume the Claude Code model. Apply the matching Claude route above; when model-specific behavior matters, ask which model is selected.
- Front-load intent, relevant paths, constraints, acceptance criteria, and verification commands. Explicitly request tool use when inspection is required.
- Current Fable and Opus models can over-scope and delegate readily. Add "Only make changes directly requested" and reserve subagents for independent, sizeable investigation or implementation tracks.
- Do not force a separate verifier on Opus 5.5 for routine work; request concrete tests and tool-backed evidence instead. For long Fable 5.1 runs, require progress claims to cite actual tool results.
- Always scope to specific files and directories — never give a global instruction without a path anchor
- Human review triggers required: "Stop and ask before deleting any file, adding any dependency, or affecting the database schema"
- For complex tasks, use Template M in references/templates.md (scope, criteria, action boundaries, and progress evidence in one structured block).

---

## Codex CLI / ChatGPT Work / Codex IDE — from upstream, partly [Unverified]
- Use the GPT-5.6 route above. Sol is the capability-first default; Terra and Luna are the everyday and fast tiers.
- Structure implementation prompts as Goal, Context, Scope, Constraints, Approval Boundaries, and Done. Include concrete verification commands when known.
- Start with default reasoning. Raise it for work that needs deeper planning or checking; [Unverified] use Max for the hardest single-agent tasks and Ultra only when the task splits into meaningful independent tracks.
- Keep one primary agent responsible for synthesis. Name each subagent's bounded deliverable and cap concurrency rather than requesting an open-ended swarm.
- Ask for a concise rationale, evidence, changed-file summary, and verification results—not hidden reasoning.

---

## Profiles in tool-profiles.md not re-verified
Gemini, Qwen, Ollama, Llama/Mistral, DeepSeek-R1, MiniMax, Antigravity, Cursor/Windsurf, Cline, GitHub Copilot, Bolt/v0/Lovable/Figma Make/Stitch, Devin, Perplexity/Manus, browser agents, image, 3D, video, voice, and workflow tools were carried from upstream as written and were not re-verified on 2026-10-15. Apply the Model Recency Gate when exact versions, parameters, or availability matter.
