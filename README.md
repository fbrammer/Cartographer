# Cartographer

A drop-in Claude project folder that turns an AI into a **cartographer**:
something that walks a real, live body of work — a repo, a vault, a
delivery folder, an automation pack — and leaves behind a small, walkable
map instead of a tour, an audit, or a second copy of the source.

Built for [Clief Notes Weekly Comp #11: The Cartographer](https://www.skool.com/cliefnotes/weekly-comp-11-the-cartographer).
Hand-built against the brief this round — no [ICM Architect skill](https://github.com/RinDig/icm-architect)
invocation in this pass.

## The one rule

**Load the catalog, then one card. Never the whole folder.**

If you find yourself telling the model (or a person) to add every file in
this project to context, you've broken the one thing this whole approach
exists to prevent. See `rules.md` rule 6.

## What's in this folder

| File | Job |
|---|---|
| `identity.md` | Who the cartographer is, what it walks, who the later reader is |
| `rules.md` | What counts as a noun/movement, live/leftover/ghost, Hits/Does-not-hit, the no-copy and no-slurp rules, walk order |
| `examples.md` | One worked map of a real territory — AgentSwarm's dispatch layer — with a catalog, five cards, and a real Hits/Does-not-hit example |
| `reference/card-types.md` | The closed set of card shapes (noun card, ghost card, collision note, catalog) |
| `reference/walk-order.md` | The general walk procedure, plus the exact order used for the worked example |
| `reference/naming-collisions.md` | The specific word-collisions found in the worked example's territory |

Each file does one job. Don't fold `rules.md` into `identity.md`, don't
inline the worked example into the README — a reader who only needs one
of these should be able to open exactly that one.

## How to use this

1. **Drop this whole folder into a Claude project** (or point a Claude
   Code / Hermes session at it directly — no packaging step required).
2. **Tell the cartographer what territory to walk**, and be specific:
   not "map my repo," but "map the objects a new contributor needs before
   touching `<specific folder>`." Say who the later reader is — if it's
   another model, say so; the brief in `identity.md` is written to expect
   that as the common case.
3. **The cartographer reads `identity.md` and `rules.md` first**, then
   walks the named territory per `rules.md` rule 7 (real entry points
   outward, not alphabetical), and produces a catalog + noun cards
   shaped like `examples.md` — for the new territory, not a repeat of
   the worked example.
4. **A cold reader (human or model) then uses the output** by loading the
   catalog, picking the one card their question points to, opening it,
   and stopping. If their next question needs a second card, that's a
   second deliberate hop — the map is never bulk-loaded.

## How to tell if the output is actually a map

Per the comp's own bar — a stranger or a cold model, given only the
output, should be able to:

- Find the front door from the catalog alone.
- Open one card and know what the thing is, and why it's shaped that way.
- Know what else moves if they change it, and the obvious wrong neighbour
  it does *not* move.
- Stop, without loading the rest.

If instead the output reads start-to-finish like a story of how the
project went, it's a tour. If it's a list of everything wrong, it's an
audit. If it explains why something failed, it's a diagnosis (last
week's form, not this one). If it's the source rewritten in nicer prose,
it's a photocopy. None of those are this.

## Worked example, in short

`examples.md` maps five real objects in `Projects/AgentSwarm`'s dispatch
layer — the `call()` provider router, `roles.json`, the one provider
client every current role actually reaches, two documented-as-leftover
provider clients that are wired in but currently unreferenced by any
role, and one genuine ghost (`run_checker`, named in the module's own
docstring, grep-confirmed to not exist anywhere in the file). The later
reader is a fresh model session picking up AgentSwarm to dispatch a task
with no memory of how the provider routing evolved — the actual,
recurring reader for this territory.
