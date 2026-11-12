# Report and plan format

Conclusion first. Short. Tables for scanning. Evidence is "category + file + line", never a sensitive value (SKILL.md rule 7).

```
## Memory Dream report (YYYY-MM-DD, mode: full | report-only | scoped)

**Conclusion:** [one or two sentences: overall health, how much can be saved, what needs the user]

**Coverage:** [files listed and read; anything not read and why]
**Store:** N files, X KB by listed bytes (largest: file A, file B). HOT (changed in the last 24 hours): N.
**Findings:** N items after grouping, which equals a + b + c + d (tier A, B, C, D). "Possibly settled" items are listed separately and not counted. Severity split: high H, medium M, low L.
**Estimated result:** about N files and X to Y KB (roughly P% smaller). The exact ledger is built at apply time.

### High and medium findings
| ID | Check | Files | Evidence (category + file + line) | Severity |
|---|---|---|---|---|
| C1 | C-01 | ... | one line | high |

Each item's proposal appears once, in its tier section below.

### Tier A: format fixes (approve as a batch)
- A1 ...

### Tier B: meaning-preserving changes (approve by ID or as a batch)
| ID | File | Change | Size range | Notes |
|---|---|---|---|---|
| B3 | ... | merge X into Y | ... | source removal is C4 |

### Tier C: your call (questions)
- **C1: [question]**
  - Option 1 (recommended): ...
  - Option 2: ...
  - Other
- **C4: remove source of merge B3** (applied only after B3 is verified)

### Tier D: report only
- D1 ...

Mark any item on a HOT file with "HOT"; it needs its own ID in your reply.

### Possibly settled open items (listed once)
- file: line summary

### Write plan
Batch 1 (turn 1): ops 1-10 ... Batch 2: ... One rewrite per file. Source removals come last.
Backup file: `YYYY-MM-DD Backup - Memory` will be sent before the first write.

**Reply with:** "apply A", "apply A and B", "apply all" (every A and B item plus any C you have answered; never D; never HOT items), named IDs (e.g., "B2, B5, C1=1, C4"), or "report only".
```

Unattended or report-only runs end after the findings and questions, with this closing line: "To act on this, open a chat and say 'run memory dream'. That run re-reads the store, re-numbers the items and asks again."

Close-out report after applying:

```
## Memory Dream complete
Before → after: files, KB. Changes by tier. Ledger exceptions: none | list.
Pending (source removals, cap leftovers): ...
Needs another turn: ...
Suggested follow-ups (not done): ...
```

Formatting notes: put recommended options first; keep each finding's evidence to one line; group low-severity items by check; do not paste sensitive values; do not add an audit, confidence or changelog section to any saved file.
