# Reference: walk order

Per `rules.md` rule 7, walk from real entry points inward, and record the
order used so a later pass can retrace it.

## General procedure

1. Find the territory's own stated entry points first: its README, its
   manifest/config file (`package.json`, `pyproject.toml`, `plugin.yaml`,
   a vault's index note), whatever a fresh reader would open first.
2. From each entry point, follow real edges outward one hop at a time —
   an import, a path both files touch, a hook registration — not the
   filesystem's alphabetical order.
3. Stop widening once you've covered the objects a reader would actually
   need before making the kind of change the map is for. A map is not
   obligated to reach 100% file coverage; it is obligated to cover the
   objects that matter for entry and change.
4. Any node you touch but choose not to card (too minor, purely internal,
   no external readers) gets a one-line mention in a collision note or is
   silently folded into its parent's card — never left dangling as an
   implied-but-uncarded reference.

## This territory (FamilyAI journal + session-state), as walked for `examples.md`

1. Entry point: `familyai-workspace` plugin's `register()` /
   `on_session_start` hook (`__init__.py`) — this is what every session
   actually executes first.
2. Outward to what that hook calls: `bootstrap()` and `load_contract()`
   in `workspace_bootstrap.py` → the **workspace contract** card.
3. Outward again to what the contract's *consumer* (`build_directive()`)
   reads, and separately to what `bootstrap()` itself constructs
   (`JournalStore`) → the **JournalStore** card.
4. Sideways from JournalStore to the second class living in the same
   source file (`SessionLogStore`) — found by reading the file, not by
   assuming one class per file.
5. Sideways again to the **session ledger** (`ledger.py`), reached
   because `session-log`'s `SKILL.md` names it as what the skill
   watches — not because it shares a folder with anything already
   walked.
6. Two items surfaced during this walk that weren't destinations of an
   edge at all: the `auto_journal.py` filename (noticed while reading
   `session-log`'s directory listing) and the `familyai journal` CLI
   (noticed only because prior planning notes named it and a grep found
   nothing) — filed as **leftover** and **ghost** cards respectively
   rather than silently dropped.
