# Craft UI

The AI ships working code. That part is free now.

Craft UI is the layer after: the small calls that decide whether a screen feels
considered or generated. An agent skill for craft-level UI work, by
[Nika Siradze](https://nikusha.com).

## What it does

Guarantees a quality floor. It does not hand you a look. [SKILL.md](./SKILL.md) is
the entry point: an agent protocol (load only what the mode needs), hard
correctness rules, taste defaults, review tables, and a ship checklist.

Satellites, loaded on demand:

- **From brief to UI** ([start-here.md](./start-here.md))
- **Surfaces** ([surfaces.md](./surfaces.md))
- **Typography** ([typography.md](./typography.md))
- **Motion** ([motion.md](./motion.md))
- **Color** ([color.md](./color.md))
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

Invoke as `/craft-ui`, or let it trigger on UI and polish work. Agents follow the
setup + intent map in [SKILL.md](./SKILL.md): route the ask (`polish`, `animate`,
`quieter`, `shape`, …), read the project's tokens first, load only the satellites
that route needs, decide motion before pasting a catalog recipe.

## License

MIT. See [LICENSE](./LICENSE).
