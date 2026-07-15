---
name: craft-ui
description: Craft-level UI polish and motion decisions that make interfaces feel finished. Use when building or reviewing frontend UI, choosing or implementing animations/transitions, fixing visual details (radius, shadows, hit areas, type), or catching AI-slop aesthetics and copy. Triggers on polish, feels off, micro-interaction, hover/press, dropdown/modal transition, stagger, border radius, box shadow, tabular nums, gradient text, em dash.
---

# Craft UI

Working code is free. This skill is the judgment layer that stops the result from reading as unfinished or generated. It guarantees a quality floor; it does not hand you a look. If every project comes out the same, you copied defaults instead of deciding.

User direction overrides everything below. Absent a clear ask otherwise, treat the **correctness** rules as non-negotiable and the **taste defaults** as the starting point to adapt.

## How to use this skill (agent protocol)

1. **Read this file first.** Do not preload every satellite.
2. **Pick one mode** from the table below. Load only the files that mode needs.
3. **Decide before paste.** For motion: answer "should this animate?" in [motion.md](./motion.md) before opening [transitions/catalog.md](./transitions/catalog.md).
4. **Match the project's stack** (Tailwind, CSS modules, Motion, plain CSS). Do not invent a parallel styling system.
5. **Before you call the work done**, walk the [Review checklist](#review-checklist) and fix misses. For reviews, ship findings only as Before / After / Why tables.

| Mode | When | Load |
| --- | --- | --- |
| From a brief | New screen or redesign from a product brief | [start-here.md](./start-here.md), then floor files as needed |
| Surfaces / type | Radius, shadows, hit areas, alignment, wrapping, nums | [surfaces.md](./surfaces.md), [typography.md](./typography.md) |
| Motion | Whether / how to animate, then recipes | [motion.md](./motion.md), then [transitions/catalog.md](./transitions/catalog.md) if implementing |
| Color | Contrast, focus, never color-alone, palette taste | [color.md](./color.md) |
| Anti-slop | Generated look, icons, glows, hero chrome | [aesthetics.md](./aesthetics.md), [copy.md](./copy.md) |
| Review | Audit existing UI or an agent diff | This file's checklist + only satellites the findings touch |

Never load all satellites at once. Never open the catalog first.

## Correctness vs taste

- **Correctness (always).** Breaking these is a bug: no `transition: all`; animate `transform`/`opacity` for movement; ship `prefers-reduced-motion`; concentric radius; real hit areas; no em dashes in UI copy; contrast/focus/color-alone rules in [color.md](./color.md).
- **Taste defaults (adapt).** Exact shadow rgba, house ease-out, `scale(0.96)` on press, single-hue wash: sane starting numbers. A playful product and a precise dashboard should not share the same motion or radius values.

Personality axes where products should diverge: color, type, density, radius scale, motion character, layout. Deliberate choices here are what stop identical "crafted" outputs.

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
2. House ease-out: `cubic-bezier(0.22, 1, 0.36, 1)`. Never `ease-in` on UI.
3. Functional UI under 300ms. Exits ~half the enter.
4. Enter from `scale(0.95)` + opacity, never `scale(0)`. Press: `scale(0.96)`, never below `0.95`.
5. Re-triggerable motion: CSS transitions, not keyframes.
6. Animate `transform`/`opacity` only for movement. No `transition: all`. Always `prefers-reduced-motion`. Gate hover behind `(hover: hover)`.
7. Outer radius = inner radius + padding. Depth from layered shadow, not solid border chrome.
8. No emoji as UI chrome; no gradient text; no gradient-square logos; no neon glow shadows.
9. No em dashes in UI copy; no "No X, no Y, just Z"; no hype adjectives without numbers.

## Common mistakes

| Mistake | Fix |
| --- | --- |
| Same radius on parent and padded child | `outer = inner + padding` |
| `transition: all` | Name exact properties |
| `ease-in` on enter/exit | Strong custom `ease-out` |
| `scale(0)` entrance | `scale(0.95)` + opacity |
| Animation on command palette / shortcut | Remove motion |
| Catalog recipe before frequency check | Read [motion.md](./motion.md) first |
| Solid card border for depth | Layered transparent `box-shadow` |
| Popover scales from center | Origin from trigger (modals stay centered) |
| Emoji / Lucide-everywhere as hero decoration | Real mark or nothing; icons must match labels |
| Mood kicker + dual CTAs + three feature cards in hero | One headline, one support line, one CTA group |
| Em dash or "No X, no Y, just Z" | Plain punctuation; positive specific claim |
| Loading every skill file for a one-line tweak | Use the mode table; load one topic |

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
- [ ] Anchored in the product's world, not generic defaults
- [ ] Not accidentally cream+serif+terracotta, dark+acid-green, or white+blue SaaS unless the brief asked
- [ ] One signature element; everything else stays quiet
- [ ] Shown cold, someone could tell which product this is

Surfaces and type
- [ ] Nested radii are concentric
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
- [ ] Strong `ease-out` (or `ease-in-out` for on-screen move); no `ease-in`
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
