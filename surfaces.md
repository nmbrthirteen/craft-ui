# Surfaces

Border radius, optical alignment, depth, grouping, spacing rhythm, section layout,
responsive behavior, image edges, hit areas. The details nobody points at and
everybody feels.

## Lightest separation that works

Do not jump to cards. Pick the lightest treatment that still communicates grouping:

1. **Whitespace** when items are tightly related or already contrast by type size/weight
2. **Dividers / hairlines** for sibling rows and metric strips (opacity-based, not solid gray)
3. **Recessed wells** for secondary or nested content
4. **Cards** only for independently interactive units or fundamentally different content

Never nest cards. Prefer content on the canvas over white cards on gray by default.
One depth technique per view: borders-only, tint, soft shadow, or layered shadow —
mixing all of them makes hierarchy accidental.

In containers, outer padding is at least the gap between children. Related children
sit closer to each other than to the container edge.

## Spacing rhythm and section layout

Use a three-step rhythm so grouping reads from the gaps: tightest within a group,
more between groups, most between sections (e.g. 8 / 16 / 32–40). Keep the same jumps
across the page.

Measure gaps between **visible contrast edges**, not invisible boxes. If a block has
a tinted background, the section gap starts at that background edge.

Page sections: outer wrapper for background + vertical padding; inner for max-width,
centering, and horizontal padding. Keep that pattern consistent so content edges
align while scrolling. Align parallel columns across stacked sections to the same
grid. Avoid floating nested max-widths on grids that should span the page container.

## Concentric border radius

Nest one rounded box inside another and the outer radius has to equal the inner
radius plus the padding between them:

```
outerRadius = innerRadius + padding
```

**Why:** if the two radii don't follow that math, the corners run non-parallel and
the eye reads the whole thing as sloppy without knowing what's wrong. This is the
single most common reason a layout feels off when nothing is technically broken.

```css
/* Good: concentric */
.card        { border-radius: 20px; padding: 8px; }  /* 12 + 8 */
.card-inner  { border-radius: 12px; }

/* Bad: same radius on both, corners diverge */
.card        { border-radius: 12px; padding: 8px; }
.card-inner  { border-radius: 12px; }
```

```tsx
// Tailwind: outer radius accounts for the padding
<div className="rounded-2xl p-2">     {/* 16px radius, 8px padding */}
  <div className="rounded-lg">        {/* 8px = 16 - 8 */}
    ...
  </div>
</div>
```

The math matters most when the layers sit close. Once padding gets past about 24px
the surfaces read as independent, so pick each radius on its own and stop forcing
the formula.

## Optical over geometric alignment

Centered by the numbers and centered to the eye are not the same thing. When the
math looks wrong, the math is wrong, so trust the eye.

**Text plus icon buttons.** Shave a couple pixels off the icon side so the button
sits balanced: `icon-side padding = text-side padding - 2px`.

```tsx
<button className="pl-4 pr-3.5 flex items-center gap-2">
  <span>Continue</span>
  <ArrowRightIcon />
</button>
```

**Play triangles.** A play icon's geometric center sits left of where the eye reads
its center. Nudge it right (`margin-left: 2px`) so it looks centered in its circle.

**Lopsided icons** like stars, arrows, and carets carry uneven weight. The best fix
is editing the SVG's viewBox or path so the component needs no compensating margin
at all. If you can't touch the SVG, a `margin-left: 1px` (`ml-px`) is the fallback.

## Depth from shadow, not borders

For **buttons, cards, and anything elevated**, reach for a layered `box-shadow`
before a solid border. Never pair a soft shadow with a solid gray border; use a
low-opacity ring/hairline instead.

**Why:** a shadow is built from transparency, so it sits correctly on any
background, whether that's an image, a gradient, or a themed surface. A solid border
color only ever looks right on the one background you picked it against.

Stack three: a hairline ring doing the border's job, a tight lift, and a soft
ambient shadow underneath.

