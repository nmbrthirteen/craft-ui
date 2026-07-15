# Typography

Hierarchy and rendering details that make text read as deliberate instead of default.

## Hierarchy

- Body on mobile is at least 16px. Do not use extra-small sizes for body or UI copy on
  small screens; tighten at larger breakpoints if needed.
- Prefer medium / semibold for headings over heavy bold. At most two weights per view:
  one for emphasis, one for body.
- Large display type: tighten tracking slightly before adding weight. Floor around
  `-0.04em`; tighter and letters touch. Do not use tight tracking on small labels.
- Constrain measure: body roughly 45–75ch; put max-width on the text element itself
  when a headline wraps badly.
- Headings: `text-wrap: balance`. Body / short UI copy: `text-wrap: pretty`.
- Avoid uppercase eyebrows unless the type is intentionally mono/wide-tracked.
- Pair on a contrast axis (serif + sans, geometric + humanist) or one family in
  multiple weights. Do not pair two near-identical sans by default.
- Do not reach for Inter / Roboto / Arial as the "designed" display voice unless the
  project already owns them. Distinctive type is a primary personality axis
  ([start-here.md](./start-here.md)).

## Choosing and loading type

- Prefer the project's existing font tokens. Only introduce a new pairing when the
  brief or brand kit calls for it.
- One display + one body is enough. A mono for code/data is optional, not a third
  brand voice.
- Load with `font-display: swap` (or the project's equivalent). Subset when possible.
- Register faces in the project's theme (`@theme`, CSS variables, or design tokens),
  not as one-off classes scattered through components.
- Enable useful OpenType features when the face supports them (tabular nums via
  `tabular-nums` / `tnum`; stylistic sets only when intentional).
- Cap display size: if a clamp max sits above ~6rem / 96px without a deliberate
  poster moment, you are shouting, not designing.
- Build a short scale and stick to it (e.g. sm / base / lg / xl / 2xl / 4xl). Do not
  invent a new size per section.

## Text wrapping

**`text-wrap: balance`** spreads a short block evenly across its lines so a heading
doesn't strand one lonely word on the last line. The balancing pass is expensive, so
browsers cap it: it only kicks in on blocks of about 6 lines or fewer (Chromium) or
about 10 (Firefox). Put it on headings and titles.

```css
h1, h2, h3 { text-wrap: balance; }   /* Tailwind: text-balance */
```

**`text-wrap: pretty`** doesn't try to even out line lengths. It just stops a single
word dangling on the final line, and it works at any length. This is the **default
for short-to-medium body text**: paragraphs, descriptions, captions, list items,
card copy.

```css
p, li, figcaption, blockquote { text-wrap: pretty; }   /* Tailwind: text-pretty */
```

For genuinely long text (10+ lines) or code blocks, use neither.

**Why:** the balancing and orphan work buys you nothing once the block is long, and
you skip the layout cost.

| Scenario | Use |
| --- | --- |
| Headings, titles | `text-wrap: balance` |
| Paragraphs, descriptions, captions, UI text | `text-wrap: pretty` |
| Long body text (10+ lines), code, preformatted | neither, leave default |

## Font smoothing on macOS

On macOS, text renders heavier than it was drawn. Apply antialiased smoothing **once
at the root** so everything renders crisp at the intended weight.

```css
html {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
```

```tsx
<html className="antialiased">
```

**Why root, not per-element:** apply it piecemeal and you get headings at one weight
and body at another on the same page. Other platforms ignore these properties, so
it's safe to set globally.

## Tabular numbers

Any number that updates in place, such as counters, prices, timers, table columns,
scoreboards, and animated transitions, should use tabular figures so every digit is
the same width.

```tsx
<span className="tabular-nums">{count}</span>   /* font-variant-numeric: tabular-nums */
```

**Why:** proportional digits are different widths, so the text reflows a couple
pixels every time a `1` becomes a `4` and the whole element twitches. Equal-width
digits hold the box still.

| Use tabular-nums | Skip it |
| --- | --- |
| Counters, timers, animated numbers | Static display numbers |
| Prices that update | Decorative large numerals |
| Table number columns | Phone numbers, zip codes |
| Scoreboards, dashboards | Version strings (v2.1.0) |

**Caveat:** some fonts (Inter, for one) reshape the `1` under this property, making
it wider and centered. That's expected and usually what you want for alignment, but
eyeball it in your actual typeface before shipping.

## Overflow and truncation

- Prefer ellipsis truncation on single-line titles in dense UI (tables, sidebars,
  metric cards) over unpredictable wraps that blow row height.
- When truncating, provide the full string via native `title` or an accessible
  tooltip on hover/focus when the value matters.
- Do not shrink font size as the primary fix for overflow; fix measure, truncation,
  or layout first.
- Buttons and chips: text should not spill; keep padding and min-width so labels
  stay readable when translated or when counts appear.
