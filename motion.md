# Motion

Animation is the part of polish most likely to backfire. Get it right and the
interface feels responsive and alive. Add it on reflex and you've made everything
slower and noisier and called it design. This file is the deciding layer (whether,
when, which easing, how fast) plus the mechanics that keep motion smooth once you've
committed. The paste-ready implementations live in
[transitions/catalog.md](./transitions/catalog.md).

## The decision

Before you write a line of animation, walk these in order.

### 1. Should this animate at all?

The only question that matters first is how often the user sees it.

| Frequency | Decision |
| --- | --- |
| 100+ times/day (keyboard shortcuts, command palette toggle) | No animation. Ever. |
| Tens of times/day (hover effects, list navigation) | Cut it or shrink it hard |
| Occasional (modals, drawers, toasts) | Standard animation |
| Rare / first-time (onboarding, success moments, celebrations) | Room for delight |

**Why:** a command palette opened a hundred times a day should open instant. An
animation there reads as lag on every single open. The same rule explains why the
catalog's 500ms tier is fine: a success check or a badge landing is rare, so it can
afford to take its time. Frequent motion earns less time, not more.

### 2. What's the reason?

Every animation needs a one-sentence answer to "why does this move?" The good ones:

- **Spatial consistency.** A toast enters and exits the same edge, so swipe-to-dismiss feels obvious.
- **State change.** A control morphs to show it flipped.
- **Explanation.** A sequence showing how a feature actually works.
- **Feedback.** A button scales on press, confirming the tap landed.
- **Stopping a jarring jump.** Something appearing or vanishing with no transition feels like a glitch.

If the only answer is "it looks cool" and the user sees it often, don't.

### 3. Which easing?

```
Entering or exiting?         -> ease-out          (starts fast, feels instant)
Moving / morphing on screen? -> ease-in-out       (natural accel + decel)
Hover or color change?       -> ease
Constant motion (marquee)?   -> linear
Otherwise                    -> ease-out
```

**Never use `ease-in` for UI.** It starts slow, so it stalls at the exact moment the
user is watching hardest. An `ease-in` dropdown at 300ms feels slower than an
`ease-out` one at the same 300ms.

The built-in keywords are too weak to feel intentional. Pick one strong custom
ease-out as the house curve and stay consistent across the project:

```css
--ease-out:    cubic-bezier(0.22, 1, 0.36, 1);   /* snappy UI exits */
--ease-in-out: cubic-bezier(0.77, 0, 0.175, 1);  /* on-screen movement */
--ease-drawer: cubic-bezier(0.32, 0.72, 0, 1);   /* iOS-like drawer pull */
```

### 4. How fast?

| Element | Duration |
| --- | --- |
| Button press feedback | 100-160ms |
| Tooltips, small popovers | 125-200ms |
| Dropdowns, selects | 150-250ms |
| Modals, drawers | 200-500ms |
| Marketing / explanatory | can be longer |

**Functional UI stays under 300ms.** A 180ms dropdown beats a 400ms one. And speed
is partly perception: a faster-spinning spinner makes a load feel quicker even when
the real time is identical, and `ease-out` at 200ms feels faster than `ease-in` at
200ms because the eye sees movement right away.

### 5. Match the character to the product

The framework above is universal; the values are not. A playful consumer app can run
slightly longer and carry a little spring; a banking dashboard or a pro tool stays
crisp, short, and bounce-free. Pick a motion character per product and hold it, the
same way you hold a type scale. Reusing the exact same curves and durations on every
project is how everything you make ends up feeling identical.

### 6. Enter and exit aren't symmetric

Exits should be quicker and quieter than enters.

**Why:** by the time something leaves, the user's attention is already on the next
thing, so motion shouldn't fight for it on the way out. Rule of thumb: exit in about
half the enter duration (enter 300ms, exit 150ms). The extreme case of the same idea
is that motion is slow where the user is deciding (a 2s hold-to-delete) and snappy
where the system is responding (a 200ms release).

## Interruptible by default: transitions over keyframes

Users change their mind mid-interaction. A CSS transition interpolates toward
whatever the latest target is, so it retargets cleanly when the state flips. A
keyframe animation runs a fixed timeline and restarts from zero when re-triggered,
which looks broken on anything that can fire twice quickly.

