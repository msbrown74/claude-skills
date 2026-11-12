# Lessons from earlier runs

A full manual cleanup of about 69 files and 229 KB took five turns and ended at about 62 files and 167 KB (roughly 27% smaller). A later read-only test run against the cleaned store showed where the process needed tightening. Contents: what stores look like, mechanics that bit, findings from the test run, questions worth asking.

## What a store looks like after a few months of use

- **Stale facts after a change.** A participant dropped out of a plan and several files still listed them. A contract type changed and a naming rule still used the old term. A date differed by one day between two files.
- **Version rot.** Overview files listing "current" versions many versions behind later files. Fix: say "the highest SemVer in the folder is current" and keep only the latest seen.
- **Layered updates.** Files that grew by appending "UPDATE" blocks instead of rewriting. The largest file shrank from 24 KB to about 7 KB when rewritten as current state.
- **Duplicates across levels.** An account-level copy of a project file; several small notes with identical aliases that merged into fewer files.
- **Contradictory rules.** Project rules versus account defaults. Resolved with one precedence line, not file-by-file edits.
- **Guardrail-risk lines.** "Do not re-question my stated facts" and "do not tag statements as unverified" can read as instructions to suppress verification. Reword to "do not re-ask confirmed facts; mention once if a document contradicts one".
- **Hygiene.** Stray artifact lines (about 35), `name:` fields with a folder prefix, duplicated aliases, descriptions over 150 characters, unresolved flags the project said to purge.
- **One proper noun spelled several ways.** Resolved from the vendor's own document.
- **Snapshots.** Balances copied into memory while a live connector was the authoritative source. Replaced with a roster and caveats.

## Mechanics that bit

- **10 write operations per turn.** Hit repeatedly; the cleanup needed five turns. Plan batches, prefer full rewrites, stop at the cap and say what remains.
- **Writes can be accepted, then refused later by a content check.** A merge that removes its source after the destination write was "accepted" could lose data. Write the destination first, verify every rewritten file, remove sources last.
- **Files change between turns.** A background pass can edit a file after you read it. Re-read before editing.
- **Deletions are for explicit requests only.** Approval of a plan item counts; an unprompted tidy does not.
- **Frontmatter matters.** The listing shows descriptions and aliases; a wrong description hides a file from retrieval.
- **Do not store the cleanup.** Run logs and findings are not user-stated facts.

## Findings from the test run

- A seven-day freshness window made 35 of 63 files report-only on the day after a manual cleanup. A short window (24 hours) plus a fresh re-read before each write is enough; files touched in bulk will still look recent, so treat that as a flag only.
- Listing sizes and read sizes disagree by 3 to 14 percent; the listing truncates descriptions and aliases; updated dates are unreliable after backfills or bulk touches.
- Index files carry display names, so a name-versus-path check needs an exemption. Projects without an index file appear nameless.
- Imported or backfilled files may be untagged prose or tag everything as stated even when derived.
- Duplicate-identifier checks are noisy for shared contact details, which are pinned anyway.
- Duplicate and contradiction checks are judgment calls, not scripts.
- A full read of about 160 KB cost roughly 45k tokens.

## Questions that were worth asking

- Which of two conflicting statements is right, when the files give no way to tell.
- Whether two names are one person, or whether an item moved from in progress to submitted.
- Whether a rule is still live after the thing it governed ended.
- Which deletions are approved, as a checklist, not a paragraph.

## Questions that were not worth asking

- Anything a primary document could settle (check the vendor's file, the sender's email, the calendar first, with the user's go-ahead).
- Anything the user had already told you and closed.
