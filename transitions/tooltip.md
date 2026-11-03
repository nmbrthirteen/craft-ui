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
  translate: -50% calc(2px * var(--motion-travel));
  opacity: 0;
  pointer-events: none;
  white-space: nowrap;
  transition:
    opacity var(--motion-fast) var(--ease-out),
    translate var(--motion-fast) var(--ease-out);
}

.cui-tip-trigger:focus-visible .cui-tip {
  opacity: 1;
  translate: -50% 0;
  transition-delay: var(--motion-delay-hint);
}

@media (hover: hover) and (pointer: fine) {
  .cui-tip-trigger:hover .cui-tip {
    opacity: 1;
    translate: -50% 0;
    transition-delay: var(--motion-delay-hint);
  }
}
```

## Notes

- `--motion-delay-hint` (400ms) lives only on the shown state, so hiding starts immediately.
- Skipping the delay while moving between neighbors in a toolbar needs a few
  lines of JS (a "tooltips are warm" timer); worth it in icon-dense UI
  ([motion.md](../motion.md) covers the perceived-speed reasoning).
- Hover is gated to real pointers so a tap on touch doesn't leave the tip stuck
  open. Focus stays ungated, so keyboard users always get the hint.
- `role="tooltip"` plus `aria-describedby` keeps it announced. Never put
  anything interactive inside.
- The delay is a wait and `--motion-travel` zeroes the 2px rise, so reduced
  motion needs nothing extra here.