| | CSS transition | Keyframe animation |
| --- | --- | --- |
| Behavior | interpolates toward latest state | fixed timeline |
| Interruptible | yes, retargets mid-flight | no, restarts |
| Use for | toggles, hover, open/close, anything re-triggerable | one-shot sequences (entrances, loaders) |

```css
/* Good: click again mid-open and it reverses smoothly */
.drawer       { transform: translateX(-100%); transition: transform 200ms var(--ease-out); }
.drawer.open  { transform: translateX(0); }
```

Save keyframes for sequences that run once and don't get interrupted. When you need
JS-driven motion with CSS performance, the Web Animations API gives you both:
hardware-accelerated, interruptible, no library.

```js
el.animate(
  [{ clipPath: "inset(0 0 100% 0)" }, { clipPath: "inset(0 0 0 0)" }],
  { duration: 1000, fill: "forwards", easing: "cubic-bezier(0.77, 0, 0.175, 1)" }
);
```

## Entrances: split and stagger

Don't animate one big container. Break the content into its real pieces (title,
description, actions) and stagger them about 100ms apart. Combine `opacity`,
`translateY`, and a small `blur`. For titles, splitting into individual words with
about 80ms stagger reads beautifully. Keep the offsets short (30-100ms), because
long ones make the page feel slow, and since stagger is decorative, never block
interaction while it plays.

```css
.stagger-item {
  opacity: 0;
  transform: translateY(12px);
  filter: blur(4px);
  animation: rise 400ms var(--ease-out) forwards;
}
.stagger-item:nth-child(1) { animation-delay: 0ms; }
.stagger-item:nth-child(2) { animation-delay: 100ms; }
.stagger-item:nth-child(3) { animation-delay: 200ms; }

@keyframes rise {
  to { opacity: 1; transform: translateY(0); filter: blur(0); }
}
```

Same idea in `motion` (Framer Motion) via `staggerChildren`:

```tsx
<motion.div
  initial="hidden"
  animate="visible"
  variants={{ visible: { transition: { staggerChildren: 0.1 } } }}
>
  {/* each child: hidden -> { opacity:0, y:12, filter:"blur(4px)" }, visible -> reset */}
</motion.div>
```

## Animate entry with `@starting-style`

The modern way to animate an element appearing, with no JavaScript and no "mounted"
flag. Declare the resting state, then the state to start from inside `@starting-style`:

```css
.toast {
  opacity: 1;
  transform: translateY(0);
  transition: opacity 400ms var(--ease-out), transform 400ms var(--ease-out);

  @starting-style {
    opacity: 0;
    transform: translateY(100%);
  }
}
```

This replaces the old React pattern of a `useEffect` that sets `mounted: true` after
first render. Use `@starting-style` where browser support allows, and fall back to the
`data-mounted` attribute toggle where it doesn't.

## Exits: keep them quiet

Use a small fixed `translateY` (about `-12px`), not the element's full height, and
run it shorter than the enter. Keep a little directional movement so it reads as
going somewhere.

**Why:** an element that just `display: none`s out of existence feels like a bug,
but a dramatic exit steals attention the user has already moved on from. The full
slide-out is only for when spatial context matters, like a card returning to its
list or a drawer closing.

```css
.item-exit {                         /* good: quiet, directional, fast */
  opacity: 0;
  transform: translateY(-12px);
  transition: opacity 150ms ease-in, transform 150ms ease-in;
}
```

## Never animate from `scale(0)`

Nothing in the real world appears out of nothing. An element growing from `scale(0)`
looks like it materialized from the void. Start from `scale(0.95)` (or higher) with
opacity. Even a barely-visible starting size gives the entrance a believable origin.

```css
.entering { transform: scale(0.95); opacity: 0; }   /* not scale(0) */
```

## Scale on press

A small scale-down on press is tactile feedback. It makes the button feel like it
physically heard the tap. Use `scale(0.96)` as the default; `scale(0.97)` is just as
fine on larger buttons. **Never below `0.95`**, because smaller than that looks
exaggerated. Use a transition (not a keyframe) so releasing mid-press returns
smoothly, and give yourself a way to opt out where the motion would distract.

```tsx
const tapScale = "active:not-disabled:scale-[0.96]";

function Button({ static: isStatic, className, children, ...props }) {
  return (
    <button
      className={cn("transition-transform duration-150 ease-out", !isStatic && tapScale, className)}
      {...props}
    >
      {children}
    </button>
  );
}

<Button>Click me</Button>      {/* scales */}
<Button static>Submit</Button> {/* opted out */}
```

