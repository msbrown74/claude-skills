# Claude Skills

A place to store and sync all my LLM skills I use in Claude, Claude Code, and Claude Desktop. These can be adapted to be used in other LLMs.

Each one is a custom [Agent Skill](https://platform.claude.com/docs/en/agents-and-tools/agent-skills/overview): a folder with a `SKILL.md` file that tells Claude how to handle one kind of task. Use them as they are, or adapt them to your own workflow.

## Skills

| Skill | What it does | Try saying |
|---|---|---|
| [`delta-sync-maintenance`](skills/delta-sync-maintenance/SKILL.md) | Reviews recent chats in a Claude Project and turns the confirmed facts into a refreshed Project Instructions block. | "run delta-sync" |
| [`qc-sweep`](skills/qc-sweep/SKILL.md) | Runs a 12-step quality-control review of an existing document and returns a numbered fix menu ranked Critical, Major, or Minor. | "run a QC sweep on this document" |
| [`qc-sweep-xlsx`](skills/qc-sweep-xlsx/SKILL.md) | Runs the same style of 12-step review on a spreadsheet or workbook, covering formulas, hidden content, links, and data integrity. | "run a QC sweep on this workbook" |
| [`reverse-outlining-documents`](skills/reverse-outlining-documents/SKILL.md) | Extracts the heading hierarchy of an existing document into a read-only outline with structural notes. | "reverse outline this" |
| [`text-humanization`](skills/text-humanization/SKILL.md) | Rewrites AI-drafted or stilted text so it reads as natural, human-written prose. | "humanize this draft" |
| [`thread-archivist`](skills/thread-archivist/SKILL.md) | Packages a conversation into one copy-paste block (background, decisions, open items, next step) for continuing in a new chat. | "archive this thread" |
| [`truth-seeking-panel`](skills/truth-seeking-panel/SKILL.md) | Stress-tests a claim or decision with a panel of fictional expert personas, cross-examination, and a scored resilience report. | "run the truth-seeking panel on this" |

## Install

**Claude Code plugin (all seven skills at once)**

This repository is also a Claude Code plugin marketplace. In Claude Code on your computer (terminal, desktop app, or VS Code), run:

```
/plugin marketplace add msbrown74/claude-skills
/plugin install core-skills@msbrown74-skills
```

On Claude Code 2.1.275 or later, one command does both:

```
/plugin install core-skills --marketplace msbrown74/claude-skills
```

The skills then appear as `/core-skills:<skill-name>`, for example `/core-skills:qc-sweep`.

Auto-update is off by default for third-party marketplaces. To turn it on, run `/plugin`, open the **Marketplaces** tab, select `msbrown74-skills`, and choose **Enable auto-update**. To update by hand, run `/plugin marketplace update msbrown74-skills`.

Installing the plugin adds roughly 2,000 tokens of skill descriptions to every session (a Claude Code estimate). If you only need a few skills, use one of the options below instead.

**Claude (web or desktop app), one skill at a time**

1. Download the zip for the skill you want from the [`zips`](zips/) folder.
2. In Claude, open **Customize → Skills**, click **+**, choose **Create skill**, then **Upload a skill**, and select the zip.
3. To update a skill, upload the newer zip.

**Claude Code, one skill at a time**

Copy the skill's folder from [`skills`](skills/) into `~/.claude/skills/` (all projects) or `.claude/skills/` (one project).

Custom skills are managed separately in each place Claude runs them, so install a skill everywhere you plan to use it.

## Repository layout

```
.claude-plugin/                   Plugin and marketplace catalog for Claude Code
skills/<skill-name>/SKILL.md      Source for each skill
zips/Skill - <skill-name> (vX.Y.Z).zip    Upload-ready package for each skill
```

## Versions

Zip files carry a [semantic version](https://semver.org/) in their names:

- **MAJOR**: structural, procedural, or technical changes to how the skill works
- **MINOR**: substantive content changes
- **PATCH**: editorial, formatting, or error fixes

## Use with care

Skills steer an AI model, and the model can still make mistakes. Check the output before you rely on it, especially for professional, technical, or high-stakes work.

## License

Released under the [MIT License](LICENSE).

## Feedback

Questions, bug reports, and suggestions are welcome through GitHub Issues.
