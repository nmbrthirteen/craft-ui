# Staggered entrance

Children of a newly revealed group arriving one after another. Hero copy, empty
states, onboarding steps, the first paint of a short list.

## HTML

```html
<div class="cui-stagger">
  <h1 style="--i: 0">Ship the audit in a day</h1>
  <p style="--i: 1">Findings, evidence, and fixes in one export.</p>
  <a style="--i: 2" href="/start">Start free</a>
</div>
```

## CSS

```css
.cui-stagger > * {
  transition:
    opacity var(--motion-slow) var(--ease-out),
    translate var(--motion-slow) var(--ease-out);
  transition-delay: calc(var(--i, 0) * var(--motion-stagger));

  @starting-style {
    opacity: 0;
    translate: 0 10px;
  }
}
```

## Notes

- `--i` is set inline per child; when rendering a list, write it from the loop
  index. `sibling-index()` will make this automatic once it's broadly shipped.
- Entrances only. Exits leave as one motion; a staggered exit makes the user
  wait for furniture ([motion.md](../motion.md#entrances-split-and-stagger)).
- 30ms is the default step. Hero copy can stretch to 60-80ms by overriding
  `--motion-stagger` on the group; past about eight items, clamp `--i` so the
  tail arrives together.
- This is for moments, once per view. A staggered dropdown menu on every open
  becomes a toll.
