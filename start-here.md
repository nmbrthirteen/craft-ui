# Start here: from brief to UI

Use this file when the work starts from a product brief, before any markup. The rest of the skill is the quality floor. Skipping this is how every project converges on the same generated look.

Work in order: **anchor → plan → critique → build → review.** Write the plan down before you build. Do not jump to components.

## 1. Anchor in the product's world

Extract the concrete subject matter: what the product deals with, the artifacts it touches, the words users use. Visual and copy choices come from that world.

- Lead the hero with the most characteristic thing about this product, not a generic headline over two cards. A read-later magazine shows an issue TOC. A cron tool shows a real run table. A budget app shows the money.
- Failure check: if two different briefs would produce the same screen, you have not anchored yet. Restart this step.

## 2. Write a one-screen plan

Decide these before placing a div:

- **Palette.** One accent + neutral ramp, 4 to 6 values. Neutrals from a slight warm or cool hue. Contrast targets in [color.md](./color.md) are non-negotiable.
- **Type.** Display + body chosen for this brief, with a real scale and weights. Do not reuse the same pairing every time.
- **Density.** Airy editorial, or compact dense. Pick on purpose.
- **Radius scale.** Sharp (~4px) = precise/technical; soft (16–24px) = friendly. Hold it concentrically ([surfaces.md](./surfaces.md)).
- **Motion character.** Crisp/minimal, or springy/alive ([motion.md](./motion.md)).
- **One signature element.** The single memorable, brief-justified thing. Spend boldness there. Cut decoration that does not serve the brief.

## 3. Critique the plan against generator defaults

If any axis matches a default below and the brief did not ask for it, change it and state why.

- **Warm cream + high-contrast serif + terracotta.** "Tasteful editorial" default.
- **Near-black + acid-green or vermilion.** "Technical dark mode" default.
- **White + blue/violet + hero over two rounded cards + pill kicker with a dot.** "Generic SaaS" default.

These are not banned when earned. They are banned when they appear because nobody chose. Complexity must match the vision: maximalist concepts need elaborate execution; minimal ones need precision in spacing and type.

## 4. Build on the quality floor

Load only what the work touches: [surfaces.md](./surfaces.md), [typography.md](./typography.md), [motion.md](./motion.md), [color.md](./color.md), [aesthetics.md](./aesthetics.md), [copy.md](./copy.md), [transitions/catalog.md](./transitions/catalog.md). These keep execution from being sloppy; they do not pick the look.

## 5. Review

Run the checklist in [SKILL.md](./SKILL.md). Final gate: shown cold, would someone know which product this is? If it could be anyone's, return to step 1.