```css
:root {
  --shadow-border:
    0 0 0 1px rgba(0, 0, 0, 0.06),
    0 1px 2px -1px rgba(0, 0, 0, 0.06),
    0 2px 4px 0 rgba(0, 0, 0, 0.04);
  --shadow-border-hover:
    0 0 0 1px rgba(0, 0, 0, 0.08),
    0 1px 2px -1px rgba(0, 0, 0, 0.08),
    0 2px 4px 0 rgba(0, 0, 0, 0.06);
}

.card {
  box-shadow: var(--shadow-border);
  transition-property: box-shadow;
  transition-duration: 150ms;
  transition-timing-function: ease-out;
}
.card:hover { box-shadow: var(--shadow-border-hover); }
```

Custom shadows: blur roughly twice the offset; lower opacity as elevation rises.
Elevated surfaces stay at the lightest canvas, not a darker gray card on light UI.

In dark mode the layered depth disappears against the dark surface, so collapse it
to a single white ring and drop drop-shadows:

```css
/* dark theme: match the project's mechanism (class, data-attr, media query) */
--shadow-border:       0 0 0 1px rgba(255, 255, 255, 0.08);
--shadow-border-hover: 0 0 0 1px rgba(255, 255, 255, 0.13);
```

This is about depth, not separation. A `border-b` between list rows, a table cell
boundary, a form input outline, a hairline in dense UI: those draw a line, they
don't lift anything. Leave them as borders. Prefer opacity-based dividers
(`color-mix` or alpha) over solid `gray-200` lines.

| Use shadows | Keep borders |
| --- | --- |
| Cards and containers with depth | Dividers between list items |
| Buttons with a bordered style | Table cell boundaries |
| Elevated surfaces (dropdowns, modals) | Input outlines (accessibility) |
| Anything on a varied background | Hairlines in dense UI |
| Hover/focus lift states | |

### Don't let the shadow get clipped

A common bug: the shadow renders, then gets sliced off on one side. The cause is
almost always an ancestor with `overflow: hidden` (or `clip`, or a carousel/grid that
crops its children), or a card pushed flush against the edge of a clipped container.

**Why it happens:** a `box-shadow` paints outside the element's box. If any ancestor
clips overflow, the part of the shadow that extends past the child gets cut.

Fixes, in order of preference:

- Don't clip the container that holds shadowed cards. Use `overflow: visible` (or
  remove the `overflow` rule) on that ancestor.
- If the container must clip (rounded image wrapper, scroll area), leave padding
  around the shadowed element at least equal to the shadow's blur and spread so the
  shadow has room to render inside the clip.
- As a last resort, move the shadow onto an inner element that isn't against the clip
  boundary.

Check the bottom and right edges specifically: that's where a card flush to a clipped
parent loses its shadow.

## Responsive

Every layout adapts from mobile to desktop. Prefer mobile-first; use container queries
when a component's layout depends on its own width, not the viewport.

- Multi-column shells (sidebars, filters) **collapse**; never squeeze columns. Add a
  mobile nav (disclosure/dialog) below the desktop breakpoint; hide desktop nav on
  small screens.
- Body text and controls are often **larger on mobile**, then slightly tighter on
  larger breakpoints. Page titles stay the same or get smaller on mobile, never bigger.
- Text inputs stay at least **16px** on small screens so iOS Safari does not zoom on
  focus.
- Flex children that must shrink need `min-width: 0` (or equivalent). Icons, avatars,
  and fixed controls must not compress.
- Tables that cannot reflow scroll horizontally; table headers do not wrap.
- Touch targets: visual control may be small, hit area at least 44×44 (see Hit areas).
- Check narrow, medium, and desktop widths before shipping.

## Image outlines

A photo or screenshot floats without a defined edge, especially when its border
pixels are close in tone to the surface behind it. A 1px low-opacity outline gives
it an edge so it sits in the design like every other surface.

The color is **non-negotiable**:

- **Light mode:** pure black, `rgba(0, 0, 0, 0.1)` (R=0 G=0 B=0).
- **Dark mode:** pure white, `rgba(255, 255, 255, 0.1)` (R=255 G=255 B=255).

**Why:** never grab a near-black or near-white from the palette (slate-900,
zinc-900, `#0a0a0a`, `#f5f5f7`) and never the accent or ink color. The outline is a
neutral separator, not a themed element. A tinted outline picks up the surface tone
behind it and reads as dirt smeared along the image edge.

