# Start here: from brief to UI

Use this for direction, brand kits, comparing ideas, or any work that starts from a product brief before markup. The rest of the skill is the quality floor. Skipping this is how every project converges on the same generated look.

Work in order: **register → anchor → plan → critique → build → review.** Write the plan down before you build. Do not jump to components.

## 0. Pick the register

- **Brand** (marketing, landing, portfolio): design IS the product. Hero discipline, signature element, composition first.
- **Product** (app UI, dashboard, tool): design SERVES the product. Density, clarity, crisp motion, quiet chrome. Status and actions beat marketing furniture.

Task cue wins. A marketing site *for* a SaaS product is brand; the app behind login is product. Design them separately. Product surfaces follow [surfaces.md](./surfaces.md#data-and-product-density); brand surfaces follow hero and copy rules harder.

## 1. Anchor in the product's world

Extract the concrete subject matter: artifacts, words users use, what the product actually deals with.

- Lead the first viewport with the most characteristic thing about this product, not a generic headline over two cards.
- Failure check: if two different briefs would produce the same screen, re-anchor.
- Cold test: strip the logo. Could this belong to any other product in the category? If yes, re-anchor.

## 2. Write a one-screen plan

Decide before placing a div:

- **Palette.** One accent + neutral ramp, 4 to 6 values. Neutrals from a slight warm or cool hue. Never default indigo/violet + gray/slate unless the project already owns them. Contrast in [color.md](./color.md) is non-negotiable.
- **Type.** Display + body for this brief, real scale, at most two weights on a view. Do not reuse the same pairing every time.
- **Density.** Airy editorial, or compact dense.
- **Radius scale.** Sharp (~4px) = precise; soft (16–24px) = friendly. Hold concentrically ([surfaces.md](./surfaces.md)).
- **Motion character.** Crisp/minimal, or springy/alive ([motion.md](./motion.md)).
- **One signature element.** Spend boldness there. Cut decoration that does not serve the brief.
- **Depth strategy.** One technique per view: whitespace, dividers, soft shadow, or surface shift — not all at once.

## Brand kit

When asked for a brand kit or visual identity from a product idea, output a **decision board**, not only swatches:

1. One-sentence visual thesis (mood, material, energy)
2. Palette as CSS variables (bg, surface, ink, muted, accent) with roles
3. Type pairing + scale + weights
4. Spacing rhythm, radius, depth strategy
5. Layout pattern for the primary surface (and register)
6. Two short scene descriptions of how the brand looks in real UI (e.g. marketing hero + one product moment)

If image generation is available, optionally render a board with two mockups. Text-only is enough to hand off to build. Then continue from step 3.

## Ideas

When asked for options / "show me 3" / compare layouts:

1. Produce 2–3 **genuinely different** directions (composition, not just accent hue). Label them.
2. Each option gets a one-line thesis + the plan axes that change.
3. Prefer implementing light variants in the real project for browser comparison when possible; otherwise describe clearly enough to choose.
4. Ask which to keep (or which combo). Build only the chosen direction through steps 3–5.

Do not ship three near-identical indigo heroes.

## Structure

When extracting or cleaning UI code:

- Match the project's existing component patterns, file layout, and naming.
- Reuse shared components before inventing new ones.
- Extract repeated sections and self-contained blocks; keep props flexible, not one-off.
- Preserve layout and behavior; this pass is structural, not a redesign.
- Prefer the project's class/token conventions; do not introduce a parallel styling system.

## 3. Critique the plan against generator defaults

If any axis matches a default below and the brief did not ask for it, change it and state why.

- **Warm cream + high-contrast serif + terracotta.** "Tasteful editorial" default.
- **Near-black + acid-green or vermilion.** "Technical dark mode" default.
- **White + blue/violet + hero over two rounded cards + pill kicker with a dot.** "Generic SaaS" default.

None banned when earned. Banned when they appear because nobody chose.

## 4. Build on the quality floor

Load only what the work touches: [surfaces.md](./surfaces.md), [typography.md](./typography.md), [motion.md](./motion.md), [color.md](./color.md), [aesthetics.md](./aesthetics.md), [copy.md](./copy.md), [transitions/catalog.md](./transitions/catalog.md). Match the project's framework and components.

## 5. Review

Run the checklist and Verify gate in [SKILL.md](./SKILL.md). Final question: shown cold, would someone know which product this is? If it could be anyone's, return to step 1.
