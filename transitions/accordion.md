# Accordion

Expand and collapse to the content's natural height without measuring anything.
Also the recipe for any container whose height changes with state: FAQ items,
expanding cards, "show more" sections.

Built on `<details>`, so keyboard and semantics come free.

## HTML

```html
<details class="cui-acc">
  <summary>Can I change plans later?</summary>
  <div class="cui-acc-body">…</div>
</details>
```

## CSS

```css
:root {
  interpolate-size: allow-keywords;
}

.cui-acc::details-content {
  block-size: 0;
  overflow: clip;
  transition:
    block-size var(--motion-slow) var(--ease-out),
    content-visibility var(--motion-slow) allow-discrete;
}

.cui-acc[open]::details-content {
  block-size: auto;
}

.cui-acc summary .chevron {
  transition: rotate var(--motion-slow) var(--ease-out);
}

.cui-acc[open] summary .chevron {
  rotate: 90deg;
}
```

## Notes

- `interpolate-size: allow-keywords` is what lets `block-size` tween to `auto`.
  Where unsupported the accordion still opens, it just snaps: the right
  fallback, since the tween is polish and the disclosure is function.
- For a non-`<details>` container, put the same `block-size` transition on a
  wrapper and toggle a `data-open` attribute; the mechanics are identical.
- Chevron rotates in the same duration as the body so the two read as one
  action.
- Collapse reuses the same timing by design; a snappier close is a
  `transition-duration: var(--motion-base)` override on the non-open state.
