# Craft UI

A Claude Code / agent skill for craft-level UI work. It is the layer you add after
the AI ships code that merely works: the small details and decisions that make an
interface feel considered instead of generated.

By [Nika Siradze](https://nikusha.com).

## What it does

Craft UI guarantees a quality floor and gives you a process for using it without
making every project look the same. It covers:

- **From brief to UI** ([start-here.md](./start-here.md)) — anchor in the product's
  world, plan, critique against the default looks, then build.
- **Surfaces** ([surfaces.md](./surfaces.md)) — concentric radius, optical alignment,
  shadows vs borders, shadow clipping, image outlines, hit areas.
- **Typography** ([typography.md](./typography.md)) — `text-wrap`, font smoothing,
  tabular numbers.
- **Motion** ([motion.md](./motion.md)) — the animation decision, easing and duration,
  enter/exit and stagger, scale-on-press, icon swaps, springs, gestures, performance,
  accessibility, debugging.
- **Color** ([color.md](./color.md)) — WCAG contrast, non-text contrast, never color
  alone, visible focus.
- **Aesthetics** ([aesthetics.md](./aesthetics.md)) — the visual defaults that read as
  AI slop: emoji-as-icons, gradient text, gradient logos, multi-hue blobs, neon glows,
  mismatched icons.
- **Copy** ([copy.md](./copy.md)) — messaging structure (hero anatomy, the kicker rule,
  CTA, page flow) and microcopy (no em dashes, no negation-triads, no hype, sentence
  case).
- **Transitions** ([transitions/](./transitions/)) — eighteen paste-ready CSS
  transitions with shared motion tokens and a [`_root.css`](./transitions/_root.css).

Start with [SKILL.md](./SKILL.md). It is the entry point and routes to the rest.

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
