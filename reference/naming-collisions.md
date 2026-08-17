# Reference: naming collisions in this territory

Per `rules.md` rule 8. Found while walking FamilyAI's journal +
session-state subsystem for `examples.md`.

## "Journal" (two things)

- **The human journal** — the `journal` trigger word, `JOURNAL.md`,
  `entries/`, `index.jsonl`, owned exclusively by `JournalStore`
  (`scripts/journal/journal_store.py:57`).
- **`journal_state`** — a key inside the workspace contract dict
  (`workspace_bootstrap.py:53`), pointing at `<root>/Journal/state` — a
  *directory*, not the human journal itself. It's the parent of both
  `state/sessions/` (session ledger) and `state/session-log/`
  (SessionLogStore's output), neither of which is "the journal" in the
  human-trigger sense.

A reader who sees `journal_state` in the contract and assumes it means
"where JournalStore writes" will misread every card downstream of it.

## "Session log" vs "session ledger" (two things, one folder apart)

- **Session ledger** — `ledger.py`'s raw per-session event file,
  `<state>/sessions/<session_id>.ledger.json`.
- **Session log** — the human-readable milestone narrative,
  `<state>/session-log/SESSION-LOG.md` (+ `session-log.jsonl`), produced
  by `SessionLogStore` *from* the ledger's events.

The ledger is upstream data; the log is the derived narrative. Renaming
one skill folder to "session-log" (from "auto-journal") makes this pair
sound even more alike than before — worth restating any time both are
mentioned in the same card.

## `journal_store.py` (one file, two classes)

`scripts/journal/journal_store.py` defines both `JournalStore` (line 57)
and `SessionLogStore` (line 192). A diff or a commit message that just
says "changed journal_store.py" tells you nothing about which of the two
disjoint output-file sets actually moved — check which class the diff
touches before assuming either card in `examples.md` is affected.
