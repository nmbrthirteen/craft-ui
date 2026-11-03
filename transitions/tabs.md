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
    <button role="tab" aria-selected="true" tabindex="0">Day</button>
    <button role="tab" aria-selected="false" tabindex="-1">Week</button>
    <button role="tab" aria-selected="false" tabindex="-1">Month</button>
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

@media (prefers-reduced-motion: reduce) {
  .cui-tabs-overlay {
    transition: none;
  }
}
```

## JS

```js
const tabs = document.querySelector(".cui-tabs");
const row = tabs.querySelector("[role=tablist]");
const overlay = tabs.querySelector(".cui-tabs-overlay");
const items = [...row.querySelectorAll("[role=tab]")];

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

function select(tab) {
  for (const item of items) {
    const selected = item === tab;
    item.setAttribute("aria-selected", selected);
    item.tabIndex = selected ? 0 : -1;
  }
  moveTo(tab);
}

row.addEventListener("click", (event) => {
  const tab = event.target.closest("[role=tab]");
  if (tab) select(tab);
});

row.addEventListener("keydown", (event) => {
  const current = items.indexOf(document.activeElement);
  const target = {
    ArrowLeft: (current - 1 + items.length) % items.length,
    ArrowRight: (current + 1) % items.length,
    Home: 0,
    End: items.length - 1,
  }[event.key];
  if (current === -1 || target === undefined) return;
  event.preventDefault();
  items[target].focus();
  select(items[target]);
});

place();
new ResizeObserver(place).observe(row);
```

## Notes

- Animating `clip-path` is the clip case of the
  [reveal exception](../motion.md#the-reveal-exception).
- Roving `tabindex`: only the selected tab is in the Tab order, and arrow keys,
  Home, and End move focus and selection together (automatic activation).
  Under reduced motion the highlight jumps instead of sliding.
- `aria-selected` is the state; the overlay copy is `aria-hidden` with
  `tabindex="-1"` so assistive tech and Tab order only ever see the real row.
- `place()` writes the first position with transitions suppressed. Skip that
  and the pill animates in from the far edge on page load and on every resize.
- The `round 999px` matches a pill highlight. For an underline style, clip a
  strip instead: `inset(calc(100% - 2px) RIGHTpx 0 LEFTpx)`.
- Both rows must share identical layout styles (`.cui-tabs-row`), or the clip
  window and the real tabs drift apart.
