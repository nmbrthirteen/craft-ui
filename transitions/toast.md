# Toast

A notification that slides into a corner stack and leaves on its own.

Enter is free: `@starting-style` fires when the element is inserted. Exit is
one class and one `transitionend`.

## HTML

```html
<div class="cui-toast-stack" aria-live="polite"></div>
```

Append each toast to the stack inside a slot wrapper:

```html
<div class="cui-toast-slot"><div class="cui-toast">Saved</div></div>
```

## CSS

```css
.cui-toast {
  transition:
    opacity var(--motion-base) var(--ease-out),
    translate var(--motion-base) var(--ease-out),
    scale var(--motion-base) var(--ease-out);

  @starting-style {
    opacity: 0;
    translate: 0 calc(16px * var(--motion-travel));
  }
}

.cui-toast-slot {
  display: grid;
  grid-template-rows: 1fr;
  transition: grid-template-rows var(--motion-base) var(--ease-out);
}

.cui-toast-slot[data-state="leaving"] {
  grid-template-rows: 0fr;
  transition-duration: var(--motion-fast);
}

.cui-toast-slot[data-state="leaving"] .cui-toast {
  opacity: 0;
  scale: calc(1 - 0.04 * var(--motion-travel));
  overflow: clip;
  transition-duration: var(--motion-fast);
}
```

## JS

```js
function dismiss(slot) {
  slot.dataset.state = "leaving";
  slot.addEventListener("transitionend", () => slot.remove(), { once: true });
}
```

## Notes

- The slot's `1fr` to `0fr` collapse is what closes the gap, so the rest of the
  stack glides up instead of jumping when a toast leaves. It is the
  size-to-content case of the
  [reveal exception](../motion.md#the-reveal-exception).
- Enter runs `--motion-base`, exit `--motion-fast`: one step below, per the
  catalog's exit rule.
- Enter slides up from below; exit fades in place with a slight shrink. Leaving
  the way it came would look dismissed by the user, and it wasn't.
- `aria-live="polite"` on the stack, once, not per toast.
- Cap the stack around three; dismiss the oldest when a new one lands.
