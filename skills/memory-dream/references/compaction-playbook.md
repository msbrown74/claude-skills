# Compaction playbook

Goal: fewer bytes, same or better answers. Judge every change by whether a future reader would answer a question worse afterward.

## What to compact, and how

| Pattern | Do this |
|---|---|
| Layered "UPDATE" or "correction" blocks | Rewrite as one current-state statement. Keep a short "was X" only when it explains a decision or guards against a repeat mistake |
| Per-version histories and changelog narratives | Keep the current version and one line on the rule it taught; the full history belongs in the artifact's own changelog |
| Snapshots (balances, prices, counts, version inventories) | Replace with the roster or pointer plus how to refresh ("the live connector is authoritative", "highest SemVer in the folder is current") |
| Closed or resolved items, cleared flags | Remove, unless the resolution is itself a standing rule ("do not re-raise X") |
| Same fact at account and project level | Keep it where it is used; at most one pointer line elsewhere |
| Long how-to or workflow detail | Propose moving it into a skill or the artifact it describes; keep a one-line pointer |
| Verbose descriptions | One line, under 150 characters, naming the people, places and projects the file covers, with no sensitive terms |
| Multiple lines for one clause | Merge into one line, e.g., "likes A, B, C (favorite: B)" |
| Overlapping files with identical aliases | Merge into one file and union the aliases |
| Research output filed as memory | Propose removal; it is re-queryable and was not stated by the user |

## What not to compact

- Pinned lines: "asked to remember" items, IDs and confirmation numbers, contact details, policy and plan numbers, safety-relevant facts.
- The user's own qualifiers and reasons when they change how a rule applies ("because the spreadsheet is a draft").
- Standing "do not raise" rules and closed-item guards.
- Dates attached to decisions.
- Lines in `[observed]`, `[inferred]`, `(for=code)`, `[s:...]` or dated Claude Code formats.

## Promotion

- A rule that appears in two or more projects, in the user's words, can be proposed for the account-level preferences file. Propose it as tier C; never promote silently.
- A procedure the user repeats can be proposed as a skill. Offer to draft it; do not store the draft in memory.

## Retention ledger

Keep a table for every tier B change: source file and line, destination (file and line, or "dropped"), reason. Refer to lines by file and line number, never by quoting sensitive values. After writing, check every rewritten file against the ledger (line count and the set of tagged lines). If an entry has no destination and no reason, the change is not allowed.

## Rewriting a file

1. Read it, and note its version token.
2. Write the full new content in one operation: frontmatter, then lines, carrying unchanged lines word for word with their tags.
3. Update the frontmatter description if the file's subject changed; set `sources` to the union of what was there and `chat`.
4. Do not tag Claude-authored text as `[stated]`. A condensed line keeps `[stated]` only if its meaning is unchanged; otherwise ask.
5. Check the new size against the plan.
