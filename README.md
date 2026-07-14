# agent-skills

Roy Bakker's agent skills for real engineering. Plug-and-play instructions that make coding agents (Claude Code, Cursor, Codex, and others following the [Agent Skills spec](https://github.com/vercel-labs/skills)) more reliable at specific, well-scoped tasks.

## Skills

| Skill | Description |
|---|---|
| [`fix-merge-conflicts`](skills/engineering/fix-merge-conflicts/SKILL.md) | Resolves merge/rebase conflicts on a feature branch — explains every conflict and the proposed fix before touching a file, auto-resolves mechanical conflicts (lockfiles, formatting, non-overlapping additions), and only applies a logic-conflict resolution once you approve it. Runs the project's checks before the final commit. |

## Install

**Via the skills CLI** (copies the skill into your project, editable):

```bash
npx skills add RoyBkker/agent-skills
```

**As a Claude Code plugin** (read-only, managed bundle that updates when this repo does):

```
/plugin marketplace add RoyBkker/agent-skills
/plugin install agent-skills@RoyBkker
```

## License

MIT
