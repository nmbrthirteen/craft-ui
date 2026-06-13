# Typography

Three rendering details that cost almost nothing and make text read as deliberate
instead of default.

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
