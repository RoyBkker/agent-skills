# agent-skills

Roy Bakker's agent skills for real engineering. Plug-and-play instructions that make coding agents (Claude Code, Cursor, Codex, and others following the [Agent Skills spec](https://github.com/vercel-labs/skills)) more reliable at specific, well-scoped tasks.

## Skills

| Skill | Description |
|---|---|
| [`fix-merge-conflicts`](skills/engineering/fix-merge-conflicts/SKILL.md) | Resolves merge/rebase conflicts on a feature branch — explains every conflict and the proposed fix before touching a file, auto-resolves mechanical conflicts (lockfiles, formatting, non-overlapping additions), and only applies a logic-conflict resolution once you approve it. Runs the project's checks before the final commit. |
| [`avoid-ai-writing-nl`](skills/writing/avoid-ai-writing-nl/SKILL.md) | Audits and rewrites **Dutch** text to remove AI writing patterns ("AI-ismen") — 47 source-verified patterns, a 3-tier vocabulary table, context profiles (social/blog/email/LinkedIn), je/u voice profiles, and detect/rewrite/edit modes. Every Dutch pattern is independently sourced (see its [`sources.md`](skills/writing/avoid-ai-writing-nl/sources.md)), not translated from English. Adapted from Conor Bronsdon's [avoid-ai-writing](https://github.com/conorbronsdon/avoid-ai-writing) (MIT). |

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
