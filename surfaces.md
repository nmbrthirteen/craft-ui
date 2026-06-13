# Surfaces

Border radius, optical alignment, depth, image edges, hit areas. The details nobody
points at and everybody feels.

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
before a solid border.

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

In dark mode the layered depth disappears against the dark surface, so collapse it
to a single white ring:

```css
/* dark theme: match the project's mechanism (class, data-attr, media query) */
--shadow-border:       0 0 0 1px rgba(255, 255, 255, 0.08);
--shadow-border-hover: 0 0 0 1px rgba(255, 255, 255, 0.13);
```

This is about depth, not separation. A `border-b` between list rows, a table cell
boundary, a form input outline, a hairline in dense UI: those draw a line, they
don't lift anything. Leave them as borders.

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
