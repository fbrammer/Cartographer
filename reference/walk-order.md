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

## This territory (AgentSwarm's dispatch layer), as walked for `examples.md`

1. Entry point: `orchestrate.py`'s `call()` function — every subcommand
   (`cmd_run`, `cmd_retry`, `cmd_refresh_apply`'s `call_fn`) routes
   through it, making it the true front door regardless of which
   subcommand a reader invokes first.
2. Outward to what `call()` can branch to: `hermes_client.py`,
   `or_client.py`, `gemini_client.py` — found by reading the branch
   itself (`orchestrate.py:46-53`), not by trusting the module
   docstring's role list, which only describes the free-tier roles in
   prose and doesn't enumerate the code branches.
3. Sideways to `roles.json`, reached because it's the thing that decides
   which branch actually fires — read directly (grepped every
   `"provider"` value) rather than trusting AGENTS.md's description of
   it, which is what surfaced the live/leftover split: all 11 entries
   say `"hermes"`, so two of the three branches found in step 2 are
   currently unreached.
4. One item surfaced during this walk that wasn't the destination of an
   edge at all: `run_checker`, noticed only because the module docstring
   (read in full while orienting on `call()`) names it and a grep found
   no matching function anywhere in the file — filed as a **ghost**
   rather than silently dropped.
