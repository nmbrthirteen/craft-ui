# Tooltip

Hover and focus hint over a trigger. Pure CSS.

The rule: slow to appear, instant to leave. The delay filters accidental
hovers; the immediate exit gets out of the way the moment attention moves on.

## HTML

```html
<button class="cui-tip-trigger" aria-describedby="tip-copy">
  <svg aria-hidden="true">…</svg>
  <span role="tooltip" id="tip-copy" class="cui-tip">Copy link</span>
</button>
```

## CSS

```css
.cui-tip-trigger {
  position: relative;
}

.cui-tip {
  position: absolute;
  bottom: calc(100% + 6px);
  left: 50%;
  translate: -50% 2px;
  opacity: 0;
  pointer-events: none;
  white-space: nowrap;
  transition:
    opacity var(--motion-fast) var(--ease-out),
    translate var(--motion-fast) var(--ease-out);
}

.cui-tip-trigger:hover .cui-tip,
.cui-tip-trigger:focus-visible .cui-tip {
  opacity: 1;
  translate: -50% 0;
  transition-delay: 400ms;
}
```

## Notes

- The 400ms delay lives only on the shown state, so hiding starts immediately.
- Skipping the delay while moving between neighbors in a toolbar needs a few
  lines of JS (a "tooltips are warm" timer); worth it in icon-dense UI
  ([motion.md](../motion.md) covers the perceived-speed reasoning).
- `role="tooltip"` plus `aria-describedby` keeps it announced. Never put
  anything interactive inside.
- The delay is a wait, and the token collapse kills the movement, so reduced
  motion needs nothing extra here.
