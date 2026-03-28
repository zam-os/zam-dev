# Your ZAM Community Instance

This is a ZAM community instance. Use this template to create a shared ZAM
space for a team, open-source project, professional association, or any
purposeful collective.

## What lives here

- **`beliefs/`** — the community's shared worldview. The ZAM agent uses these
  as context when assisting members. Approved by git commit.
- **`goals/`** — shared objectives, decomposed into tasks and learning tokens.
- **`members/`** — who belongs to this community and in what role.
- **`.zam/config.yaml`** — non-secret community configuration: identity, and the
  list of source repos members should clone locally.

## Getting started

### 1. Create your community repo from this template

Click **"Use this template"** on GitHub. For a public community (recommended),
create a public repository, e.g. `your-org/zam-your-community`.

Clone it:
```bash
git clone https://github.com/your-org/zam-your-community
cd zam-your-community
```

### 2. Edit `.zam/config.yaml`

Set the community identity and list any source repos members should clone:

```yaml
identity:
  community_id: your-community

repos:
  - url: github:your-org/your-main-repo
    description: The main source repository
    link: false
```

### 3. Run `/setup` in Claude Code or Gemini CLI

```bash
claude  # or: gemini
# then: /setup
```

### 4. Add beliefs, goals, and members

Edit the files in `beliefs/`, `goals/`, and `members/` to reflect your
community's identity. Commit each change — the git history is your approval trail.

## How members join

1. Members add this community to their personal instance's `.zam/config.yaml`:
   ```yaml
   communities:
     - url: github:your-org/zam-your-community
       role: member
   ```
2. They run `/setup` in their personal instance — it reads the community config,
   clones this repo and any listed source repos automatically.

## Supported platforms

| Platform | Package manager |
|----------|----------------|
| macOS (Apple Silicon) | Homebrew (`brew`) |
| Windows 11 | WinGet (`winget`) / WSL |

## Updating after a zam-core upgrade

```bash
npm install
npx zam setup --force
git add .claude/skills/zam/ .gemini/skills/zam/
git commit -m "chore: update zam-core skill files"
```
