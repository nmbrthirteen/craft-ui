# Success draw

A checkmark that draws itself once. Payment sent, upload finished, settings
saved.

This is the one place long motion is right: it confirms, it runs once, and the
user is watching. Never attach it to actions that repeat all day
([motion.md](../motion.md#1-should-this-animate-at-all)).

## HTML

```html
<svg class="cui-check" viewBox="0 0 24 24" aria-hidden="true">
  <path d="M5 12.5l4.5 4.5L19 7" pathLength="1" fill="none"
        stroke="currentColor" stroke-width="2.5"
        stroke-linecap="round" stroke-linejoin="round"/>
</svg>
```

## CSS

```css
.cui-check path {
  stroke-dasharray: 1;
  stroke-dashoffset: 1;
}

.cui-check.is-done path {
  stroke-dashoffset: 0;
  transition: stroke-dashoffset var(--motion-deliberate) var(--ease-out) 80ms;
}
```

## Notes

- `pathLength="1"` normalizes any path to length 1, so the dash math never
  needs `getTotalLength()` and you can swap in your own checkmark path
  untouched.
- The 80ms delay gives whatever just happened (button swap, modal close) a
  beat to settle so the draw reads as its own moment.
- Replay for testing: remove `is-done`, read `el.offsetWidth` to force a
  reflow, add it back.
- Pair with a circle or badge behind it entering one token faster
  (`--motion-slow`), so the stage arrives before the performance.
