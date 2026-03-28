# ZAM Community Instance

This is a ZAM community instance. ZAM communities are purposeful collectives —
teams, open-source projects, professional associations, or any group that shares
beliefs, goals, and learning context.

## First time here?

Run `/setup` to complete first-time setup. It will:
- Install dependencies and distribute skill files (`zam setup`)
- Configure the community identity
- Set up any linked source repositories for developer communities

## Regular use

Run `/zam` to start a learning session in the context of this community.

## What lives here

- `beliefs/` — the community's shared worldview, approved by git commit
- `goals/` — shared objectives, decomposed into tasks and learning tokens
- `members/` — membership model and member list

The git history is the approval trail. Every committed change represents a
conscious decision made collaboratively.

## Skill files

After running `zam setup`, you will find:
- `.claude/skills/zam/SKILL.md` — the ZAM learning agent skill for Claude Code
- `.gemini/skills/zam/SKILL.md` — the same for Gemini CLI

To update them after a `zam-core` upgrade: `npm install && npx zam setup --force`
