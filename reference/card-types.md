# Reference: card types

The closed set of card shapes this cartographer produces. Every card in
`examples.md`, or in any territory-specific map produced from this
folder, is one of these. Don't invent a sixth shape mid-map.

## Noun card

The default. One real, addressable thing: a file, a class, a contract, a
data object. Always carries:

- **Source** — path, and line numbers/symbol name where useful.
- **Status** — Live / Leftover / Ghost (see `rules.md` rule 3).
- **Body** — what it is and why it's shaped that way, in the
  cartographer's own words, short.
- **Hits** — real, checkable downstream effects (rule 4).
- **Does not hit** — the guessable-but-wrong neighbour, and why not
  (rule 4). Omit only for a card nothing in the territory would ever
  plausibly change (rare — most nouns get this line).

## Ghost card

A noun card with no working **Source** to point to — the source line
instead says where the *name* comes from (a doc, a comment, a plan) and
states plainly that nothing backs it yet. No Hits/Does not hit section;
a ghost has no live behavior to propagate.

## Collision note

Not a noun card. A short paragraph, filed under `reference/`, naming two
different things in the territory that share a word, and which is which.
Referenced from any noun card where the collision is relevant, rather
than re-explained inline every time.

## Catalog

Not a card. The single small table at the top of a map: one row per
card, its one-line identity, and its status. This is the only thing a
cold reader loads before choosing a door.
