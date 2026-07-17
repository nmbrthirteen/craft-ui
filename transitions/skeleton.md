# Skeleton to content

A placeholder that pulses while loading, then hands off to the real content
with a quiet crossfade.

## HTML

```html
<div class="cui-skeleton" aria-hidden="true">…placeholder blocks…</div>
```

When data lands, replace it with the real markup inside a `.cui-loaded`
container.

## CSS

```css
.cui-skeleton {
  animation: cui-skeleton-pulse 1.8s var(--ease-in-out) infinite;
}

@keyframes cui-skeleton-pulse {
  50% { opacity: 0.55; }
}

.cui-loaded {
  transition: opacity var(--motion-slow) var(--ease-out);

  @starting-style {
    opacity: 0;
  }
}

@media (prefers-reduced-motion: reduce) {
  .cui-skeleton {
    animation: none;
    opacity: 0.75;
  }
}
```

## Notes

- The skeleton must match the real content's geometry: same radii, same line
  heights, same block count. If the reveal shifts layout, the transition reads
  as a bug regardless of how smooth the fade is.
- Pulse opacity on the whole placeholder rather than sweeping a shimmer band:
  cheaper, calmer, and it doesn't fight the content fade at handoff.
- Fade the loaded container in once. Don't stagger rows arriving from a fetch;
  loading is not an entrance to celebrate.
- Delay showing the skeleton by 150-300ms (CSS `animation-delay` on a fade-in,
  or a JS timer). Fast responses should never flash a placeholder.
- The pulse duration is intentionally untokened; it's ambient, not an event,
  so the reduced-motion block handles it explicitly.
