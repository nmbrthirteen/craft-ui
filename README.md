# Craft UI

The go-to agent skill for design engineering — direction, build, motion, dark mode,
responsive, anti-slop, and ship review — by [Nika Siradze](https://nikusha.com).

Working code is free. Craft UI is the judgment layer that stops interfaces from
reading as unfinished or generated: concentric radius, motion that earns its time,
contrast that holds, copy without generator tells, paste-ready transitions when the
motion decision is yes.

## What it covers

[SKILL.md](./SKILL.md) is the entry: setup protocol, intent map, absolute bans,
verify gate, review tables. Satellites load on demand:

- **Direction** ([start-here.md](./start-here.md)) — register, plan, brand kit, ideas
- **Surfaces** ([surfaces.md](./surfaces.md)) — radius, depth, cards, spacing, responsive
- **Typography** ([typography.md](./typography.md))
- **Motion** ([motion.md](./motion.md))
- **Color / dark mode** ([color.md](./color.md))
- **Aesthetics** ([aesthetics.md](./aesthetics.md))
- **Copy** ([copy.md](./copy.md))
- **Transitions** ([transitions/](./transitions/)) — eighteen paste-ready CSS recipes

## Install

```bash
git clone git@github.com:nmbrthirteen/craft-ui.git ~/.agents/skills/craft-ui
```

If your setup loads skills from `~/.claude/skills`, symlink it there:

```bash
ln -s ~/.agents/skills/craft-ui ~/.claude/skills/craft-ui
```

Invoke as `/craft-ui`, or let it trigger on design and polish work. Agents follow
[SKILL.md](./SKILL.md): route the ask (`design`, `brand kit`, `dark mode`,
`responsive`, `animate`, `polish`, …), read project tokens first, load only the
satellites that route needs.

## License

MIT. See [LICENSE](./LICENSE).
