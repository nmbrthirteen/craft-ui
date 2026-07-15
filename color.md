# Color and contrast

Color is where polish and accessibility are the same conversation. A muted gray that
looks tasteful in the mockup can be unreadable for a chunk of your users, and an
accent that fails contrast under white text is both an a11y bug and a sloppy look.
The contrast targets below are correctness, not taste. Hit them, then make the
palette yours.

## Text contrast (follow always)

WCAG AA, the baseline to meet:

- **Normal text: at least 4.5:1** against its background.
- **Large text: at least 3:1.** Large means 24px or larger, or 18.66px (14pt) bold or larger.

AAA is stricter (7:1 normal, 4.5:1 large) and worth it for long-form reading, but AA
is the floor for shipping.

**Why:** below 4.5:1, low-vision users and anyone on a dim or sun-glared screen lose
the text. This is the most common accessibility failure in generated UI, and it
usually hides in the prettiest, lightest grays.

The traps to check first:

- **Muted and placeholder text.** A light-gray placeholder like `$0.00` or "Coffee,
  groceries, rent..." is the usual offender. Placeholders still need 4.5:1, and they
  are not a substitute for a label.
- **Gray text on a colored background.** Washes out and often fails contrast. Prefer
  a darker shade of the background's own hue, or ink slightly tinted toward that hue.
- **White text on a mid-tone accent button.** Plenty of mid-saturation greens, teals,
  and oranges fail 4.5:1 with white text. Darken the accent for the button, or switch
  the label to a dark ink. Check it, don't eyeball it.
- **Text over images or gradients.** Contrast has to hold over the lightest part of
  the background, so add a scrim if it doesn't.

## Non-text contrast (follow always)

WCAG AA also requires **at least 3:1** for things that aren't text but carry meaning:

- Input borders, the edges of a control against its surround.
- Icons and the meaningful parts of a glyph.
- Focus indicators (see below).
- Chart bars, lines, and legend swatches.

A 1px hairline at very low opacity can be invisible to many users. If a border
communicates "this is a field," it has to be seen.

## Don't encode meaning in color alone (follow always)

Roughly 1 in 12 men have some red-green color blindness. If red means error and green
means success and that's the only difference, those users get nothing.

- Pair color with a second signal: an icon, a label, a shape, a position.
- A red input border gets an error message and ideally an icon. A green "safe to
  spend" figure says "safe to spend" in words too.

**Test:** view the screen in grayscale. If you can no longer tell states apart, the
color was doing all the work.

## Focus has to be visible (follow always)

Every interactive element needs a visible `:focus-visible` state that meets 3:1
against what's around it. This is also where the default browser blue often clashes:
you don't have to keep it, but whatever replaces it has to be clearly visible.

```css
:focus-visible {
  outline: 2px solid var(--focus-ring);
  outline-offset: 2px;
}
```

**Why:** keyboard users navigate by the focus ring. Removing it (`outline: none` with
nothing in its place) strands them. A brand-colored ring is fine as long as it passes
3:1 and doesn't fight the component it sits on.

## Where taste comes in

Once contrast is satisfied, the palette is yours and is a primary way products differ
(see the range section in [SKILL.md](./SKILL.md)):

- Lead with one accent, not three. A single confident color reads more designed than
  a rainbow.
- Build neutrals from a slight hue (warm or cool grays) rather than pure `#000`/`#888`
  steps, so the surface has a temperature.
- Reserve saturated color for action and meaning; let large surfaces stay calm.

## Quick gut check

- [ ] Body text meets 4.5:1; large text and headings meet 3:1
- [ ] Placeholder and muted text still meet 4.5:1 (and aren't the only label)
- [ ] Button label passes contrast on its own fill (white-on-accent often fails)
- [ ] Input borders, icons, and focus rings meet 3:1
- [ ] No state relies on color alone; it survives a grayscale check
- [ ] Every interactive element has a visible focus-visible style
