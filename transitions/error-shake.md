# Error shake

Invalid input feedback: a short horizontal shake on the field plus the message
arriving beneath it.

State is `aria-invalid`, which the field needs anyway; the CSS reads it so the
animation can't fire without the semantics.

## HTML

```html
<input class="cui-field" aria-invalid="true" aria-describedby="err-email">
<p class="cui-field-error" id="err-email">Enter a valid email.</p>
```

## CSS

```css
.cui-field[aria-invalid="true"] {
  border-color: var(--cui-danger, #d43c3c);
  animation: cui-shake var(--motion-slow) var(--ease-in-out);
}

@keyframes cui-shake {
  20% { translate: -5px 0; }
  45% { translate: 4px 0; }
  70% { translate: -2px 0; }
  90% { translate: 1px 0; }
}

.cui-field-error {
  color: var(--cui-danger, #d43c3c);
  transition:
    opacity var(--motion-base) var(--ease-out),
    translate var(--motion-base) var(--ease-out);

  @starting-style {
    opacity: 0;
    translate: 0 -4px;
  }
}
```

## JS

Re-shake when the user resubmits while still invalid:

```js
field.style.animation = "none";
void field.offsetWidth;
field.style.animation = "";
```

## Notes

- Shake once and stop. A looping or repeating shake is an alarm, and the second
  trigger should come only from the user acting again.
- The decaying distances (5, 4, 2, 1) read as a physical settle; equal swings
  read as a metronome.
- Shake the field alone. If the label and message swing too, the whole form
  panics.
- The message must say what's wrong; the shake plus red is never enough on its
  own ([color.md](../color.md): never color alone).
