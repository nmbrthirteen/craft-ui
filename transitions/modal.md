# Modal

Centered dialog over a dimmed page. Confirmations, focused forms, anything that
blocks the flow until answered.

Built on `<dialog>` + `showModal()`: focus trap, Esc, inert background, and
`::backdrop` come free.

## HTML

```html
<dialog class="cui-modal">…</dialog>
```

Open with `dialog.showModal()`, close with `dialog.close()`.

## CSS

```css
.cui-modal {
  opacity: 0;
  translate: 0 calc(12px * var(--motion-travel));
  scale: calc(1 - 0.02 * var(--motion-travel));
  transition:
    opacity var(--motion-base) var(--ease-out),
    translate var(--motion-base) var(--ease-out),
    scale var(--motion-base) var(--ease-out),
    display var(--motion-base) allow-discrete,
    overlay var(--motion-base) allow-discrete;
}

.cui-modal[open] {
  opacity: 1;
  translate: 0 0;
  scale: 1;
  transition-duration: var(--motion-slow);

  @starting-style {
    opacity: 0;
    translate: 0 calc(12px * var(--motion-travel));
    scale: calc(1 - 0.02 * var(--motion-travel));
  }
}

.cui-modal::backdrop {
  background: rgb(0 0 0 / 0.4);
  opacity: 0;
  transition:
    opacity var(--motion-base) var(--ease-out),
    display var(--motion-base) allow-discrete,
    overlay var(--motion-base) allow-discrete;
}

.cui-modal[open]::backdrop {
  opacity: 1;
  transition-duration: var(--motion-slow);

  @starting-style {
    opacity: 0;
  }
}
```

## Notes

- Close with `dialog.close()`, never by hiding the element yourself, or the exit
  transition is skipped.
- The small rise plus scale reads as the dialog arriving. A bare opacity fade on
  a large surface reads as a rendering glitch.
- The backdrop keeps a fixed color and fades with `opacity`, which stays on the
  compositor. Animating `background` would repaint every frame.
- Backdrop around 0.4 opacity. Near-black behind a modal turns the page into a
  photo lightbox.
- Enter runs `--motion-slow`, exit `--motion-base`: the user asked for the
  modal, they only tolerate its exit.
