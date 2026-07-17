# Button loading

A button that trades its label for a spinner while work runs, without moving a
pixel of layout.

State is `aria-busy`, which the button should carry anyway; the CSS reads it so
the visuals can't drift out of sync with what's announced.

## HTML

```html
<button class="cui-btn">
  <span class="cui-btn-label">Save changes</span>
  <span class="cui-btn-spinner" aria-hidden="true"></span>
</button>
```

## CSS

```css
.cui-btn {
  position: relative;
}

.cui-btn-label {
  transition:
    opacity var(--motion-fast) var(--ease-out),
    translate var(--motion-fast) var(--ease-out);
}

.cui-btn-spinner {
  position: absolute;
  inset: 0;
  display: grid;
  place-items: center;
  opacity: 0;
  translate: 0 4px;
  transition:
    opacity var(--motion-fast) var(--ease-out),
    translate var(--motion-fast) var(--ease-out);
}

.cui-btn-spinner::after {
  content: "";
  width: 1em;
  height: 1em;
  border-radius: 50%;
  border: 2px solid currentColor;
  border-inline-start-color: transparent;
  animation: cui-spin 600ms linear infinite;
}

.cui-btn[aria-busy="true"] {
  pointer-events: none;
}

.cui-btn[aria-busy="true"] .cui-btn-label {
  opacity: 0;
  translate: 0 -4px;
}

.cui-btn[aria-busy="true"] .cui-btn-spinner {
  opacity: 1;
  translate: 0 0;
}

@keyframes cui-spin {
  to {
    rotate: 1turn;
  }
}

@media (prefers-reduced-motion: reduce) {
  .cui-btn-spinner::after {
    animation: cui-spin 1.6s steps(8) infinite;
  }
}
```

## Notes

- The spinner is absolutely positioned over the label, so the button keeps the
  label's width and nothing reflows.
- `pointer-events: none` plus `aria-busy`, rather than `disabled`: `disabled`
  throws keyboard focus somewhere else mid-action.
- The spinner is a progress indicator, so reduced motion slows it to a stepped
  tick instead of removing it; a frozen ring reads as hung.
- On success, clear `aria-busy` and chain [success-draw](./success-draw.md)
  in the label slot if the moment deserves it.
