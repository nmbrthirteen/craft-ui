# Craft UI

The AI ships working code. That part is free now.

Craft UI is the layer after. The small calls that decide whether a screen feels
considered or generated: the radius that lines up with the one inside it, the dropdown
that grows from the button you pressed, the number that holds the layout still when it
ticks. Invisible on their own. Stacked, they are why a product feels trustworthy
without anyone being able to say why.

An agent skill for craft-level UI work, by [Nika Siradze](https://nikusha.com).

## What it does

Guarantees a quality floor. It does not hand you a look. If everything you build with
it comes out the same, you copied the defaults instead of deciding. It covers:

- **From brief to UI** ([start-here.md](./start-here.md)). Anchor in the product's
  world, plan, critique against the default looks, then build.
- **Surfaces** ([surfaces.md](./surfaces.md)). Concentric radius, optical alignment,
  shadows vs borders, shadow clipping, image outlines, hit areas.
- **Typography** ([typography.md](./typography.md)). `text-wrap`, font smoothing,
  tabular numbers.
- **Motion** ([motion.md](./motion.md)). The animation decision, easing and duration,
  enter/exit and stagger, scale-on-press, icon swaps, springs, gestures, performance.
- **Color** ([color.md](./color.md)). WCAG contrast, non-text contrast, never color
  alone, visible focus.
- **Aesthetics** ([aesthetics.md](./aesthetics.md)). The tells that read as AI slop:
  emoji-as-icons, gradient text, gradient logos, multi-hue blobs, neon glows.
- **Copy** ([copy.md](./copy.md)). Hero anatomy, the kicker rule, CTA, page flow. No em
  dashes, no negation triads, no hype, sentence case.
- **Transitions** ([transitions/](./transitions/)). Eighteen paste-ready CSS
  transitions on shared motion tokens, with a [`_root.css`](./transitions/_root.css).

Start with [SKILL.md](./SKILL.md). It routes to the rest.

## Install

Clone into your agent skills directory so the skill is discoverable:

```bash
git clone git@github.com:nmbrthirteen/craft-ui.git ~/.agents/skills/craft-ui
```

If your setup loads skills from `~/.claude/skills`, symlink it there:

```bash
ln -s ~/.agents/skills/craft-ui ~/.claude/skills/craft-ui
```

Then invoke it as `/craft-ui`, or let it trigger on UI and polish work.

## License

MIT. See [LICENSE](./LICENSE).
