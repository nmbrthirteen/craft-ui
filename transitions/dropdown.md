# Dropdown

An anchored surface that grows out of its trigger. Menus, selects, comboboxes.
For a centered surface with no anchor, use [modal](./modal.md).

Built on the native popover attribute, so light dismiss, stacking, and Esc come
free and there is no open/close JS to write.

## HTML

```html
<button popovertarget="menu">Options</button>
<div id="menu" popover class="cui-dropdown">…</div>
```

## CSS

```css
.cui-dropdown {
  opacity: 0;
  scale: 0.96;
  transform-origin: top;
  transition:
    opacity var(--motion-fast) var(--ease-out),
    scale var(--motion-fast) var(--ease-out),
    display var(--motion-fast) allow-discrete,
    overlay var(--motion-fast) allow-discrete;
}

.cui-dropdown:popover-open {
  opacity: 1;
  scale: 1;
  transition-duration: var(--motion-base);

  @starting-style {
    opacity: 0;
    scale: 0.96;
  }
}
```

## Notes

- Transitions read their timing from the destination state, so the closed state
  carrying `--motion-fast` and the open state overriding to `--motion-base` is
  what makes closing faster than opening
  ([motion.md](../motion.md#6-enter-and-exit-arent-symmetric)).
- `transform-origin` must match the anchor side: `top` for a menu below the
  trigger, `bottom` above it, `top left` when it hangs off a corner. Growth from
  anywhere but the trigger breaks the illusion that the trigger produced it.
- Position with CSS anchor positioning where available, otherwise whatever
  positioning you already have. The recipe owns only the enter and exit.
- Reduced motion is covered by the token collapse in [`_root.css`](./_root.css).
