---
name: craft-ui
description: Design engineering for building, directing, polishing, and reviewing UI. Use when designing or building interfaces, picking visual direction or a brand kit, comparing layout ideas, implementing motion, adding dark mode, making layouts responsive, fixing surfaces/type/color/copy, catching generated-looking UI, or shipping a final polish pass. Triggers on design, build UI, landing page, dashboard, brand kit, show me options, dark mode, make responsive, polish, feels off, micro-interaction, audit, quieter, distill, animate, gradient text, em dash.
---

# Craft UI

Working code is free. This is the judgment layer that decides whether an interface feels finished or generated. It sets a quality floor; it does not hand you a look. If every project comes out the same, you copied defaults instead of deciding.

User direction overrides everything below. Absent a clear ask otherwise, **correctness** is mandatory and **taste defaults** are starting points to adapt.

## Setup

1. **Route** with the [Intent map](#intent-map). Load only the listed files.
2. **Read the project** — tokens, theme, global CSS, or a representative component. Match that stack. Prefer existing components and tokens.
3. **Pick the register** — Brand (marketing/landing/portfolio: design IS the product) or Product (app/dashboard/tool: design SERVES the product). Task cue wins.
4. **Motion** — decide in [motion.md](./motion.md) before opening [transitions/catalog.md](./transitions/catalog.md).
5. **Ship** — walk the [Checklist](#checklist), run [Verify](#verify), fix misses. Reviews use Before / After / Why tables only.

Never load every file. Never open the catalog first.

## Intent map

| Intent | Load |
| --- | --- |
| Build UI, landing page, dashboard, new screen | [start-here.md](./start-here.md) if no direction yet, then only the floor files the work touches |
| Shape / plan / from a brief | [start-here.md](./start-here.md) |
| Brand kit / visual identity | [start-here.md](./start-here.md#brand-kit) |
| Ideas / show options / compare layouts | [start-here.md](./start-here.md#ideas) |
| Polish / ship-ready | Checklist + [surfaces.md](./surfaces.md), [aesthetics.md](./aesthetics.md), [copy.md](./copy.md); others only for hits |
| Audit / review | Checklist + only files the findings touch |
| Animate / transition / micro-interaction | [motion.md](./motion.md), then [transitions/catalog.md](./transitions/catalog.md) if implementing |
| Dark mode | [color.md](./color.md#dark-mode), [surfaces.md](./surfaces.md#depth-from-shadow-not-borders) |
| Responsive / mobile | [surfaces.md](./surfaces.md#responsive) |
| Surfaces / radius / shadow / cards / spacing | [surfaces.md](./surfaces.md) |
| Forms / controls / nav / overlays / tables / empty states | [surfaces.md](./surfaces.md#forms-and-controls) (also nav, overlays, data, empty sections below it) |
| Type / wrapping / tabular | [typography.md](./typography.md) |
| Color / contrast / palette | [color.md](./color.md) |
| Quieter / less generated look | [aesthetics.md](./aesthetics.md), [copy.md](./copy.md) |
| Distill / simplify | [start-here.md](./start-here.md#3-critique-the-plan-against-generator-defaults), [aesthetics.md](./aesthetics.md), [copy.md](./copy.md) |
| Extract / reuse components | [start-here.md](./start-here.md#structure) |

Narrower intent wins when two could fit.

## Files

| File | Covers |
| --- | --- |
| [start-here.md](./start-here.md) | Register, plan, brand kit, ideas, structure, critique, build handoff |
| [surfaces.md](./surfaces.md) | Radius, depth, cards, spacing, responsive, forms, nav, overlays, data density, empty/loading |
| [typography.md](./typography.md) | Hierarchy, wrapping, smoothing, tabular nums, tracking, truncation |
| [motion.md](./motion.md) | Animate-or-not, easing, duration, enter/exit, stagger, press, springs, a11y |
| [color.md](./color.md) | Contrast, focus, palette, dark mode |
| [aesthetics.md](./aesthetics.md) | Named generated-UI tells |
| [copy.md](./copy.md) | Hero anatomy, kicker, CTA, microcopy |
| [transitions/catalog.md](./transitions/catalog.md) | Eighteen paste-ready CSS transitions + [`_root.css`](./transitions/_root.css) |

## Floor

**Correctness (bugs if broken):** no `transition: all`; animate `transform`/`opacity` for movement; `prefers-reduced-motion`; concentric radius; real hit areas; no em dashes in UI copy; contrast/focus/color-alone in [color.md](./color.md); layouts adapt mobile → desktop; dark mode is redesigned, not inverted.

**Taste defaults (adapt):** house ease-out `cubic-bezier(0.22, 1, 0.36, 1)`; press `scale(0.96)`; enter from `scale(0.95)` + opacity; single-hue wash; layered shadow rgba. Personality axes that should diverge across products: color, type, density, radius, motion character, layout.

**Do not ship unless explicitly asked:**

- `ease-in` on enter/exit; bounce/elastic as the house curve; `scale(0)` entrances; motion on keyboard / 100×/day actions
- Nested cards; cards as the default layout answer
- Default indigo/violet accents and gray/slate neutrals when the project has no such tokens
- Gradient text; gradient-square logos; multi-hue aurora; colored glow shadows; pill/eyebrow kickers; icon-in-colored-tile hero chrome; emoji as chrome
- Inter/Roboto/Arial as the unearned display face; cream/sand + terracotta + display serif as the unearned editorial default
- Em dashes; "No X, no Y, just Z"; hype without numbers
- Dark mode via invert / `filter: invert` on images; desktop-only layouts with no mobile path

**Defaults worth keeping:**

1. Decide whether to animate before how ([motion.md](./motion.md#1-should-this-animate-at-all))
2. Functional UI under 300ms; exits ~half the enter
3. Re-triggerable motion uses transitions, not keyframes
4. Lightest separation: whitespace → divider → card; outer radius = inner + padding
5. Gate hover behind `(hover: hover)`

**Cold test:** strip the logo. Could this belong to any other product in the category? If yes, return to [start-here.md](./start-here.md).

## Interaction states

Where the control exists: default, hover (fine pointer only), `:focus-visible`, pressed, disabled, loading, empty, error. Keep dimensions stable when labels or loading text change.

## Verify

- Desktop and narrow mobile both work; no horizontal page overflow
- Primary path covers the interaction states that apply
- No text overflow in buttons, cards, sidebars, compact panels
- Contrast and focus pass; every animation has reduced-motion handling
- Project tokens/components reused; no parallel system invented

## Reviewing

Markdown tables with **Before | After | Why**, one row per change, grouped by principle. Cite file and property when the snippet is unclear. Omit empty groups. No loose Before/After lines outside tables.

| Before | After | Why |
| --- | --- | --- |
| `transition: all 300ms` | `transition: transform 200ms var(--ease-out)` | Name exact properties |
| card nested in card | single surface | Nested cards are lazy hierarchy |
| light palette inverted for dark | redesigned surfaces, ring not drop-shadow | Invert is not dark mode |
| "go green — then roll it back" | comma or two sentences | Em dash reads as generated |

## Checklist

Direction
- [ ] Register chosen; anchoring matches it
- [ ] Not cream+serif+terracotta, dark+acid-green, or white+blue/violet SaaS unless briefed
- [ ] One signature element; passes the cold test; project tokens reused

Surfaces and type
- [ ] Concentric radii; lightest separation; no nested cards
- [ ] Optical alignment; layered shadow / dark rings; shadows not clipped
- [ ] Image outlines black/white at 10%; hit areas ≥40×40 (≥44 touch), non-overlapping
- [ ] Spacing rhythm (tight → group → section); headings balance; body pretty; root antialiased; tabular nums on updating numbers
- [ ] Heading weight medium/semibold; tracking tight only on large display
- [ ] Forms labeled; errors not color-alone; overlays not clipped; sensible z-stack
- [ ] Product density when register is product; empty/loading/error states covered
- [ ] Truncation planned where needed; no spilled button/chip text

Motion
- [ ] Justified; no keyboard/100×/day motion
- [ ] Strong ease-out; no ease-in; no bounce/elastic house curve
- [ ] Under 300ms; exits quicker; enter from 0.95; press 0.96
- [ ] Transitions for re-triggerable; popovers origin-aware
- [ ] transform/opacity only; no `transition: all`; reduced-motion; hover gated

Color, dark, responsive
- [ ] Body 4.5:1; large 3:1; placeholders 4.5:1; focus 3:1
- [ ] No washed gray on colored bg; no color-alone state
- [ ] Dark mode redesigns surfaces; shadows dropped or rings
- [ ] Mobile and desktop work; mobile nav when needed; inputs ≥16px on small screens

Aesthetics and copy
- [ ] No banned tells without an explicit ask
- [ ] No em/en dashes; no negation-triad; no hype without numbers
- [ ] Hero: one headline, ≤2-line subhead, one primary CTA naming an outcome
- [ ] Interaction states covered; Verify passed

---

*Craft UI by Nika Siradze. More at [nikusha.com](https://nikusha.com).*
