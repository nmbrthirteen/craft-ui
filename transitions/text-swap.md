# Text swap

Inline text or a number that changes in place: prices, counters, statuses,
button labels.

Old and new occupy the same grid cell, so layout never jumps; the old value
slides up and out while the new one slides up and in.

## HTML

```html
<span class="cui-swap"><span>$29</span></span>
```

## CSS

```css
.cui-swap {
  display: inline-grid;
  overflow: clip;
  font-variant-numeric: tabular-nums;
}

.cui-swap > * {
  grid-area: 1 / 1;
  transition:
    opacity var(--motion-base) var(--ease-out),
    translate var(--motion-base) var(--ease-out);

  @starting-style {
    opacity: 0;
    translate: 0 0.6em;
  }
}

.cui-swap > .is-out {
  opacity: 0;
  translate: 0 -0.6em;
}
```

## JS

```js
function swapText(host, next) {
  for (const child of host.children) {
    child.classList.add("is-out");
    child.addEventListener("transitionend", () => child.remove(), {
      once: true,
    });
  }
  const span = document.createElement("span");
  span.textContent = next;
  host.append(span);
}
```

## Notes

- Inserting the new node is what triggers `@starting-style`; no reflow tricks
  needed on this one.
- Everything moves upward, which reads as the value advancing. If direction
  carries meaning (a price dropping), add a `data-dir="down"` variant with the
  signs flipped.
- `tabular-nums` holds the width steady for numeric swaps
  ([typography.md](../typography.md)).
- The loop marks all children out, not just the last, so a rapid double update
  can't strand a ghost value.
