# Aesthetics: defaults that read as AI slop

These are the looks agents reach for when nobody decided. Default to the restrained version. Earn flashier choices only when the brand asks. Named tells below are auto-fail unless the user explicitly requested them.

## Named tells (kill on sight)

| Tell | What it looks like | Do instead |
| --- | --- | --- |
| Pill / eyebrow kicker | Capsule above the H1 with a tiny icon + short label | Cut it, or fold a real fact into the headline |
| Icon-in-colored-tile | Big Lucide icon centered in a soft rounded square as hero/feature chrome | Real product artifact, photo, or typography alone |
| Gradient text | Cyan→purple (or any multi-stop) wash on a headline word | Flat ink or flat accent |
| Gradient-square logo | Rounded square with blue→purple fill as the mark | Solid brand color or a real mark |
| Multi-hue aurora | Soft blended blobs / candy pastel background | Flat surface or one-hue low-contrast wash |
| Neon / colored glow | Purple button casting a purple halo; glow clipped by `overflow` | Neutral low-opacity layered shadow |
| Floating bob cards | Cards over the hero with looping float/parallax | Static composition; motion only on interaction |
| Kitchen-sink hero | Kicker + long headline + paragraph + dual CTAs + three feature cards in the first viewport | Brand, one headline, one short line, one CTA group, one dominant visual |
| Glowy pill CTA | Fully-rounded button with gradient fill + blurred glow | Solid fill, readable contrast, quiet shadow |
| Fake app/code window | Decorative macOS chrome or code screenshot that shows nothing real | Real UI from the product, or cut it |
| Hairline as depth | Light 1px border doing the job of elevation | Layered transparent `box-shadow` ([surfaces.md](./surfaces.md)) |
| Uniform Lucide diet | Same thin-stroke icon pack decorating every empty spot | Fewer icons; match label meaning; vary weight only if the brand set does |

## No emoji as UI

Don't use emoji as interface elements: not in badges, feature bullets, section icons, or buttons.

**Why:** emoji render differently per OS, cannot recolor with the type system, and read as placeholders. Fine in user-generated content. Not product chrome.

- Prefer the project's icon set (Lucide, Phosphor, Radix, etc.) at matching weight and size.
- Or use nothing: a small colored status dot + text beats an emoji pill.

## Icons must mean what they label

A padlock next to "Groceries" or a random square next to "Coffee" is worse than no icon. Pick icons that name the thing, or drop icon chips and keep the label.

## No gradient text

Headlines and body are a solid color. Emphasize with a flat accent, not a gradient wash.

## No gradient-filled logos or app icons by default

A rounded square with a blue-to-purple fill is the universal placeholder mark. Solid brand color, or a real mark.

## No decorative multi-hue gradients

Skip aurora blobs and rainbow washes. Flat, or a subtle **single-hue** wash at low contrast. Two or more hues blending is the fail.

## Shadows are for depth, not glow

Colored halos under buttons are decoration. Shadows stay neutral and low-opacity ([surfaces.md](./surfaces.md)).

## Quick gut check

- [ ] No named tell from the table above without an explicit user ask
- [ ] No emoji as icon, bullet, or badge marker
- [ ] No gradient on text; logo is solid or a real mark
- [ ] Background flat or single-hue wash
- [ ] Shadows neutral, not colored glow
- [ ] First viewport is not a kitchen-sink hero
