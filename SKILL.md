---
name: craft-ui
description: Craft-level UI polish, the small details and motion decisions that make an interface feel right instead of just work. Use when building or reviewing frontend UI, implementing animations/transitions, or doing visual detail work. Covers border radius, optical alignment, shadows vs borders, image outlines, hit areas, typography (text-wrap, tabular-nums, font smoothing), the animation decision (whether/when to animate, easing, duration), enter/exit and stagger animations, scale-on-press, icon swaps, springs, gestures, and performance, plus a catalog of paste-ready CSS transitions (dropdown, modal, panel, page slide, notification badge, success check, error shake, skeleton, shimmer, sliding tabs, tooltip, number pop-in, text/icon swap, avatar hover, input clear). Triggers on "make it feel better", "feels off", "polish this UI", "add a transition", "animate the dropdown/modal", "stagger animation", "hover state", "micro-interaction", "border radius", "box shadow", "tabular numbers".
---

# Craft UI

The AI ships code that works. That part is free now. What it does not hand you is the
feel: the dozens of tiny calls that decide whether a product reads as considered or as
something nobody finished.

That feel rarely comes from one big move. It is the border radius that lines up with
the one inside it. The dropdown that grows out of the button you pressed instead of
popping in from nowhere. The number that holds the layout still when it ticks. Each one
is invisible alone. Stack enough and you get a product people trust without being able
to say why. That trust is the point.

Treat this skill as the judgment layer. Use it while building. Use it harder while
reviewing, whether the code is yours or the AI's.

## How to read this skill

These are recommendations, not a spec to reproduce. The skill guarantees a quality
floor. It does not hand you a look. If everything you build with it comes out looking
the same, you're copying the defaults instead of deciding.

**If you're starting a screen from a brief, read [start-here.md](./start-here.md)
first.** It's the sequence (anchor, plan, critique, build, review) that keeps the
output from converging on the same generated look. The files below are the floor you
build on once the direction is set.

Two kinds of rules live here, and they're not equal:

- **Correctness (follow always).** These prevent broken or sloppy results, and they
  don't constrain style: no `transition: all`, animate `transform`/`opacity` for
  movement, ship a `prefers-reduced-motion` guard, concentric radius math, real hit
  areas, no em dashes in copy. Breaking these is a bug.
- **Taste defaults (a starting point, adapt freely).** The exact shadow rgba, the
  house ease-out curve, `scale(0.96)` on press, the single-hue wash: these are sane
  defaults so you don't start from zero. Tune them to the brand. A playful product
  and a precise dashboard should not share the same numbers.

### Make it have range

A floor is not a look. The skill standardizes correctness; the personality is yours,
and these are the axes where two craft-ui products *should* diverge. If you're not
making deliberate choices here, you'll get the generic result:

- **Color.** One product is near-monochrome with a single accent; another is warm and
  earthy; another is high-contrast and loud. Don't default to the same blue/violet.
- **Type.** A grotesk, a humanist sans, a serif display, a mono-accented technical
  voice all change the feel before a single pixel of layout does.
- **Density and whitespace.** Airy and editorial versus compact and dashboard-dense
  are different products. Pick on purpose.
- **Radius scale.** Sharp 4px corners read as precise/technical; 16-24px reads as
  soft/friendly. Choose a scale and hold it (concentrically).
- **Motion character.** Crisp and minimal, or springy and alive. The decision
  framework in [motion.md](./motion.md) applies either way; the values change.
- **Layout.** Not every page is a centered hero over two cards. Vary the composition.

When in doubt, match the motion and the visual choices to the product's mood: a
celebration can bounce, a banking dashboard stays crisp and fast. Cohesion across all
of it is what makes a thing feel designed rather than assembled.

## What's in here

Each file stands on its own. Jump to whichever one the work touches.

