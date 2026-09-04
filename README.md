# The Alchemist's Ledger

**[7mxdie.github.io/alchemists-ledger](https://7mxdie.github.io/alchemists-ledger/)**

An alchemy recipe finder for modded Skyrim. It answers one question:

> **What should I combine?**

Cast a power in game, drop the file it writes onto the page, and every 2- and
3-ingredient recipe your load order can produce gets ranked — starting with the
ones you can brew right now, from the ingredients in your pack.

It works with **any** load order, because the data comes from your own game
rather than a curated list. There is nothing to configure: whatever mods you
have installed is what you see.

---

## How to use it

1. Install the companion mod *(link to follow — not yet released)*
2. Cast **Record the Ledger**, under Magic → Powers
3. Drop `AlchemistsLedger.json` onto the page

You will find the file in `Data/SKSE/Plugins/StorageUtilData/` inside your
Skyrim folder. Mod Organizer 2 writes it to
`overwrite/SKSE/Plugins/StorageUtilData/` instead. Ignore the file with
`DO_NOT_UPLOAD` in its name — that one is the mod's own cache.

The first cast on a new load order takes about a minute while it reads every
ingredient. After that it is instant, and it rebuilds itself whenever you
change your mods.

Nothing is uploaded. The page reads the file in your browser and never sends it
anywhere.

---

## What you get

**Your Ledger** — the best recipes you can make right now, from what you are
carrying. This is where it opens.

**All Recipes** — everything your load order allows, whether or not you have
the ingredients.

**Ingredients** — every ingredient in your game, what it does, and how many you
are carrying.

### Three ways to rank

| | |
|---|---|
| **Potency** | How strong the recipe is. |
| **Per ingredient** | Potency divided by how many reagents it costs, so a strong two-ingredient recipe beats a slightly stronger three-ingredient one. |
| **Yield** | Potency multiplied by how many you could actually brew. Ten weak potions are often worth more than one strong one. |

Click a column header to sort by it, and again to reverse it. Sorting re-runs
the whole search rather than reshuffling what is on screen, so it genuinely
finds the best recipe by that measure.

### One ingredient away

Your Ledger also tells you what to go and find: the single ingredient that
would unlock your best new recipe, and what it would be worth compared to the
best you can brew today.

### Recipes where the third ingredient is pointless

A great many three-ingredient recipes are just a good pair plus a passenger. If
the third ingredient changes the result by less than 10%, the recipe collapses
into its pair and lists the discarded thirds with what each was actually worth.
Nothing is hidden — you can open it and see all of them.

---

## Potency

Potency ranks a recipe by its **inherent** strength. It deliberately ignores
your Alchemy skill, perks and Fortify Alchemy gear.

That is on purpose. If it counted your gear, the ranking would change every
time you swapped a ring, and it would be different for every character. Leaving
it out means one ranking that is true for everyone and stays true as you level.

**Your game will show a bigger number, and that is expected.** Skyrim starts
from the same effects and then applies everything about your character on top.
Potency is not gold value and not your final potion strength. Use it to decide
what to combine; use your alchemy menu to see what you actually get.

---

## Two ingredients with the same name

Modded load orders routinely contain several different ingredients sharing a
display name. On one reference load order, 28 names covered 61 distinct
records — five of them called *Goliath Grouper Scales*, with five entirely
different effect sets.

Where two records are genuinely interchangeable they are merged. Where they are
not, they are shown separately with their source plugin and their strongest
effects, because merging them would build recipes from the wrong one.

Effects are matched on magic-effect record identity, never on display name, for
the same reason.

---

## How it is built

One `index.html`. No build step, no framework, no dependencies, no backend, no
tracking, no bundled data. Ranking runs in a Web Worker so the page stays
responsive while it works through several hundred thousand combinations.

The page needs to be served over http — it reads files, so opening it from disk
will not work.

---

## Licence

MIT — see [LICENSE](LICENSE).

Skyrim and its data belong to Bethesda Softworks. This is an unofficial fan
tool, not affiliated with or endorsed by Bethesda or by the authors of any mod
whose data it reads.
