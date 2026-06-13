# Icon swap

## When to use

Cross-fading two icons in the same slot: hamburger to close, sun to moon, play to pause, expand to collapse. Both icons stay in the DOM stacked in the same grid cell.

## HTML usage

```html
<div class="t-icon-swap" data-state="a">
  <span class="t-icon" data-icon="a">…</span>
  <span class="t-icon" data-icon="b">…</span>
</div>
```

State: set data-state="a" or "b" on .t-icon-swap.
The matching .t-icon fades in; the other fades out with blur
and scale.

## Tunable variables

| Variable | Default | Notes |
| --- | --- | --- |
| `--icon-swap-dur` | `250ms` | sourced from `--p5-dur` |
| `--icon-swap-blur` | `2px` | sourced from `--p5-blur` |
| `--icon-swap-start-scale` | `0.25` | sourced from `--p5-start-scale` |
| `--icon-swap-ease` | `ease-in-out` | sourced from `--p5-ease` |

The `:root` defaults below are the tuned values for this transition. Drop them into your global stylesheet once. Every transition in this skill reads from semantic names like these, so multiple transitions can share a single `:root` block.

```css
:root {
  --icon-swap-dur: 250ms;
  --icon-swap-blur: 2px;
  --icon-swap-start-scale: 0.25;
  --icon-swap-ease: ease-in-out;
}
```

## CSS

```css
.t-icon-swap {
  position: relative;
  display: inline-grid;
}
.t-icon-swap .t-icon {
  grid-area: 1 / 1;
  transition:
    opacity   var(--icon-swap-dur) var(--icon-swap-ease),
    filter    var(--icon-swap-dur) var(--icon-swap-ease),
    transform var(--icon-swap-dur) var(--icon-swap-ease);
  will-change: opacity, filter, transform;
}
.t-icon-swap[data-state="a"] .t-icon[data-icon="a"],
.t-icon-swap[data-state="b"] .t-icon[data-icon="b"] {
  opacity: 1;
  filter: blur(0);
  transform: scale(1);
}
.t-icon-swap[data-state="a"] .t-icon[data-icon="b"],
.t-icon-swap[data-state="b"] .t-icon[data-icon="a"] {
  opacity: 0;
  filter: blur(var(--icon-swap-blur));
  transform: scale(var(--icon-swap-start-scale));
}

@media (prefers-reduced-motion: reduce) {
  .t-icon-swap .t-icon { transition: none !important; }
}
```

The `@media (prefers-reduced-motion: reduce)` guard at the bottom of the snippet is required. Keep it. It zeroes the transition for users who have asked for less motion at the OS level.

## JavaScript orchestration

None. Pure CSS. Toggle the documented HTML attributes or class names from whatever already drives state in your app.

