# Transition catalog

Eighteen production-ready CSS transitions. Each one is namespaced under `t-*`
selectors, reads its values from semantic custom properties, and ships a
`prefers-reduced-motion` guard. These are tuned and tested, so paste them verbatim,
wire the documented HTML hooks, and move on. Don't collapse them into shorthand,
don't strip `will-change`, don't rename the variables.

**Why so strict:** the exact selectors, property lists, and timing reads are what
make them work. "Tidying" them is the fastest way to break a transition that was
fine.

This is the implementation layer. The decisions behind these values (whether to
animate at all, which easing, how fast) live in [../motion.md](../motion.md). Read
that first when unsure. It's where the reasoning is, like why a modal closes faster
than it opens and why a success check gets to run long.

## The eighteen

| Transition | When to use | Recipe |
| --- | --- | --- |
| **Card resize** | Tween a container's width or height when its layout state changes. | [01-card-resize.md](./01-card-resize.md) |
| **Number pop-in** | Re-enter each digit with a blurred slide when a number updates. | [02-number-pop-in.md](./02-number-pop-in.md) |
| **Notification badge** | Slide a small badge onto a trigger and pop the dot. | [03-notification-badge.md](./03-notification-badge.md) |
| **Text states swap** | Swap text in place with a blurred up-and-down transition. | [04-text-states-swap.md](./04-text-states-swap.md) |
| **Menu dropdown** | Open an origin-aware dropdown that grows from its trigger. | [05-menu-dropdown.md](./05-menu-dropdown.md) |
| **Modal open / close** | Scale-up modal dialog with a softer scale-down on close. | [06-modal.md](./06-modal.md) |
| **Panel reveal** | Slide a panel into a region with a cross-blur. | [07-panel-reveal.md](./07-panel-reveal.md) |
| **Page side-by-side** | Slide between two side-by-side pages (list to detail, step 1 to step 2). | [08-page-side-by-side.md](./08-page-side-by-side.md) |
| **Icon swap** | Cross-fade two icons in the same slot with blur and scale. | [09-icon-swap.md](./09-icon-swap.md) |
| **Success check** | Compose fade + rotate + Y-bob + path stroke-draw to celebrate a completed action. | [10-success-check.md](./10-success-check.md) |
| **Avatar group hover** | Distance-falloff lift on a row of items with a bouncy spring on return. | [11-avatar-group-hover.md](./11-avatar-group-hover.md) |
| **Error state shake** | Per-segment cubic-bezier shake with auto-reverting border + message. | [12-error-state-shake.md](./12-error-state-shake.md) |
| **Input clear with dissolve** | Fly-out + per-word streak when a text field is cleared. | [13-input-clear-dissolve.md](./13-input-clear-dissolve.md) |
| **Skeleton loader and reveal** | Pulse a placeholder, then cross-fade + cross-blur to the loaded content. | [14-skeleton-reveal.md](./14-skeleton-reveal.md) |
| **Shimmer text** | Sweep a highlight band across muted text on a loop (pure CSS). | [15-shimmer-text.md](./15-shimmer-text.md) |
| **Tabs sliding** | Slide the active pill between tabs in a segmented control. | [16-tabs-sliding.md](./16-tabs-sliding.md) |
| **Tooltip open/close** | Delayed fade+scale in, instant out (pure CSS). | [17-tooltip.md](./17-tooltip.md) |
| **Texts reveal** | Staggered blurred rise for stacked text lines, quiet fade out. | [18-texts-reveal.md](./18-texts-reveal.md) |

## Picking the right one

Match against the **visible UI element** first, then the verb:

- **Trigger plus a small dot floating on top** points to notification badge.
- **Trigger plus a surface that grows from it** points to dropdown (anchored, origin-aware) or modal (centered, no anchor).
- **Surface that slides into a region of the page** points to panel reveal.
- **Two screens, list to detail or step 1 to step 2** points to page side-by-side.
- **Element changes width or height** points to card resize.
- **Element's text content changes in place** points to text states swap.
- **Two icons in the same slot** points to icon swap.
- **A number updates** points to number pop-in.
- **Confirmation / success / "done" moment** (checkmark, payment processed, file uploaded) points to success check.
- **Hovering an item in a horizontal stack** (avatars, chips, segmented buttons, tag pills) points to avatar group hover.
- **Form validation error / "this is wrong" feedback** (invalid field, wrong PIN, duplicate name) points to error state shake.
- **Clearing a text field** (search box clear button, filter reset) points to input clear with dissolve.
- **Placeholder that loads then swaps to real content** (list row, card, profile header) points to skeleton loader and reveal.
- **In-progress / "thinking" text that should feel alive** (loading label, streaming status) points to shimmer text.
- **Small horizontal set of mutually-exclusive options with a moving highlight** (view switcher, segmented control, filter tabs) points to tabs sliding.
- **Hover/focus hint that appears over a trigger** (icon tooltip, info bubble) points to tooltip open / close.
- **Stacked headline plus supporting line entering with rhythm** (hero copy, empty state, onboarding step) points to texts reveal.

If two could fit, prefer the lower-overhead one: card resize over panel reveal,
dropdown over modal, success check over a full modal celebration, unless the design
clearly calls for the heavier surface. The success check is animation-only; if you
also need to swap a spinner for the check, pair it with **icon swap**. When nothing
matches cleanly, don't guess. Show the catalog and let the user pick.

## Motion tokens

The shared value vocabulary behind all eighteen. Match on **usage**, not on the raw
number: a 300ms modal close is still a `Quick` (150ms) close that should be brought
down. These are the values baked into [`_root.css`](./_root.css).