```tsx
<img
  className="outline outline-1 -outline-offset-1 outline-black/10 dark:outline-white/10"
  src={src}
  alt={alt}
/>
```

Use `outline`, not `border`. Outline doesn't add to the box size, and
`outline-offset: -1px` insets it so the image keeps its real dimensions.

## Hit areas

Interactive elements need at least a 40x40px hittable region (44x44 to satisfy
WCAG). When the visible control is smaller, like a 20px checkbox or a small icon
button, grow the hit area with a pseudo-element instead of padding the layout.

```tsx
<button className="relative size-5 after:absolute after:top-1/2 after:left-1/2 after:size-10 after:-translate-1/2">
  <CheckIcon />
</button>
```

**Why:** miss the floor and small controls become a game of tap-and-pray on touch.
But two interactive elements must never have overlapping hit areas either, because a
tap in the overlap is a coin flip. If the extended area would collide with a
neighbor, shrink it to the largest size that still clears.

## Buttons and primary action

One primary filled button per view (treat a dialog as its own view). Everything else
is secondary, quiet, outline, or ghost. Destructive actions stay secondary until they
are the confirm action in a dedicated confirm step. Icon-side padding matches the
optical rules above. Keep control height stable when labels or loading text change.

## Forms and controls

- Every field has a visible label (or an accessible name that is still clear). Placeholders
  are hints, not labels.
- Group related fields under a short section heading. Keep vertical rhythm steady; do
  not invent a new gap per field.
- Validation: message + icon (or text) beside the field, not color alone. Prefer
  inline errors next to the control that failed. See [color.md](./color.md) and the
  error shake recipe when motion helps.
- Native controls first. Style with CSS state (checked, disabled, focus); do not
  toggle classes from JS just to fake checked state.
- Checkboxes, radios, and toggles keep a usable hit area (see Hit areas) and stay
  larger on touch / small screens when the project allows.
- Selects need a consistent chevron and focus ring; do not rely on the ugliest
  OS default if the rest of the form is custom.
- Autocomplete, password managers, and zoom: inputs stay ≥16px on small viewports.

## Navigation and chrome

- One clear current-page / current-section indicator. Do not mark selection with color
  alone.
- Desktop header or sidebar is fine; below the desktop breakpoint ship a real mobile
  nav (menu button + panel/dialog). Hiding desktop links without a replacement is a bug.
- Horizontal tab/pill rows that cannot fit scroll horizontally; they never wrap into
  a ragged second line of tabs or overflow the page.
- Sidebars and filter columns collapse on small screens (see Responsive); do not
  squeeze them.

## Overlays and stacking

- Dropdowns, popovers, and menus that live inside `overflow: hidden` / scroll parents
  get clipped. Escape with a portal, `position: fixed`, popover/dialog API, or render
  outside the clipping ancestor.
- Keep a small semantic stack: dropdown → sticky → modal backdrop → modal → toast →
  tooltip. No `z-index: 9999` one-offs.
- Modals and dialogs trap focus while open, restore focus on close, and offer a clear
  dismiss (scrim click and/or Escape) unless the flow is deliberately blocking.
- Toasts and banners do not cover primary actions or the focus target without a way
  to dismiss.

## Data and product density

For dashboards, tables, and settings (product register):

- Prefer scanability over hero furniture. Status and primary actions stay findable
  without scrolling past marketing chrome.
- Tables: clear header row, consistent numeric alignment (`tabular-nums`),
  horizontal scroll when needed, no wrapped header labels.
- Metric / KPI strips: lightest separation (dividers or whitespace), not a card per
  stat by default.
- Truncate long titles with a plan (ellipsis + title/tooltip), not random wrap that
  blows row height.

## Empty, loading, and error

- Empty states explain what belongs here and offer one clear next action. No cute
  dead-ends.
- Loading: prefer skeletons or quiet placeholders that match final layout; avoid
  layout jump when content arrives (see skeleton transition when motion helps).
- Errors say what went wrong and how to fix or retry. Pair with [copy.md](./copy.md).
- First-run / onboarding moments can take more motion; daily empty lists stay quiet.

