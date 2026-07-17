# Drawer

A panel that slides in from an edge. Settings, carts, mobile nav, detail views
too heavy for a dropdown and too light for a page.

Also `<dialog>` + `showModal()`; only the geometry differs from
[modal](./modal.md).

## CSS

```css
.cui-drawer {
  position: fixed;
  inset: 0 0 0 auto;
  height: 100dvh;
  width: min(24rem, 90vw);
  max-height: none;
  margin: 0;
  translate: 100% 0;
  transition:
    translate var(--motion-base) var(--ease-out),
    display var(--motion-base) allow-discrete,
    overlay var(--motion-base) allow-discrete;
}

.cui-drawer[open] {
  translate: 0 0;
  transition-duration: var(--motion-slow);

  @starting-style {
    translate: 100% 0;
  }
}

.cui-drawer::backdrop {
  background: rgb(0 0 0 / 0);
  transition:
    background var(--motion-base) var(--ease-out),
    display var(--motion-base) allow-discrete,
    overlay var(--motion-base) allow-discrete;
}

.cui-drawer[open]::backdrop {
  background: rgb(0 0 0 / 0.4);
  transition-duration: var(--motion-slow);

  @starting-style {
    background: rgb(0 0 0 / 0);
  }
}
```

## Notes

- Left edge: `inset: 0 auto 0 0` and `translate: -100% 0`. Bottom sheet:
  `inset: auto 0 0 0`, `height: auto`, `translate: 0 100%`.
- Slide only. Fading a full-height surface while it moves makes the page behind
  shimmer through it.
- `100dvh`, not `100vh`, so mobile browser chrome never crops the drawer footer.
- The `inset`/`margin` resets override the UA's centered-dialog defaults.
