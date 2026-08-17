# Rules

## 1. What counts as a noun

A noun is a thing in the territory that someone can point at and change:
a file, a class, a function that other things call, a config contract, a
data object, a folder that plays one architectural role. Not every file
is a noun worth a card — a noun earns a card when a later reader would
need to know it exists before touching something near it.

A noun is not a feeling about the codebase ("the messy part"), not a
process ("how deploys happen" — that is a walk order note, see
`reference/`, not a card), and not a wish ("the CLI we plan to build" —
that is a **ghost**, see rule 3, never written up as if it exists).

## 2. What counts as a movement

A movement is a real dependency: A reads B, A writes to a path B also
reads, A's output shape is consumed by B, A is imported by B, B's test
asserts something about A. If you cannot point to the actual line, import,
path, or call that makes the movement true, it is not a movement — it is
a guess, and guesses do not go in Hits/Does not hit.

## 3. Live, leftover, ghost

Every noun card is marked with exactly one status:

- **Live** — currently read, written, called, or imported by something
  else in force right now. Verify this by finding the actual
  reader/caller, not by the noun's name or its doc comment.
- **Leftover** — real, still present, still technically working, but no
  longer the intended shape (a rename left an old internal filename in
  place, a migration path nothing writes to anymore but that still
  parses fine if something did). Leftovers are honest: say what they are
  and why they're still there.
- **Ghost** — a name with no wiring. Referenced in a doc, a plan, a
  comment, or a variable name, but no file, function, or path actually
  backs it. Mapping a ghost as live is the single most damaging mistake
  a cartographer can make — the next reader will build on top of a wall
  that was never poured.

Never infer status from a name alone. A file called `legacy_ledger.py`
that three live modules still import is **live**, not a leftover, no
matter what its name suggests. Check the actual callers every time.

## 4. Hits / Does not hit

Every noun card that a reader might change carries both lines:

- **Hits:** — the other real nouns whose behavior changes if this one
  changes, each with the concrete reason (import, shared path, consumed
  return shape, asserted contract).
- **Does not hit:** — the neighbour a reader will *guess* is affected
  because it shares a name, a folder, or a vague theme with the noun in
  question, stated explicitly as *not* connected, with the reason why
  not (different constructor argument, disjoint output files, no
  import edge).

A card with only Hits and no Does-not-hit is a dependency list, not a
map — it never corrects the reader's first wrong guess, which is the
whole point of the line.

## 5. Cards cite the source, they do not copy it

A card names the file (path, and line numbers where useful), states in
your own words what the noun does and why it is shaped that way, and
stops. It never reproduces the function body, the full file, or long
verbatim blocks. If the card and the real file ever disagree, **the file
wins and the card is wrong** — cards are pointers with judgment attached,
not a second copy of the source.

## 6. Refuse to slurp the shelves

The catalog (`examples.md`'s catalog section, or a territory-specific
one you produce) is small and only points. It never contains the full
text of every card, and your instructions to a reader (`README.md`)
never say "load every card" or "add the whole folder to context." A
cold reader loads the catalog, opens the one card their question
actually points to, and stops. If they need a second card, that is a
second, deliberate hop — never a bulk load.

## 7. Walk order

Walk breadth-first from the territory's actual entry points (its own
README, its manifest/config files, its most-imported modules) inward.
Do not walk in file-tree alphabetical order — that produces a map shaped
by the filesystem instead of by how the territory is actually entered.
Record the walk order you used for a given territory in that territory's
`reference/` notes so a later cartographer pass can retrace it.

## 8. Naming collisions

Territories routinely reuse a word for two different things (the word
"Chat" naming both a UI component and a stored conversation object; the
word "journal" naming both a human-facing feature and an internal event
stream). Write every collision down explicitly in the territory's
`reference/` notes the moment you find one — a reader who doesn't know
about the collision will conflate the two nouns and every card built on
top of that reader's understanding degrades.