## Origin-aware popovers

A popover should grow out of the trigger that opened it, not from its own center.
The default `transform-origin: center` is wrong for almost every anchored surface.
Wire it to the trigger. Component libraries hand you this as a CSS variable:

```css
.popover { transform-origin: var(--radix-popover-content-transform-origin); }
/* or, Base UI: */
.popover { transform-origin: var(--transform-origin); }
```

**Modals are the exception.** They're anchored to nothing, so they keep
`transform-origin: center` and appear centered in the viewport.

## Tooltips: delay once, then instant

A tooltip should wait before appearing so a passing cursor doesn't trigger it. But
once one tooltip in a group is already open, hovering to an adjacent trigger should
open the next one instantly, with no delay and no animation.

**Why:** the delay exists to prevent accidental activation. Once the user is clearly
reading tooltips, re-paying that delay on every neighbor makes the whole toolbar feel
sluggish. Skipping it once the first is open feels faster without losing the guard.

```css
.tooltip {
  transition: transform 125ms ease-out, opacity 125ms ease-out;
  transform-origin: var(--transform-origin);
}
.tooltip[data-instant] {
  transition-duration: 0ms;   /* set data-instant on neighbors while one is open */
}
```

## Contextual icon swaps

When an icon changes on hover or state (play to pause, like to liked), don't toggle
visibility. Cross-fade with `opacity`, `scale`, and `blur`. Use **exactly** these
values, every time:

- `scale`: `0.25` to `1` (never `0.5` or `0.6`)
- `opacity`: `0` to `1`
- `filter`: `blur(4px)` to `blur(0px)`
- transition: `{ type: "spring", duration: 0.3, bounce: 0 }`, where **bounce is always `0`**

If the project already has `motion` / `framer-motion`, use `AnimatePresence` with
those values. If it doesn't, **don't add a dependency just for this.** Keep both
icons in the DOM (one absolutely positioned over the other) and cross-fade with CSS
using `cubic-bezier(0.2, 0, 0, 1)`. Because neither icon unmounts, both the enter and
the exit animate.

Animate icons that show up contextually: hover actions, state toggles, loading and
success indicators. Leave static nav icons, decorative icons, and always-on icons
alone.

## Skip the entrance on first load

Elements already in their resting state on page load shouldn't animate in, only on
later state changes. In `motion`, set `initial={false}` on `AnimatePresence`. This is
right for icon swaps, toggles, tabs, and segmented controls.

It's **wrong** for anything whose entrance is the point, like a staggered hero or a
first-time loading state, because `initial={false}` skips that entrance entirely.
Always check a full page refresh after you apply it.

## Springs

Springs simulate physics, so they feel more natural than fixed-duration curves for
anything that should feel alive or be interruptible. They settle on parameters, not
a clock, and they keep their velocity when interrupted, where a keyframe restarts
from zero. That's what makes them right for gestures the user might reverse
mid-motion.

```js
// duration + bounce: easiest to reason about
{ type: "spring", duration: 0.5, bounce: 0.2 }

// physical parameters: more control
{ type: "spring", mass: 1, stiffness: 100, damping: 10 }
```

Keep `bounce` subtle (0.1-0.3) and save it for drag-to-dismiss and playful moments;
most UI wants none. For decorative mouse-tracking, run the value through a spring
(`useSpring`) instead of binding it straight to the pointer, because raw binding has
no momentum and feels mechanical. And decoration like that only earns its place when
it isn't competing with a function: a live graph in a finance app is better with no
animation at all.

## clip-path: reveal without extra DOM

`clip-path: inset(top right bottom left)` defines a rectangular window, and each
value eats in from that edge. It's one of the most underused animation tools in CSS.

```css
.hidden  { clip-path: inset(0 100% 0 0); }   /* fully clipped from the right */
.visible { clip-path: inset(0 0 0 0); }      /* fully shown */
```

What it unlocks:

- **Scroll reveals.** Animate `inset(0 0 100% 0)` to `inset(0 0 0 0)` as the element enters the viewport.
- **Before/after sliders.** Overlay two images and drive the top one's right inset from the drag position. No extra elements, fully GPU-composited.
- **Hold-to-delete.** Transition a colored overlay to full over 2s linear on `:active`, then snap back in 200ms on release.
- **Tab color transitions** that no amount of timing individual color properties can match. Duplicate the tab list styled "active", clip the copy to just the active tab, and animate the clip.

