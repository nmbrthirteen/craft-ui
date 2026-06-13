# Aesthetics: defaults that read as AI slop

There's a specific look that screams "a model generated this": emoji standing in for
icons, gradient text, a gradient-filled app icon, neon glows under buttons. None of
it is illegal, but it's what gets reached for when nobody made a real decision, and
people now read it as unfinished. Default to the restrained version. Earn the
flashier choice only when the brand genuinely calls for it.

## No emoji as UI

Don't use emoji as interface elements: not in badges, not as feature-list bullets,
not as section icons, not in buttons.

**Why:** emoji render differently on every OS, can't be recolored or sized to match
your type, and instantly read as a placeholder nobody replaced. A lightning-bolt
emoji in a "Cold start under 40ms" pill is the giveaway.

- **Use a real icon set** (Lucide, Phosphor, Radix icons, or the project's existing
  set) so weight, size, and color match the surrounding type.
- **Or use nothing.** A status pill with a small colored dot and text reads cleaner
  than the same pill with an emoji.

Emoji are fine in user-generated content (a chat message, a reaction). They are not
fine as product chrome.

## Icons must mean what they label

If an icon sits next to a label, it has to represent that label. A padlock next to
"Groceries", a generic card next to "Train pass", a vague square next to "Coffee":
those read as whatever icon was within reach, and a wrong icon is worse than none.

**Why:** a mismatched icon is a placeholder that shipped. The reader notices the lock
on the grocery row and trusts the whole interface a little less.

- **Pick icons that name the thing**: a cart for groceries, a cup for coffee, a train
  for transit. If the set doesn't have a close match, use a neutral category icon
  consistently, not a random near-miss per row.
- **Or drop the icon chips entirely.** A clean label plus the amount reads better than
  a row of decorative, meaningless glyphs.

## No gradient text

Headlines and body text are a solid color. If you want to emphasize one word, set it
in the accent color, flat.

**Why:** a cyan-to-purple gradient across a headline word is the single most common
generated-landing-page move. It also tends to fail contrast checks at the light end
and looks muddy at small sizes.

## No gradient-filled logos or app icons by default

A rounded square filled with a blue-to-purple gradient is the placeholder logo every
generator produces. Use a solid brand color, or a real mark if one exists.

## No decorative multi-hue gradients

Skip the "aurora" blobs and rainbow background washes used to make an empty page look
designed.

**Why:** they date instantly and fight whatever real content lands on top. A flat
surface, or at most a **subtle single-hue wash** (one color fading to transparent, low
contrast), is the safe default. A subtle radial or linear wash in one brand hue is
fine. Two or more hues blending is the thing to avoid.

## Shadows are for depth, not glow

A colored glow under a button (a purple button casting a purple halo) is decoration,
not elevation. Shadows should be neutral and low-opacity, the way real light behaves.
See [surfaces.md](./surfaces.md) for the layered shadow recipe.

**Why:** neon glows have no real-world referent, so they read as a sticker effect.
Depth comes from a soft dark shadow, not a saturated bloom.

## Quick gut check

Before shipping a screen, scan for these. Each one found is a place to make a real
decision instead of a default:

- [ ] No emoji used as an icon, bullet, or badge marker
- [ ] No gradient applied to text
- [ ] Logo/app icon is a solid fill or a real mark, not a generic gradient square
- [ ] Background is flat or a single-hue wash, not a multi-color blob
- [ ] Button and card shadows are neutral, not a colored glow