| File | Covers |
| --- | --- |
| [start-here.md](./start-here.md) | **Read first.** From brief to UI: anchor in the product's world, plan, critique against default looks, then build |
| [surfaces.md](./surfaces.md) | Concentric border radius, optical alignment, shadows vs borders, shadow clipping, image outlines, hit areas |
| [typography.md](./typography.md) | `text-wrap` balance/pretty, macOS font smoothing, tabular numbers |
| [motion.md](./motion.md) | The animation decision, easing and duration, enter/exit and stagger, scale-on-press, icon swaps, springs, gestures, performance, accessibility, debugging |
| [color.md](./color.md) | Contrast ratios (WCAG AA), non-text contrast, never color-alone, visible focus, palette taste |
| [aesthetics.md](./aesthetics.md) | Visual defaults that read as AI slop: emoji-as-icons, gradient text, gradient logos, multi-hue blobs, neon glows, mismatched icons |
| [copy.md](./copy.md) | Messaging (hero anatomy, the kicker rule, CTA, page flow) and microcopy (no em dashes, no negation-triads, no hype, sentence case) |
| [transitions/catalog.md](./transitions/catalog.md) | Eighteen paste-ready CSS transitions, the shared motion tokens, and [`_root.css`](./transitions/_root.css) |

Surfaces and typography are the static details. Motion is how you think about
anything that moves. Aesthetics and copy are what keep a screen from looking and
reading like a generator made it. The catalog is the code you copy once you've
decided the motion belongs. That order matters: reason about the animation in
`motion.md` first, then grab a recipe. Never the other way around.

## The one rule that beats the rest

**Decide whether to animate before you touch how.** The most common motion mistake
is not a weak easing curve. It is animating something that should never have moved.

