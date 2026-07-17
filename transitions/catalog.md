# Transition catalog

Sixteen paste-ready CSS transitions on one token set. Decide first, then pick:
whether to animate, which easing family, how fast all live in
[../motion.md](../motion.md). This file is the implementation shelf.

The recipes are CSS-first. Most ride `@starting-style` and
`transition-behavior: allow-discrete` on native primitives (`popover`,
`<dialog>`, `<details>`), so inserting a node or toggling an attribute is the
whole trigger, and JS appears only where the platform has no primitive yet.

## Shared conventions

- **Tokens** come from [`_root.css`](./_root.css): four durations, three eases,
  one stagger step. Recipes never hardcode timing.
- **Exits step down one token** from their enter (open at `--motion-slow`,
  close at `--motion-base`). The user asked for the surface; they only tolerate
  its exit.
- **State lives in attributes the UI already needs**: `aria-selected`,
  `aria-invalid`, `aria-busy`, `aria-pressed`, `[open]`, `:popover-open`.
  Styling reads those directly, so visuals can't drift out of sync with
  semantics, and there is no parallel class for JS to forget.
- **Reduced motion is one switch**: the token collapse in `_root.css` covers
  every tokened transition and keyframe. The two recipes with untokened
  ambient animation (skeleton pulse, button spinner) carry their own guard.
- **Class prefix `cui-`** keeps the recipes collision-free; rename to the
  project's convention when pasting.

## The sixteen

**Overlays**

| Transition | When | Recipe |
| --- | --- | --- |
| Dropdown | Anchored surface grows from its trigger | [dropdown.md](./dropdown.md) |
| Modal | Centered dialog over a dimmed page | [modal.md](./modal.md) |
| Drawer | Panel slides in from an edge | [drawer.md](./drawer.md) |
| Tooltip | Delayed hover hint, instant exit | [tooltip.md](./tooltip.md) |
| Toast | Self-dismissing corner notification, stack closes its own gap | [toast.md](./toast.md) |

**Disclosure and navigation**

| Transition | When | Recipe |
| --- | --- | --- |
| Accordion | Height-to-auto without measuring; any container that resizes with state | [accordion.md](./accordion.md) |
| Sliding tabs | Active highlight glides between options | [tabs.md](./tabs.md) |
| View swap | One region replaced by another (step, list-to-detail) | [view-swap.md](./view-swap.md) |

**Feedback**

| Transition | When | Recipe |
| --- | --- | --- |
| Button loading | Label trades places with a spinner, layout holds | [button-loading.md](./button-loading.md) |
| Success draw | Checkmark draws itself once | [success-draw.md](./success-draw.md) |
| Error shake | Invalid field shakes, message arrives | [error-shake.md](./error-shake.md) |
| Badge pop | Count appears or bumps | [badge-pop.md](./badge-pop.md) |

**Content**

| Transition | When | Recipe |
| --- | --- | --- |
| Skeleton to content | Placeholder pulse, quiet handoff | [skeleton.md](./skeleton.md) |
| Text swap | Inline value changes in place | [text-swap.md](./text-swap.md) |
| Icon swap | Two icons trade one slot | [icon-swap.md](./icon-swap.md) |
| Staggered entrance | Group's children arrive in rhythm, once | [stagger.md](./stagger.md) |

## Picking

Match the visible element, then the verb:

- Surface anchored to a trigger: **dropdown**. Centered and blocking:
  **modal**. From an edge: **drawer**. Corner, leaves on its own: **toast**.
  Hover hint over a control: **tooltip**.
- A container's height changes with state (FAQ, show-more, expanding card):
  **accordion**, whose mechanics cover any resize-to-content.
- A highlight moves across mutually exclusive options: **sliding tabs**.
- A whole region's content is replaced: **view swap**.
- Something changes in place: words or numbers, **text swap**; icons,
  **icon swap**; a count on a dot, **badge pop**.
- An async action runs from a button: **button loading**; it finished,
  **success draw**; it failed validation, **error shake**.
- Content is on its way: **skeleton**. A view's first reveal: **staggered
  entrance**.

When two fit, take the lighter one: accordion over view swap, dropdown over
modal, text swap over a full region transition. When none fits, that usually
means the answer is no animation ([../motion.md](../motion.md#the-decision)).

## Installing

1. Add [`_root.css`](./_root.css) to the global stylesheet once. Projects with
   existing motion tokens: map names instead of duplicating scales.
2. Paste the recipe. Keep the property lists enumerated; `transition: all` is
   a floor violation, and the enumerated lists are what keep unrelated style
   changes from riding along.
3. Wire the state attribute the recipe documents. If the project toggles a
   different attribute or class, adapt the selector, never bolt on a second
   state.
4. Keep the reduced-motion behavior: the token collapse, plus the local guards
   in skeleton and button-loading.
5. Baseline: `@starting-style` and `allow-discrete` are cross-browser as of
   2024\. Where a recipe leans newer (`interpolate-size`, view transitions),
   its notes name the fallback, and the fallback is always "works, without the
   tween".
