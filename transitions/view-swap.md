# View swap

One region of the page replaced by another: step to step in a flow, list to
detail, tab panels with real content.

Built on the View Transitions API: one JS wrapper, all choreography in CSS.

## JS

```js
function swapView(render) {
  if (!document.startViewTransition) return render();
  document.startViewTransition(render);
}
```

`render` is whatever already updates the DOM (framework state change included).

## CSS

```css
main {
  view-transition-name: view;
}

::view-transition-old(view) {
  animation: cui-view-out var(--motion-base) var(--ease-in-out) both;
}

::view-transition-new(view) {
  animation: cui-view-in var(--motion-base) var(--ease-in-out) both;
}

@keyframes cui-view-out {
  to {
    opacity: 0;
    translate: -24px 0;
  }
}

@keyframes cui-view-in {
  from {
    opacity: 0;
    translate: 24px 0;
  }
}
```

## Notes

- Forward slides left. For back navigation, set `data-direction="back"` on
  `<html>` before the swap and flip the translate signs under
  `html[data-direction="back"]` selectors.
- Browsers without the API run `render()` directly and show the new view
  instantly. Correct fallback: navigation is function, the slide is polish.
- Same-document only as written. For full page navigations, add
  `@view-transition { navigation: auto; }` and the same keyframes work
  cross-document.
- The keyframes read `--motion-base`, so the reduced-motion token collapse
  covers them too.
