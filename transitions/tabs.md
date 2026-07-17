# Sliding tabs

A tab list or segmented control where the active highlight slides between
options.

Two copies of the list are stacked. The top copy is styled fully active and
clipped to a window; moving the window is the entire animation. Label colors
cross over inside the moving edge for free, which per-tab color transitions
can't reproduce ([motion.md](../motion.md) describes the technique).

## HTML

```html
<div class="cui-tabs">
  <div class="cui-tabs-row" role="tablist">
    <button role="tab" aria-selected="true">Day</button>
    <button role="tab" aria-selected="false">Week</button>
    <button role="tab" aria-selected="false">Month</button>
  </div>
  <div class="cui-tabs-row cui-tabs-overlay" aria-hidden="true">
    <button tabindex="-1">Day</button>
    <button tabindex="-1">Week</button>
    <button tabindex="-1">Month</button>
  </div>
</div>
```

## CSS

```css
.cui-tabs {
  position: relative;
}

.cui-tabs-overlay {
  position: absolute;
  inset: 0;
  pointer-events: none;
  background: var(--cui-tabs-pill, #111);
  color: var(--cui-tabs-pill-text, #fff);
  clip-path: inset(0 100% 0 0 round 999px);
  transition: clip-path var(--motion-base) var(--ease-out);
}
```

## JS

```js
const row = tabs.querySelector("[role=tablist]");
const overlay = tabs.querySelector(".cui-tabs-overlay");

function moveTo(tab) {
  const right = row.offsetWidth - tab.offsetLeft - tab.offsetWidth;
  overlay.style.clipPath =
    `inset(0 ${right}px 0 ${tab.offsetLeft}px round 999px)`;
}

function place() {
  overlay.style.transition = "none";
  moveTo(row.querySelector('[aria-selected="true"]'));
  requestAnimationFrame(() => (overlay.style.transition = ""));
}

place();
new ResizeObserver(place).observe(row);
```

On tab click, update `aria-selected` and call `moveTo(tab)`.

## Notes

- `aria-selected` is the state; the overlay copy is `aria-hidden` with
  `tabindex="-1"` so assistive tech and Tab order only ever see the real row.
- `place()` writes the first position with transitions suppressed. Skip that
  and the pill animates in from the far edge on page load and on every resize.
- The `round 999px` matches a pill highlight. For an underline style, clip a
  strip instead: `inset(calc(100% - 2px) RIGHTpx 0 LEFTpx)`.
- Both rows must share identical layout styles (`.cui-tabs-row`), or the clip
  window and the real tabs drift apart.
