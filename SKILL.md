---
name: craft-ui
description: Go-to design engineering skill for building, directing, polishing, and reviewing UI. Use when designing or building interfaces, picking visual direction or a brand kit, comparing layout ideas, implementing motion, adding dark mode, making layouts responsive, fixing surfaces/type/color/copy, catching AI slop, or shipping a final polish pass. Triggers on design, build UI, landing page, dashboard, brand kit, show me options, dark mode, make responsive, polish, feels off, micro-interaction, audit, quieter, distill, animate, gradient text, em dash.
---

# Craft UI

The go-to skill for design engineering: direction, build, motion, dark mode, responsive, anti-slop, and ship review. Working code is free. This is the judgment layer that stops the result from reading unfinished or generated. It guarantees a quality floor; it does not hand you a look. If every project comes out the same, you copied defaults instead of deciding.

User direction overrides everything below. Absent a clear ask otherwise, treat **correctness** as non-negotiable and **taste defaults** as the starting point to adapt.

## Setup (do before designing)

You MUST do these in order.

1. **Route the ask** with the [Intent map](#intent-map). Load only those files.
2. **Read the project.** Open tokens, theme, global CSS, or a representative component. Match that stack. Prefer existing components and tokens.
3. **Pick the register.** Marketing / landing / portfolio = design IS the product. App / dashboard / tool = design SERVES the product. Task cue wins.
4. **Decide before paste.** Motion: [motion.md](./motion.md) before [transitions/catalog.md](./transitions/catalog.md).
5. **Ship gate.** Walk the [Review checklist](#review-checklist), run [Verify](#verify), fix misses. Reviews ship only as Before / After / Why tables.

Never load all satellites at once. Never open the catalog first.

## Intent map

| Intent / synonyms | Route | Load |
| --- | --- | --- |
| `design`, build UI, landing page, dashboard, new screen | Build | [start-here.md](./start-here.md) if no direction yet, then floor files the work touches |
| `shape`, plan, from a brief, redesign from scratch | Direction | [start-here.md](./start-here.md) |
| `brand kit`, visual identity, brand direction | Brand kit | [start-here.md](./start-here.md) brand-kit section |
| `ideas`, options, show me 3, compare layouts | Ideas | [start-here.md](./start-here.md) ideas section, then build the chosen one |
| `polish`, final pass, ship-ready | Polish | Checklist + [surfaces.md](./surfaces.md), [aesthetics.md](./aesthetics.md), [copy.md](./copy.md); others on hits |
| `audit`, review, critique, what is wrong | Review | Checklist + only satellites findings touch |
| `animate`, transition, micro-interaction, hover/press | Motion | [motion.md](./motion.md), then catalog if implementing |
| `dark mode`, dark theme, prefers-color-scheme | Dark mode | [color.md](./color.md) dark-mode section + [surfaces.md](./surfaces.md) depth rules |
| `responsive`, mobile, breakpoints, make this work on phone | Responsive | [surfaces.md](./surfaces.md) responsive section |
| surfaces, radius, shadow, hit area, cards, spacing, section layout | Surfaces | [surfaces.md](./surfaces.md) |
| `typeset`, type, wrapping, tabular | Type | [typography.md](./typography.md) |
| `colorize`, contrast, focus ring, palette | Color | [color.md](./color.md) |
| `quieter`, less slop, too loud, generic AI look | Anti-slop | [aesthetics.md](./aesthetics.md), [copy.md](./copy.md) |
| `distill`, simplify, too much chrome | Distill | [start-here.md](./start-here.md) critique + [aesthetics.md](./aesthetics.md) + [copy.md](./copy.md) |
| `componentize`, extract components, clean up classes | Structure | Match project component patterns; reuse before inventing; keep layout/behavior identical |

If two intents fit, pick the narrower one. If none fit, apply hard rules + register, load satellites only when a detail comes up.

## Correctness vs taste

- **Correctness (always).** No `transition: all`; animate `transform`/`opacity` for movement; `prefers-reduced-motion`; concentric radius; real hit areas; no em dashes in UI copy; contrast/focus/color-alone in [color.md](./color.md); responsive from mobile up; dark mode is designed, not inverted.
- **Taste defaults (adapt).** Exact shadow rgba, house ease-out, `scale(0.96)` on press, single-hue wash. A playful product and a precise dashboard should not share the same numbers.

Personality axes: color, type, density, radius, motion character, layout.

## Absolute bans

Do not ship these unless the user explicitly asked:

- `transition: all`; `ease-in` on UI enter/exit; bounce/elastic as the house curve
- `scale(0)` entrances; motion on keyboard / 100×/day actions
- Nested cards; cards as the default layout answer
- Default indigo/violet accents and gray/slate neutrals when the project has no such tokens
- Gradient text; gradient-square logos; multi-hue aurora; colored glow shadows
- Pill/eyebrow kickers and icon-in-colored-tile hero chrome
- Emoji as product chrome; Inter/Roboto/Arial as the unearned "designed" display face
- Em dashes; "No X, no Y, just Z"; hype without numbers
- Cream/sand body + terracotta + display serif as the unearned editorial default
- Dark mode as simple invert; CSS `filter: invert` as the final image treatment
- Desktop-only layouts with no mobile path

## AI slop cold test

Strip the logo. Could this screen belong to any other SaaS/tool shipped this year? If yes, return to register + [start-here.md](./start-here.md). Fixing radius on a generic composition is not craft.

## Interaction states (always cover)

Where the control exists, ship: default, hover (pointer fine only), `:focus-visible`, pressed/active, disabled, loading, empty, error. Keep control dimensions stable when labels, counts, or loading text change.

## Verify

Before calling the work done:

- Desktop and a narrow mobile width both work; no horizontal page overflow
- Primary path exercises the interaction states that apply
- Text does not overflow buttons, cards, sidebars, or compact panels
- Contrast and focus rules pass; motion has reduced-motion handling
- Project tokens/components reused; no parallel design system invented

## Quick reference

| File | Covers |
| --- | --- |
| [start-here.md](./start-here.md) | Direction, brand kit, ideas, brief → build → review |
| [surfaces.md](./surfaces.md) | Radius, optical alignment, depth, cards vs whitespace, spacing rhythm, section layout, responsive, hit areas |
| [typography.md](./typography.md) | Hierarchy, wrapping, smoothing, tabular nums, tracking |
| [motion.md](./motion.md) | Animate-or-not, easing, duration, enter/exit, stagger, press, springs, gestures, perf, a11y |
| [color.md](./color.md) | Contrast, focus, palette taste, dark mode |
| [aesthetics.md](./aesthetics.md) | Named AI-slop tells |
| [copy.md](./copy.md) | Hero anatomy, kicker, CTA, microcopy bans |
| [transitions/catalog.md](./transitions/catalog.md) | Eighteen paste-ready CSS transitions + [`_root.css`](./transitions/_root.css) |

## Non-negotiables

1. **Decide whether to animate before how.** Keyboard / 100×/day: no animation. See [motion.md](./motion.md#1-should-this-animate-at-all).
2. House ease-out: `cubic-bezier(0.22, 1, 0.36, 1)`. Never `ease-in` on UI. No bounce/elastic house curve.
3. Functional UI under 300ms. Exits ~half the enter.
4. Enter from `scale(0.95)` + opacity, never `scale(0)`. Press: `scale(0.96)`, never below `0.95`.
5. Re-triggerable motion: CSS transitions, not keyframes.
6. Animate `transform`/`opacity` only for movement. No `transition: all`. Always `prefers-reduced-motion`. Gate hover behind `(hover: hover)`.
7. Outer radius = inner + padding. Lightest separation that works (whitespace → divider → card). Never nest cards.
8. No emoji chrome; no gradient text; no gradient-square logos; no neon glow shadows.
9. No em dashes; no negation-triads; no hype without numbers.
10. Layouts adapt mobile → desktop. Dark mode redesigns surfaces and contrast; it does not invert.

## Common mistakes

| Mistake | Fix |
| --- | --- |
| Same radius on parent and padded child | `outer = inner + padding` |
| Jump straight to cards | Whitespace or divider first |
| Card inside a card | Flatten; one surface |
| `transition: all` / `ease-in` / bounce house curve | Named props + strong ease-out |
| Catalog before frequency check | [motion.md](./motion.md) first |
| Solid gray border + shadow | Ring/hairline at low opacity + layered shadow |
| Default indigo + gray neutrals | Project tokens or a deliberate brief palette |
| Gray body on a tinted wash | Darker ink tinted toward the wash hue |
| Dark mode = invert colors | Redesign surfaces; drop elevation shadows; real dark assets |
| Desktop layout shrunk onto mobile | Collapse columns; add mobile nav; larger touch/type on small screens |
| Em dash / negation-triad / kitchen-sink hero | [copy.md](./copy.md) + [aesthetics.md](./aesthetics.md) |
| Inventing tokens beside the project | Read theme first; extend it |

## Reviewing UI

Present every change as a **markdown table with Before / After / Why**, grouped under the principle. One row per change. Cite file and property when unclear. Drop empty principle groups.

#### Motion
| Before | After | Why |
| --- | --- | --- |
| `transition: all 300ms` | `transition: transform 200ms var(--ease-out)` | Name exact properties |
| `transform: scale(0)` entry | `scale(0.95)` + opacity | Nothing real appears from nothing |
| `ease-in` on a dropdown | strong `ease-out` | `ease-in` stalls when the user is watching |
| animation on a keyboard action | no animation | Fired 100×/day; motion reads as lag |

#### Surfaces
| Before | After | Why |
| --- | --- | --- |
| `rounded-xl` card + inner same + `p-2` | concentric outer/inner | Outer = inner + padding |
| white cards on gray by default | content on canvas, or divider | Cards only when they earn the job |
| card nested in card | single surface | Nested cards are lazy hierarchy |
| solid border + shadow | low-opacity ring + layered shadow | Borders fight varied backgrounds |
| popover from center | trigger-anchored origin | Popovers grow from their trigger |

#### Responsive / dark
| Before | After | Why |
| --- | --- | --- |
| two columns squeezed on mobile | stack; mobile nav | Never shrink tool columns |
| `12px` inputs on iOS | ≥16px text on small screens | Prevents focus zoom |
| light palette inverted for dark | redesigned surfaces, no drop shadows | Invert reads wrong |
| raster logo via `filter: invert` | true dark asset | Filters are not a dark treatment |

#### Aesthetics / copy / color
| Before | After | Why |
| --- | --- | --- |
| emoji status / gradient headline word | icon or flat accent | Generated-page tells |
| "go green — then roll it back" | comma or two sentences | Em dash is the generated-text tell |
| light-gray placeholder ~2:1 | 4.5:1 | Placeholders still need AA |

Do not write loose "Before:" / "After:" lines outside a table.

## Review checklist

Direction
- [ ] Register chosen; anchoring matches it
- [ ] Not cream+serif+terracotta, dark+acid-green, or white+blue/violet SaaS unless briefed
- [ ] One signature element; everything else quiet
- [ ] Passes the AI slop cold test
- [ ] Existing tokens/components reused

Surfaces and type
- [ ] Concentric radii; lightest separation that works; no nested cards
- [ ] Optical icon alignment; depth from layered shadow / dark rings
- [ ] Shadows not clipped; image outlines black/white at 10%
- [ ] Hit areas ≥40×40 (≥44 touch) and non-overlapping
- [ ] Spacing rhythm: tight in groups, larger between groups, largest between sections
- [ ] Headings balance; body pretty; root antialiased; updating nums tabular
- [ ] Heading weight medium/semibold (not heavy bold by default); tracking tight only on large display

Motion
- [ ] Justified; no keyboard/100×/day motion
- [ ] Strong ease-out; no ease-in; no bounce/elastic house curve
- [ ] Under 300ms functional; exits quicker; enter from 0.95; press 0.96
- [ ] Transitions for re-triggerable; popovers origin-aware
- [ ] transform/opacity only; no `transition: all`; reduced-motion; hover gated

Color, dark, responsive
- [ ] Body 4.5:1; large 3:1; placeholders 4.5:1; focus 3:1
- [ ] No washed gray on colored bg; no color-alone state
- [ ] Dark mode redesigns contrast/surfaces; shadows dropped or replaced with rings
- [ ] Mobile and desktop both work; mobile nav when needed; inputs ≥16px on small screens

Aesthetics and copy
- [ ] No named slop tells without an explicit ask
- [ ] No em/en dashes; no negation-triad; no hype without numbers
- [ ] Hero: one headline, ≤2-line subhead, one primary CTA naming an outcome
- [ ] Interaction states covered; Verify section passed

---

*Craft UI by Nika Siradze. More at [nikusha.com](https://nikusha.com).*
