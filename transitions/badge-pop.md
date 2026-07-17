# Badge pop

A count badge that pops in when it appears and bumps when the number changes.

## HTML

```html
<button class="cui-badge-host">
  Inbox
  <span class="cui-badge">3</span>
</button>
```

## CSS

```css
.cui-badge-host {
  position: relative;
}

.cui-badge {
  position: absolute;
  top: -6px;
  right: -6px;
  font-variant-numeric: tabular-nums;
  transition:
    scale var(--motion-base) var(--ease-pop),
    opacity var(--motion-fast) var(--ease-out);

  @starting-style {
    scale: 0.5;
    opacity: 0;
  }
}

.cui-badge.is-bumped {
  animation: cui-bump var(--motion-base) var(--ease-pop);
}

@keyframes cui-bump {
  50% { scale: 1.25; }
}
```

## JS

```js
function setCount(badge, n) {
  badge.textContent = n;
  badge.classList.remove("is-bumped");
  void badge.offsetWidth;
  badge.classList.add("is-bumped");
}
```

## Notes

- `--ease-pop` is the only overshoot in the token set, and this is the kind of
  moment that earns it: small, rare, and worth a wink. It never becomes the
  house curve ([motion.md](../motion.md#3-which-easing)).
- Enter from `scale: 0.5`, respecting the floor's ban on `scale(0)` entrances;
  at badge size the half-scale start still reads as popping from nothing.
- `tabular-nums` so 9 to 10 doesn't wobble the pill width
  ([typography.md](../typography.md)).
- Count going to zero: fade the badge out with a plain opacity transition, no
  pop. Removal is not an event to celebrate.
