# Aesthetics: defaults that read as AI slop

These are the looks agents reach for when nobody decided. Default to the restrained version. Earn flashier choices only when the brand asks. Named tells below are auto-fail unless the user explicitly requested them.

## Named tells (kill on sight)

| Tell | What it looks like | Do instead |
| --- | --- | --- |
| Pill / eyebrow kicker | Capsule above the H1 with a tiny icon + short label | Cut it, or fold a real fact into the headline |
| Tiny uppercase tracked eyebrow on every section | `ABOUT` / `PROCESS` / `01 · Pricing` above each H2 | Different cadence; number only real sequences |
| Icon-in-colored-tile | Big icon centered in a soft rounded square as hero/feature chrome | Real product artifact, photo, or typography alone |
| Gradient text | Cyan→purple (or any multi-stop) wash on a headline word | Flat ink or flat accent; emphasize with weight/size |
| Gradient-square logo | Rounded square with blue→purple fill as the mark | Solid brand color or a real mark |
| Multi-hue aurora / candy pastel | Soft blended blobs or pastel wash background | Flat surface or one-hue low-contrast wash |
| Neon / colored glow / cut-off glow | Purple halo under a button; glow clipped by `overflow` | Neutral low-opacity directional shadow |
| Floating bob cards | Cards over the hero with looping float/parallax | Static composition; motion only on interaction |
| Kitchen-sink hero / default hero stack | Kicker + headline + subline + primary + secondary link, stacked center | Own the fold: change axis, drop secondary, lead with the artifact |
| Dual CTA by reflex | "Get started" + "Learn more" / "See the proof" every time | One primary; secondary only when it earns a job |
| Glowy pill CTA | Fully-rounded button with gradient fill + blurred glow | Solid fill, readable contrast, quiet shadow |
| Hover boop | Button `translateY` / scale-up on hover | Color/fill/underline change; no lift on buttons |
| Fake app/code window | Decorative macOS chrome or code screenshot that shows nothing real | Real UI from the product, or cut it |
| Hairline as depth | Light 1px border doing the job of elevation | Layered transparent `box-shadow` ([surfaces.md](./surfaces.md)) |
| Border + fat soft shadow | `1px` border plus wide blurry drop shadow on the same card/button | Pick one: edge or ≤8px-blur directional shadow |
| Over-rounded cards | 24–40px radius on cards/inputs as the default | ~12–16px cards; pills only for tags/buttons |
| Side-stripe accent | Thick `border-left` color bar on cards/alerts | Full border, tint, leading icon/number, or nothing |
| Identical feature card grid | Endless same-size icon + title + blurb cards | Vary composition; fewer cards; real artifacts |
| Hero-metric template | Giant number + tiny label + gradient accent as the whole story | Specific claim in context; product UI shows real data |
| Uniform Lucide diet | Same thin-stroke icon pack decorating every empty spot | Fewer icons; match label meaning |
| Nested cards | Card inside a card, or cards as the default layout | One surface; spacing and type do hierarchy |
| Default Inter/Roboto/Arial display | "Safe" system face as the designed brand voice | Distinctive face for the brief, or project tokens |
| Rotating free-font carousel | Fraunces, Space Grotesk, Sora, Syne, Figtree, Cormorant, etc. as identity | Own the type decision; do not cycle defaults across projects |
| Cream editorial body | Warm sand/beige page + terracotta + high-contrast serif reflex | Earn warmth via accent/type/imagery; body bg from the brief |
| Graph-paper / stripe / decorative grid bg | CSS grid overlay or diagonal stripes as decoration | Plain surface or real product structure |
| Botched glass | Heavy blur, illegible type on frost, or glow-as-material | Solid surface, or real translucency with contrast + fallback |
| Card hover-lift everywhere | Every card translates up and grows shadow on hover | Lift only interactive cards; subtle; gate with `(hover: hover)` |
| Stock collage hero | Generic people/handshakes/gradient mesh as the main visual | Real product, place, or artifact from the brief |
| Hard color seams | Adjacent sections with unrelated saturated fills and a dead cut | One palette; hand off tone; hard break only when deliberate |
| Loud saturated accent everywhere | Same vivid swatch on dots, buttons, headline words, labels | Tonal accents (lighter/darker/desaturated shifts) |
| Sketchy SVG illustrations | Doodle/feTurbulence "whimsy" scenes | Real assets or no illustration |
| Meta-irony copy | Naming a trope then winking at it | Make the specific claim |

## Layout and motion tells

- **Content visible by default.** Never gate text or controls on an entrance finishing (`opacity: 0` + scroll/JS reveal that can fail). If motion never runs, the page must still be fully readable.
- **Clear the cut.** Content must not be shaved by `clip-path`, notches, `overflow: hidden`, or fixed heights. Pad clear of the cut and verify at zoom.
- **Actually center.** Icons, numbers, and labels in pills/circles/badges are centered optically and mathematically; verify, do not assume.
- **No edge-flung default.** Do not maroon clusters on opposite rims with a dead gulf unless asymmetry is composed on purpose.
- **Directional shadow or none.** Avoid fat all-around halos by reflex.

## No emoji as UI

Don't use emoji as interface elements: not in badges, feature bullets, section icons, or buttons.

**Why:** emoji render differently per OS, cannot recolor with the type system, and read as placeholders. Fine in user-generated content. Not product chrome.

- Prefer the project's icon set (Lucide, Phosphor, Radix, etc.) at matching weight and size.
- Or use nothing: a small colored status dot + text beats an emoji pill.

## Icons must mean what they label

A padlock next to "Groceries" or a random square next to "Coffee" is worse than no icon. Pick icons that name the thing, or drop icon chips and keep the label.

- Do not wrap icons in decorative colored squares/circles by default.
- Match icon optical size to the set's designed box; do not arbitrarily upscale a 16px glyph.
- Icons beside labels are quieter than the text (muted color / lower emphasis).
- Align an icon to the first line of a label+description group (`items-start`), not the vertical center of the whole block, unless it is a single-line row.

## No gradient text

Headlines and body are a solid color. Emphasize with a flat accent, weight, or size — not a gradient wash.

## No gradient-filled logos or app icons by default

A rounded square with a blue-to-purple fill is the universal placeholder mark. Solid brand color, or a real mark.

## No decorative multi-hue gradients

Skip aurora blobs and rainbow washes. Flat, or a subtle **single-hue** wash at low contrast. Two or more hues blending is the fail.

## Shadows are for depth, not glow

Colored halos under buttons are decoration. Shadows stay neutral, low-opacity, and directional ([surfaces.md](./surfaces.md)).

## Quick gut check

- [ ] No named tell from the table above without an explicit user ask
- [ ] No emoji as icon, bullet, or badge marker
- [ ] No nested cards; cards earn their job
- [ ] No gradient on text; logo is solid or a real mark
- [ ] Background flat or single-hue wash; no hard accidental color seams
- [ ] Shadows neutral and directional, not colored glow or fat all-around bloom
- [ ] First viewport is not a kitchen-sink / default hero stack
- [ ] Content visible without animation; nothing sliced by a clip
