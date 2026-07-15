---
name: craft-ui
description: Craft-level UI polish and motion decisions that make interfaces feel finished. Use when building or reviewing frontend UI, choosing or implementing animations/transitions, fixing visual details (radius, shadows, hit areas, type), or catching AI-slop aesthetics and copy. Triggers on polish, feels off, micro-interaction, hover/press, dropdown/modal transition, stagger, border radius, box shadow, tabular nums, gradient text, em dash, quieter, distill, shape, audit.
---

# Craft UI

Working code is free. This skill is the judgment layer that stops the result from reading as unfinished or generated. It guarantees a quality floor; it does not hand you a look. If every project comes out the same, you copied defaults instead of deciding.

User direction overrides everything below. Absent a clear ask otherwise, treat the **correctness** rules as non-negotiable and the **taste defaults** as the starting point to adapt.

## Setup (do before designing)

You MUST do these in order. Skipping them is how agents invent a second design system and paste the catalog blindly.

1. **Route the ask** using the [Intent map](#intent-map). Load only the files that route names. Do not preload every satellite.
2. **Read the project.** Open at least one real file: tokens, theme, global CSS, or a representative component. Match that stack (Tailwind, CSS modules, Motion, plain CSS). Prefer existing components and tokens over inventing parallels.
3. **Pick the register.** Marketing / landing / portfolio = design IS the product (hero discipline, signature element, [start-here.md](./start-here.md) hard). App / dashboard / tool = design SERVES the product (density, crisp motion, fewer decorative tells). Task cue beats guesswork.
4. **Decide before paste.** Motion work answers "should this animate?" in [motion.md](./motion.md) before opening [transitions/catalog.md](./transitions/catalog.md).
5. **Before you call it done**, walk the [Review checklist](#review-checklist) and fix misses. Reviews ship only as Before / After / Why tables.

Never load all satellites at once. Never open the catalog first.

## Intent map

First word or clear intent maps to a route. Load that route's files (this file's hard rules always apply).

| Intent / synonyms | Route | Load |
| --- | --- | --- |
| `shape`, plan, from a brief, redesign from scratch | From a brief | [start-here.md](./start-here.md), then floor files as needed |
| `polish`, final pass, ship-ready, feels almost done | Review + floor | This checklist + [surfaces.md](./surfaces.md), [aesthetics.md](./aesthetics.md), [copy.md](./copy.md); pull others only for hits |
| `audit`, review, critique, what is wrong | Review | This checklist + only satellites the findings touch |
| `animate`, transition, micro-interaction, hover/press | Motion | [motion.md](./motion.md), then [transitions/catalog.md](./transitions/catalog.md) if implementing |
| surfaces, radius, shadow, hit area, alignment | Surfaces | [surfaces.md](./surfaces.md) |
| `typeset`, type, wrapping, tabular | Type | [typography.md](./typography.md) |
| `colorize`, contrast, focus ring, palette | Color | [color.md](./color.md) |
| `quieter`, less slop, too loud, generic AI look | Anti-slop | [aesthetics.md](./aesthetics.md), [copy.md](./copy.md) |
| `distill`, simplify, too much chrome | Distill | [start-here.md](./start-here.md) steps 3–5 + [aesthetics.md](./aesthetics.md) + [copy.md](./copy.md) |

If two intents fit, pick the narrower one (e.g. "fix the dropdown motion" → Motion, not Review). If none fit, apply this file's hard rules plus the register, and load satellites only when a specific detail comes up.

## Correctness vs taste

- **Correctness (always).** Breaking these is a bug: no `transition: all`; animate `transform`/`opacity` for movement; ship `prefers-reduced-motion`; concentric radius; real hit areas; no em dashes in UI copy; contrast/focus/color-alone rules in [color.md](./color.md).
- **Taste defaults (adapt).** Exact shadow rgba, house ease-out, `scale(0.96)` on press, single-hue wash: sane starting numbers. A playful product and a precise dashboard should not share the same motion or radius values.

Personality axes where products should diverge: color, type, density, radius scale, motion character, layout. Deliberate choices here are what stop identical "crafted" outputs.

## Absolute bans

Do not ship these unless the user explicitly asked for that exact move:

- `transition: all`; `ease-in` on UI enter/exit; bounce/elastic as the house curve
- `scale(0)` entrances; motion on keyboard / 100×/day actions
- Nested cards; cards as the default layout answer
- Gradient text; gradient-square logos; multi-hue aurora backgrounds; colored glow shadows
- Pill/eyebrow kickers and icon-in-colored-tile hero chrome
- Emoji as product chrome; Inter/Roboto/Arial as the "designed" display face by default
- Em dashes; "No X, no Y, just Z"; hype adjectives without numbers
- Cream/sand/beige body + terracotta + display serif as the unearned editorial default

## AI slop cold test

Before shipping, ask: if you stripped the logo, could this screen belong to any other SaaS/tool shipped this year? If yes, return to register + [start-here.md](./start-here.md) anchoring. Fixing radius while the composition is generic is not craft.

## Quick reference

| File | Covers |
| --- | --- |
| [start-here.md](./start-here.md) | Brief → UI: anchor, plan, critique defaults, build, review |
| [surfaces.md](./surfaces.md) | Concentric radius, optical alignment, shadows vs borders, clipping, image outlines, hit areas |
| [typography.md](./typography.md) | `text-wrap`, font smoothing, `tabular-nums` |
| [motion.md](./motion.md) | Animate-or-not, easing, duration, enter/exit, stagger, press, springs, gestures, perf, a11y |
| [color.md](./color.md) | WCAG AA, non-text contrast, never color-alone, visible focus, palette taste |
| [aesthetics.md](./aesthetics.md) | Named AI-slop tells: emoji icons, gradient text/logos, pills, glows, aurora, hero chrome |
| [copy.md](./copy.md) | Hero anatomy, kicker rule, CTA, page flow; no em dashes, negation-triads, or hype |
| [transitions/catalog.md](./transitions/catalog.md) | Eighteen paste-ready CSS transitions + [`_root.css`](./transitions/_root.css) |

## Non-negotiables

1. **Decide whether to animate before how.** Keyboard / 100×/day actions: no animation. Frequency table in [motion.md](./motion.md#1-should-this-animate-at-all).
2. House ease-out: `cubic-bezier(0.22, 1, 0.36, 1)`. Never `ease-in` on UI. No bounce/elastic as the default curve.
3. Functional UI under 300ms. Exits ~half the enter.
4. Enter from `scale(0.95)` + opacity, never `scale(0)`. Press: `scale(0.96)`, never below `0.95`.
5. Re-triggerable motion: CSS transitions, not keyframes.
6. Animate `transform`/`opacity` only for movement. No `transition: all`. Always `prefers-reduced-motion`. Gate hover behind `(hover: hover)`.
7. Outer radius = inner radius + padding. Depth from layered shadow, not solid border chrome. Cards only when they earn the job; never nest cards.
8. No emoji as UI chrome; no gradient text; no gradient-square logos; no neon glow shadows.
9. No em dashes in UI copy; no "No X, no Y, just Z"; no hype adjectives without numbers.

## Common mistakes

| Mistake | Fix |
| --- | --- |
| Same radius on parent and padded child | `outer = inner + padding` |
| `transition: all` | Name exact properties |
| `ease-in` on enter/exit | Strong custom `ease-out` |
| Bounce/elastic as house easing | Ease-out; save spring bounce for rare delight |
| `scale(0)` entrance | `scale(0.95)` + opacity |
| Animation on command palette / shortcut | Remove motion |
| Catalog recipe before frequency check | Read [motion.md](./motion.md) first |
| Solid card border for depth | Layered transparent `box-shadow` |
| Card inside a card | Flatten; one surface, clearer hierarchy |
| Popover scales from center | Origin from trigger (modals stay centered) |
| Emoji / Lucide-everywhere as hero decoration | Real mark or nothing; icons must match labels |
| Mood kicker + dual CTAs + three feature cards in hero | One headline, one support line, one CTA group |
| Em dash or "No X, no Y, just Z" | Plain punctuation; positive specific claim |
| Inventing new tokens beside the project's | Read existing theme first; extend it |
| Loading every skill file for a one-line tweak | Use the intent map; load one topic |

## Reviewing UI

Present every change as a **markdown table with Before / After / Why**, grouped under the principle. One row per change. Cite file and property when the snippet alone is unclear. Drop principles with nothing to fix.

#### Motion
| Before | After | Why |
| --- | --- | --- |
| `transition: all 300ms` | `transition: transform 200ms var(--ease-out)` | Name exact properties; `all` animates unrelated changes |
| `transform: scale(0)` entry | `transform: scale(0.95); opacity: 0` | Nothing real appears from nothing |
| `ease-in` on a dropdown | strong `ease-out` | `ease-in` stalls when the user is watching |
| animation on a keyboard action | no animation | Fired 100×/day; motion reads as lag |

#### Surfaces
| Before | After | Why |
| --- | --- | --- |
| `rounded-xl` card + `rounded-xl` inner (`p-2`) | `rounded-2xl` card, `rounded-lg` inner | Concentric: outer = inner + padding |
| solid border on a card | layered `box-shadow` | Shadows work on any background |
| card nested inside a card | single surface, spacing does the grouping | Nested cards are lazy hierarchy |
| `transform-origin: center` on a popover | trigger-anchored origin | Popovers grow from their trigger |

#### Aesthetics
| Before | After | Why |
| --- | --- | --- |
| emoji in a status badge | Lucide icon or colored dot | Emoji chrome reads as placeholder |
| gradient text on a headline word | flat accent color | Generated-landing-page tell |
| purple glow under a button | neutral low-opacity shadow | Glow is decoration, not depth |
| pill kicker above H1 | cut it, or fold a fact into the headline | Mood-pill hero chrome is templated |

#### Color
| Before | After | Why |
| --- | --- | --- |
| light-gray placeholder ~2:1 | darken to 4.5:1 | Body and placeholders must clear AA |
| white label on mid-tone accent | darker fill or dark ink | White-on-accent often fails 4.5:1 |
| gray body on a tinted wash | ink tinted toward the wash hue, darker | Gray-on-color washes out and fails contrast |
| error by red border only | border + message + icon | Color-alone fails for color-blind users |
| `outline: none` | visible `:focus-visible` at 3:1 | Keyboard users need the ring |

#### Copy
| Before | After | Why |
| --- | --- | --- |
| "go green below — then roll it back" | "go green below, then roll it back" | Em dash is the top generated-text tell |
| "No streaks, no badges, just focus" | "One timer, then you're done" | Negation-triad is banned filler |
| "blazing fast deploys" | "cold start under 40ms" | Specific claims beat hype |

Do not write loose "Before:" / "After:" lines outside a table.

## Review checklist

Direction
- [ ] Register chosen (brand vs product) and anchoring matches it
- [ ] Anchored in the product's world, not generic defaults
- [ ] Not accidentally cream+serif+terracotta, dark+acid-green, or white+blue SaaS unless the brief asked
- [ ] One signature element; everything else stays quiet
- [ ] Passes the AI slop cold test
- [ ] Existing project tokens/components reused where they fit

Surfaces and type
- [ ] Nested radii are concentric
- [ ] No nested cards; cards earn their job
- [ ] Icons optically centered
- [ ] Depth from layered shadow; borders for dividers/inputs
- [ ] Card shadows not clipped by `overflow: hidden`
- [ ] Images: pure black/white 1px outline at 10% opacity
- [ ] Hit areas ≥40×40px and non-overlapping
- [ ] Headings `text-wrap: balance`; body `pretty`
- [ ] Root `-webkit-font-smoothing: antialiased`
- [ ] Updating numbers use `tabular-nums`

Motion
- [ ] Every animation has a reason; frequent/keyboard actions are not animated
- [ ] Strong `ease-out` (or `ease-in-out` for on-screen move); no `ease-in`; no bounce/elastic house curve
- [ ] Functional durations under 300ms; exits quicker than enters
- [ ] Entrances from `scale(0.95)` + opacity; split/stagger where it helps
- [ ] Press `scale(0.96)`, never below `0.95`
- [ ] Re-triggerable motion uses transitions, not keyframes
- [ ] Popovers origin-aware; modals centered
- [ ] Only `transform`/`opacity` for movement; no `transition: all`
- [ ] `will-change` only on compositor props where stutter is real
- [ ] `prefers-reduced-motion` on every animation; hover gated with `(hover: hover)`

Color and contrast
- [ ] Body 4.5:1; large text 3:1; placeholders still 4.5:1
- [ ] Button labels pass on their fill
- [ ] No washed-out gray text on colored backgrounds
- [ ] Input borders, icons, focus rings meet 3:1
- [ ] No state relies on color alone
- [ ] Every interactive element has visible `:focus-visible`

Aesthetics and copy
- [ ] No emoji as icon/bullet/badge; icons match labels
- [ ] No gradient text; logo is solid fill or real mark
- [ ] No pill/eyebrow kicker, icon-in-colored-tile hero, or floating bobbing cards unless brief demands
- [ ] Background flat or single-hue wash, not multi-hue aurora
- [ ] Shadows neutral, not colored glow
- [ ] No em/en dashes; no negation-triad or "X, not Y" buildup; no hype clichés
- [ ] Sentence case; claims specific
- [ ] Hero: one headline, ≤2-line subhead, one primary CTA naming an outcome
- [ ] Deliberate color, type, density, radius, and motion character

---

*Craft UI by Nika Siradze. More at [nikusha.com](https://nikusha.com).*
