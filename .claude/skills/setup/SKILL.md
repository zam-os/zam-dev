---
name: setup
description: First-time setup for a ZAM community instance. Reads .zam/config.yaml, distributes skill files, clones listed source repos, and links any source packages. Run this once after creating your community repo from the template.
user-invocable: true
---

# ZAM Community Setup

You are guiding the user through first-time setup of their ZAM community instance.
Be direct and practical. Run each step, confirm it worked, then move to the next.

---

## What you are setting up

- **This repo** (`beliefs/`, `goals/`, `members/`) — the community's slow layer. Tracked in git.
- **Skill files** — copied from `zam-core` into `.claude/skills/zam/` and `.gemini/skills/zam/`.
- **Source repos** — cloned alongside this repo, linked if they are source packages.

---

## Step 0 — Read community config

Read `.zam/config.yaml`. Extract:
- `identity.community_id`
- `repos[]` — list of `{url, description, link}` entries

## Step 1 — Detect platform

```bash
uname -s
```

- **Darwin** → macOS. Package manager: `brew`.
- **MINGW***, **MSYS***, **CYGWIN***, or failure → Windows. Package manager: `winget`.

## Step 2 — Check Node.js

```bash
node --version
```

Must be v18 or later. If missing:

| Platform | Command |
|----------|---------|
| macOS | `brew install node` |
| Windows | `winget install OpenJS.NodeJS` |

## Step 3 — Install dependencies

```bash
npm install
npx zam --version
```

## Step 4 — Distribute skill files

```bash
npx zam setup --skip-init --skip-claude-md
```

Copies `.claude/skills/zam/` and `.gemini/skills/zam/` from `node_modules/zam-core/`.

To update existing files: `npx zam setup --skip-init --skip-claude-md --force`

## Step 5 — Clone source repos

**Skip if `repos` in config is empty.**

Determine the parent directory:
```bash
dirname $(pwd)
```

For each entry in `repos[]`:

**5a. Clone if not already present:**
```bash
git clone https://github.com/<org>/<repo> <parent-dir>/<repo>
```

**5b. If `link: true` — build and link the package:**
```bash
cd <parent-dir>/<repo>
npm install
npm link
```

Then link into this community instance:
```bash
cd <community-dir>
npm link <package-name>
```

Package name comes from `<repo>/package.json` → `"name"` field.

Confirm:
```bash
npx zam --version
```

## Step 6 — Commit setup artifacts

```bash
git add .claude/skills/zam/ .gemini/skills/zam/ CLAUDE.md
git commit -m "chore: distribute zam-core skill files"
```

## Step 7 — Done

Tell the user:

> "Community setup is complete. Add your community's beliefs, goals, and members,
> then commit each change. Members join by listing this community in their personal
> `.zam/config.yaml` and running `/setup`."

---

## Updating after a zam-core upgrade

```bash
npm install
npx zam setup --skip-init --skip-claude-md --force
git add .claude/skills/zam/ .gemini/skills/zam/
git commit -m "chore: update zam-core skill files"
```
