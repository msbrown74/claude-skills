# Credits

Ideas were adapted, not copied. Check each project's own license before reusing its text.

| Source | License | What was borrowed |
|---|---|---|
| Anthropic "Auto Dream" for Claude Code (unofficial write-up, claudefa.st) | not applicable | Four phases (orient, gather signal, consolidate, prune and index); convert relative dates to absolute; fix contradictions at the source; dual trigger (time and activity) |
| Anthropic Managed Agents "dreaming" (research preview) | not applicable | Choice between automatic updates and review before changes land |
| orchestkit `dream` (Yonatan Gross) | MIT | Dry-run first; deterministic checks before judgment; about 60% word-overlap duplicate test; consult-gate before pruning |
| grandamenium `dream-skill` | MIT | Backup before the first run; never delete without a replacement; verification list after a run |
| mem0 `dream` | Apache-2.0 | Pinned entries never pruned; diff report before changes; per-conflict choice (A, B, skip); contradictions not auto-resolved; concurrency guard |
| OpenClaw `memory-doctor` | MIT-0 | Index drift and orphan checks; snapshot-backed manual apply |
| OpenClaw `agent-memory-cleanup`, `willow-memory-health`, `memory-curator` | not checked | Cleanup only after authorization; monthly review cadence |
| kochetkov-ma `memory-optimize` (brewcode) | not stated | Interactive approval per step; migrate entries that belong in rules; a validation pass |
| SomeStay07 `claude-memory-skill` | not checked | Canonical location per topic |
| Agent Skills specification and Anthropic skill authoring guidance | not applicable | Frontmatter limits, progressive disclosure, one-level references, plan-validate-execute for destructive work |
| Claude Code memory documentation | not applicable | `MEMORY.md` index loads the first 200 lines or 25 KB |