## Gestures and drag

- **Dismiss on velocity, not just distance.** `velocity = |dragDistance| / elapsedTime`; past about 0.11, dismiss no matter how far the drag went. A quick flick should be enough.
- **Damp past the boundary.** Drag beyond a natural edge and it should move less the further it goes, not slam into an invisible wall. Real things slow before they stop.
- **Capture the pointer** once a drag starts, so it keeps going even when the pointer leaves the element's bounds.
- **Ignore extra touch points** after the first. Switch fingers mid-drag without this and the element jumps to the new position.

## Mask a rough crossfade with blur

When a crossfade between two states looks off no matter the easing or duration, add a
brief `filter: blur(2px)` during the transition.

**Why it works:** without it the eye catches two distinct objects overlapping; the
blur blends them into one apparent transformation. Keep blur under 20px, since heavy
blur is expensive, Safari especially.

## Performance

- **Animate only `transform` and `opacity`** for movement. They skip layout and paint
  and run on the GPU. Animating `width`, `height`, `margin`, or `padding` fires the
  whole pipeline and drops frames.
- **Prefer percentage transforms.** `translateY(100%)` moves an element by its own
  height regardless of its actual size, so it adapts to content and is harder to get
  wrong than hardcoded pixels.
- **`scale()` scales children too** (unlike width/height). Scale a button on press and
  its text and icons scale with it. That's what you want.
- **CSS beats JS under load.** CSS animations run off the main thread, so they stay
  smooth while the browser is busy loading or scripting; `requestAnimationFrame`
  animations drop frames in those windows. Use CSS for predetermined motion, JS for
  dynamic or interruptible motion.
- **`motion`'s `x` / `y` / `scale` shorthands are not hardware-accelerated.** They run
  on the main thread. For motion that has to stay smooth under load, animate the full
  `transform` string instead:

  ```tsx
  <motion.div animate={{ x: 100 }} />                          // can drop frames under load
  <motion.div animate={{ transform: "translateX(100px)" }} />  // GPU-composited
  ```

- **Don't write to an inherited CSS variable on a hot path.** Changing a custom
  property on a parent recalculates styles for every child. During a drag, write
  `transform` straight onto the moving element instead of updating a shared `--var`.
- **Never `transition: all`.** Name exact properties (`transition-property: scale,
  opacity`) so unrelated changes like color or padding don't ride along. Tailwind's
  bare `transition` maps to `all`; `transition-transform` is safe (it covers
  `transform, translate, scale, rotate`), and for other combos use the bracket syntax
  `transition-[scale,opacity,filter]`.
- **`will-change` sparingly.** It pre-promotes an element to its own GPU layer,
  killing the one-frame stutter when motion starts. Worth it only for `transform`,
  `opacity`, `filter`, and `clip-path`, and only when you actually see first-frame
  jank (Safari benefits most). Never `will-change: all`, because every layer costs
  memory.

## Accessibility

**Honor `prefers-reduced-motion`.** Reduced motion means fewer and gentler
animations, not zero. Keep the opacity and color transitions that aid comprehension,
and drop the movement and position changes.

```css
@media (prefers-reduced-motion: reduce) {
  .element { animation: fade 0.2s ease; }   /* no transform-based motion */
}
```

```tsx
const reduce = useReducedMotion();
const closedX = reduce ? 0 : "-100%";
```

**Gate hover effects behind capability.** Touch devices fire hover on tap, so a hover
animation triggers on every touch. Wrap it so it only applies to real pointers:

```css
@media (hover: hover) and (pointer: fine) {
  .element:hover { transform: scale(1.05); }
}
```

## Debugging motion

- **Watch it in slow motion.** Multiply the duration 2-5x (or use the DevTools
  animation inspector) and look for two states visibly overlapping in a crossfade,
  easing that starts or stops abruptly, a wrong transform-origin, or properties
  drifting out of sync.
- **Step frame by frame** in the DevTools Animations panel to catch timing mismatches
  between coordinated properties that are invisible at full speed.
- **Look again the next day.** Imperfections you tuned past with tired eyes are
  obvious with fresh ones.
- **Test gestures on real hardware.** Drawers and swipes behave differently under a
  real finger than a mouse, so connect a physical device, not just a simulator.
