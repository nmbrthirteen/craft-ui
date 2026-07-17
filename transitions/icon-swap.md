# Icon swap

Two icons trading one slot: play/pause, menu/close, copy/check, sun/moon.

Pure CSS off the attribute the control already toggles.

## HTML

```html
<button class="cui-icon-swap" aria-pressed="false" aria-label="Play">
  <svg class="cui-icon-a">…</svg>
  <svg class="cui-icon-b">…</svg>
</button>
```

## CSS

```css
.cui-icon-swap {
  display: inline-grid;
  place-items: center;
}

.cui-icon-swap > svg {
  grid-area: 1 / 1;
  transition:
    opacity var(--motion-fast) var(--ease-out),
    rotate var(--motion-base) var(--ease-out),
    scale var(--motion-base) var(--ease-out);
}

.cui-icon-b {
  opacity: 0;
  rotate: -60deg;
  scale: 0.6;
}

.cui-icon-swap[aria-pressed="true"] .cui-icon-a {
  opacity: 0;
  rotate: 60deg;
  scale: 0.6;
}

.cui-icon-swap[aria-pressed="true"] .cui-icon-b {
  opacity: 1;
  rotate: 0deg;
  scale: 1;
}
```

## Notes

- Opacity runs a token faster than rotate and scale, so mid-swap you never see
  both icons at full strength fighting for the slot.
- The counter-rotation makes the pair feel like one object turning. Drop the
  `rotate` lines for direction-bearing icons (arrows, chevrons) and keep
  opacity plus scale.
- `aria-pressed` fits toggles. For one-way swaps like copy turning into a
  check, drive the same selectors from `data-state="done"` instead.
- Update `aria-label` alongside the state, or the control announces the wrong
  action.
