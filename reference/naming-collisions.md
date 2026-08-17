# Reference: naming collisions in this territory

Per `rules.md` rule 8. Found while walking AgentSwarm's dispatch layer
for `examples.md`.

## "Checker" (a role name vs. a removed mechanism)

`roles.json` has a live entry literally named `checker_hermes` — a real,
reachable role. The module docstring in `orchestrate.py` separately talks
about "no configured checker model" and a removed `run_checker` function
(see the **ghost card** in `examples.md`). These are not the same thing:
`checker_hermes` is a normal worker role like any other coder role, while
the docstring's "checker" is a description of an old, now-removed design
where checking judgment lived in Python rather than in the driving Claude
session. Reading `checker_hermes` in `roles.json` and assuming it wires
up to whatever the docstring's "checker" discussion describes would be
wrong — trace the actual dispatch instead (`call()`, per the worked
example) rather than pattern-matching on the word.

## "Provider" (a `roles.json` field vs. the Hermes CLI's own `--provider` flag)

Every `roles.json` entry has a `"provider"` key — but for entries with
`"provider": "hermes"`, there is a *second*, unrelated provider concept
one level down: `hermes_provider` (e.g. `"google"`, `"nvidia"`), which
becomes the Hermes CLI's own `--provider` flag. `call()`'s `"provider"`
picks which Python client module handles the request
(`hermes_client.py` vs `or_client.py` vs `gemini_client.py`); the
role's `hermes_provider` (only meaningful when the outer `"provider"` is
`"hermes"`) picks which upstream service Hermes itself talks to. Two
different routing decisions, same word, one level of nesting apart.