**Why:** anything a user fires hundreds of times a day, like a keyboard shortcut or a
command palette, needs to be instant. Put an animation there and it reads as lag
every single time, forever. The frequency framework is in
[motion.md](./motion.md#1-should-this-animate-at-all). Easing, duration, springs:
none of it matters until "should this animate?" is a clear yes.

A handful of defaults worth keeping in your head (all explained in the deep-dives):

- House ease-out is `cubic-bezier(0.22, 1, 0.36, 1)`. Never `ease-in` on UI.
- Functional UI motion stays under 300ms. Exits run about half the enter.
- Enter from `scale(0.95)`, never `scale(0)`. Press feedback is `scale(0.96)`, never below `0.95`.
- Anything re-triggerable uses CSS transitions, not keyframes.
- Animate `transform` and `opacity` only. Never `transition: all`. Always ship a `prefers-reduced-motion` guard.
- Outer radius equals inner radius plus padding. Depth comes from layered shadow, not a solid border.
- No emoji as UI, no gradient text, no gradient-square logos, no neon glow shadows.
- No em dashes in the copy, and no "No X, no Y, just Z" subheads.

## Reviewing UI

Present every change as a **markdown table with Before / After / Why columns**,
grouped under the principle it belongs to. One row per change, each on a single diff
so the list scans in seconds. Name the file and the exact property when the snippet
alone doesn't make it obvious. If you checked a principle and nothing needed fixing,
drop it. An empty table is just noise.

#### Motion
| Before | After | Why |
| --- | --- | --- |
| `transition: all 300ms` | `transition: transform 200ms var(--ease-out)` | Name exact properties; `all` lets unrelated changes animate for free |
| `transform: scale(0)` entry | `transform: scale(0.95); opacity: 0` | Nothing in the real world appears from nothing |
| `ease-in` on a dropdown | a strong `ease-out` curve | `ease-in` stalls at the exact moment the user is watching |
| animation on a keyboard action | no animation | Fired 100x/day, so motion reads as lag |

#### Surfaces
| Before | After | Why |
| --- | --- | --- |
| `rounded-xl` card + `rounded-xl` inner (`p-2`) | `rounded-2xl` card, `rounded-lg` inner | Concentric: outer equals inner plus padding |
| solid border on a card | layered `box-shadow` | Shadows sit on any background; a border color only works on one |
| `transform-origin: center` on a popover | trigger-anchored origin variable | Popovers grow from their trigger (modals stay centered) |

#### Aesthetics
| Before | After | Why |
| --- | --- | --- |
| lightning-bolt emoji in a status badge | Lucide icon or a small colored dot | Emoji as chrome reads as a placeholder nobody replaced |
| gradient text on a headline word | accent color, flat | Gradient text is the generic generated-landing-page move |
| purple glow shadow under a button | neutral low-opacity shadow | Glow is decoration, not depth |

#### Color
| Before | After | Why |
| --- | --- | --- |
| light-gray placeholder at ~2:1 | darken to meet 4.5:1 | Body and placeholder text must clear AA |
| white label on a mid-tone accent button | darker accent or dark ink label | White-on-accent often fails 4.5:1 |
| error shown by red border only | red border plus message and icon | Color-alone fails for color-blind users |
| `outline: none` on a button | visible `:focus-visible` ring at 3:1 | Keyboard users navigate by the focus ring |

#### Copy
| Before | After | Why |
| --- | --- | --- |
| "go green below — then roll it back" | "go green below, then roll it back" | Em dash is the top tell of generated text |
| "No streaks, no badges, just focus" | "One timer, then you're done" | Negation-triad is banned filler |
| "Built for one wallet, not a finance team" | "Built for one wallet" | "X, not Y" positions by what it isn't |
| mood kicker above the H1 ("A printed monthly...") | cut it, or fold a real fact into the headline | Mood-kicker over the title is a templated tell |
| "blazing fast deploys" | "cold start under 40ms" | Specific claims beat hype adjectives |

Don't write findings as loose "Before:" / "After:" lines outside a table.

## Review checklist

Direction (from the brief)
- [ ] Choices are anchored in the product's actual world, not generic defaults
- [ ] Not landing in a default look by accident (cream+serif+terracotta, dark+acid-green, white+blue SaaS) unless the brief asked for it
- [ ] One signature element; everything around it stays quiet
- [ ] Shown cold, someone could tell which product this is

Surfaces and type
- [ ] Nested rounded elements use concentric radius (outer equals inner plus padding)
- [ ] Icons are optically centered, not just geometrically
- [ ] Depth comes from layered shadow; borders only for dividers/inputs
- [ ] Card shadows aren't clipped by an `overflow: hidden` ancestor (check bottom/right edges)
- [ ] Images carry a pure-black/white 1px outline at 10% opacity
- [ ] Interactive elements have 40x40px or larger hit areas that never overlap
- [ ] Headings use `text-wrap: balance`; body uses `text-wrap: pretty`
- [ ] Root has `-webkit-font-smoothing: antialiased`
- [ ] Numbers that update use `tabular-nums`

Motion
- [ ] Every animation has a reason, and frequent/keyboard actions aren't animated
- [ ] Easing is a strong `ease-out` (or `ease-in-out` for on-screen movement); no `ease-in`
- [ ] Functional durations stay under 300ms; exits are quicker than enters
- [ ] Entrances start from `scale(0.95)` plus opacity, split and staggered where it helps
- [ ] Press feedback is `scale(0.96)`, never below `0.95`
- [ ] Re-triggerable motion uses transitions, not keyframes
- [ ] Popovers are origin-aware (modals stay centered)
- [ ] Only `transform`/`opacity` animate for movement; no `transition: all`
- [ ] `will-change` only on compositor-friendly props, only where stutter is real
- [ ] Every animation ships a `prefers-reduced-motion` guard; hover effects gated behind `(hover: hover)`

Color and contrast
- [ ] Body text meets 4.5:1; large text/headings meet 3:1; placeholders still meet 4.5:1
- [ ] Button labels pass contrast on their own fill (white-on-accent often fails)
- [ ] Input borders, icons, and focus rings meet 3:1
- [ ] No state relies on color alone; it survives a grayscale check
- [ ] Every interactive element has a visible `:focus-visible` style

Aesthetics and copy
- [ ] No emoji used as an icon, bullet, or badge marker; icons match their labels
- [ ] No gradient on text; logo/app icon is a solid fill or real mark, not a gradient square
- [ ] Background is flat or a single-hue wash, not a multi-color blob
- [ ] Button and card shadows are neutral, not a colored glow
- [ ] No em dashes or en dashes in any UI copy
- [ ] No "No X, no Y, just Z" or "X, not Y" buildup; no hype clichés (blazing fast, seamless, 10x)
- [ ] Sentence case on headings, buttons, and labels; claims are specific
- [ ] No mood-only kicker above the headline; hero subhead is 1 to 2 lines, one idea
- [ ] Primary CTA names the outcome ("Mail me issue 15"), not the system action ("Submit")
- [ ] Deliberate choices on color, type, density, radius, and motion character (not the same defaults every time)

---

*Craft UI by Nika Siradze. More at [nikusha.com](https://nikusha.com).*
