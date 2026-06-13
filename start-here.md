# Start here: from brief to UI

This is where UI work begins after a product brief, before you place a single div.
The rest of the skill is the quality floor. This file is what stops every project
from converging on the same generated look. If you skip it, you get a competent page
that could belong to any product, which is the thing we are trying to avoid.

Work in this order: anchor, plan, critique, build, review.

## 1. Anchor in the product's world

Read the brief and pull out the concrete subject matter: what this product actually
deals with, the artifacts it touches, the words its users use. Your visual and copy
choices come from that world, not from a default.

- The hero should lead with the most characteristic thing about this product, not a
  generic headline over two cards. A read-later magazine shows an issue's table of
  contents. A cron tool shows a real run table. A budget app shows the money.
- If two different briefs would produce the same screen from you, you haven't anchored
  yet.

## 2. Make a one-screen plan before building

Decide these up front, written down, so you're choosing instead of defaulting:

- **Palette.** One accent plus a neutral ramp, 4 to 6 values. Build neutrals from a
  slight warm or cool hue so surfaces have a temperature. Contrast targets in
  [color.md](./color.md) are non-negotiable.
- **Type.** A display face and a body face chosen for this brief, with a real scale
  and intentional weights. Type sets the personality before layout does. Don't reach
  for the same pairing every time.
- **Density.** Airy and editorial, or compact and dense. Pick on purpose.
- **Radius scale.** Sharp (about 4px) reads precise and technical; soft (16 to 24px)
  reads friendly. Choose one and hold it concentrically (see [surfaces.md](./surfaces.md)).
- **Motion character.** Crisp and minimal, or springy and alive. See [motion.md](./motion.md).
- **One signature element.** The single memorable, brief-justified thing. Spend your
  boldness here and keep everything around it quiet. Cut decoration that doesn't
  serve the brief.

## 3. Critique the plan against the defaults

Before building, check the plan against the looks a generator reaches for when nobody
decided anything. If any axis matches one of these and the brief didn't ask for it,
change it and justify the change.

The defaults to catch yourself reaching for:

- **Warm cream background, high-contrast serif, terracotta accent.** The "tasteful
  editorial" default.
- **Near-black background, one bright acid-green or vermilion accent.** The "technical
  dark mode" default.
- **White page, blue or violet accent, hero over two rounded cards, a pill kicker with
  a dot.** The "generic SaaS" default.

None of these are banned. They're only a problem when they show up because no choice
was made. If the brief genuinely calls for warm editorial, do warm editorial well,
and make it specific enough that it couldn't be swapped onto another product.

Also check: **does the complexity match the vision?** A maximalist concept needs
elaborate execution; a minimal one needs precision in spacing, type, and detail.
Elegance is executing the chosen direction well, not piling on features to justify it.

## 4. Build on the quality floor

Now bring in the rest of the skill: [surfaces.md](./surfaces.md),
[typography.md](./typography.md), [motion.md](./motion.md), [color.md](./color.md),
[aesthetics.md](./aesthetics.md), [copy.md](./copy.md), and the
[transitions catalog](./transitions/catalog.md). These don't dictate the look; they
keep the execution from being sloppy.

## 5. Review

Run the checklist in [SKILL.md](./SKILL.md). Then ask the one question that matters
most: if you showed this to someone cold, would they know which product it is, or
could it be anyone's? If it's anyone's, go back to step 1.