**Durations**

| Value | Name | Usage |
| --- | --- | --- |
| 40ms | Stagger | per-item stagger offset |
| 80ms | Micro | tooltip delay, shake segment, large stagger |
| 150ms | Quick | modal close, dropdown close, text swap, tooltip appear |
| 250ms | Fast | icon swap, dropdown open, modal open, tabs sliding, page slide |
| 350ms | Medium | panel close, toast close |
| 400ms | Slow | panel open, skeleton content reveal, input clear |
| 500ms | Very slow | emphasis moments, badge appear, text reveal, success check |

The 500ms tier looks like it violates the "UI under 300ms" rule in
[../motion.md](../motion.md). It doesn't. Every entry there is a rare or celebratory
moment: a badge arriving, a success check, a hero revealing once on load. Frequent,
functional motion stays under 300ms; the exception earns its extra time precisely
because the user sees it seldom.

**Easings**

| Value | Name | Usage |
| --- | --- | --- |
| cubic-bezier(0.22, 1, 0.36, 1) | Smooth ease out | modal / dropdown / panel open + close, page slide, resize, position change |
| ease-in-out | Ease in out | icon swap, text swap, text reveal, skeleton reveal |
| ease-out | Ease out | tooltip open / close |
| linear | Linear | shimmer, skeleton pulse, spinner |
| cubic-bezier(0.34, 1.36, 0.64, 1) | Bouncy overshoot | badge pop open |
| cubic-bezier(0.34, 3.85, 0.64, 1) | Strong bouncy overshoot | bouncy hover-out (avatar return) |

`cubic-bezier(0.22, 1, 0.36, 1)` is the house ease-out for this whole skill. It's
what the recipes use everywhere a strong, snappy exit curve is wanted. Pick one
strong ease-out and stay consistent across a project; mixing near-identical curves
is noise no one benefits from.

**Distances**

| Value | Name | Usage |
| --- | --- | --- |
| 4px | Micro | text swap |
| 6px | Small | error shake (small segment) |
| 8px | Base | badge diagonal reveal, page slide, error shake (large segment) |
| 12px | Medium | text reveal |
| 30px | Large | check badge appear |

**Blur**

| Value | Name | Usage |
| --- | --- | --- |
| 2px | Small | panel reveal, icon swap, text swap, skeleton reveal, number pop-in |
| 3px | Medium | page slide, text reveal |
| 8px | Large | success check open |

## Installing a transition

1. **Install the variables from [`_root.css`](./_root.css)** into the project's global
   stylesheet once, or just the per-snippet `:root` block from the recipe file if you
   only need one transition. If the universal block is already imported, do **not**
   duplicate it.
2. **Paste the chosen recipe's CSS verbatim.** Don't rewrite selectors, don't collapse
   to shorthand, don't strip `will-change`.
3. **Wire the documented HTML hooks**: the `t-*` class names and the state
   attributes/classes each recipe lists (`data-open`, `data-state`, `data-page`,
   `aria-selected`, `.is-open`, `.is-closing`, `.is-error`, `.is-shaking`,
   `.has-value`, `.is-clearing`, `.is-pulsing`, `.is-revealed`, `.is-shown`,
   `.is-hiding`).
4. **Keep the `@media (prefers-reduced-motion: reduce)` block.** Every recipe ships
   one; removing it fails accessibility audits.
5. **For transitions that need JS** (dropdown, modal, text swap, number pop-in, page
   slide, success check, avatar group hover, error state shake, input clear, skeleton
   reveal, tabs sliding, texts reveal), copy the small orchestration snippet and adapt
   selectors to the DOM. Keep the `getComputedStyle(...).getPropertyValue("--…")`
   reads so JS timing stays in sync with the CSS values. Shimmer text and tooltip are
   pure CSS, so no JS.

Keep the diff small: only touch the files needed to introduce the transition. Don't
rename existing variables, don't reformat unrelated CSS, don't add a motion library.

## The mistakes that break these recipes

- **Stripping the close-state cleanup** on dropdown/modal. Without the `setTimeout`
  that removes `.is-closing`, the next open jumps from the closing scale instead of
  the resting pre-open scale.
- **Forgetting the reflow** in text swap, number pop-in, success-check replay, and
  error shake. `void el.offsetWidth` between removing and re-adding the class is what
  guarantees the animation replays.
- **Animating the container instead of the inner pieces.** For the badge, animate the
  dot, not the trigger; for page slide, animate the page sections, not the wrapper.
- **Swapping enumerated properties for `transition: all`.** Every recipe lists exact
  properties on purpose so unrelated style changes don't ride in for free.
- **Hardcoding the success check's `stroke-dasharray`.** The snippet ships `20` as a
  placeholder. Replace it with `path.getTotalLength()` rounded up by 1 for your path,
  or the stroke pre-reveals or over-draws.
- **Setting the avatar hover `transition-timing-function` in CSS.** It has to be set
  inline in JS before the `--shift` / `--scale-active` writes, so the bouncy ease-out
  only applies on `mouseleave`.
- **Leaving the input-clear glow on `mix-blend-mode: multiply` in dark mode.** Flip to
  `screen`, bump `--glow-opacity` to about 0.85, and paint white gradients in JS.
- **Forgetting to write the tabs pill's first position without a transition.** On
  first paint and resize, set `transform` + `width` with `transition: none` (then
  reflow + restore), or the pill animates in from `translateX(0)` / `width: 0`.
