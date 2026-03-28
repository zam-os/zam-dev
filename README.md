# ZAM Developer Community

This is the ZAM developer community — the group of people actively building
[zam-core](https://github.com/zam-os/zam), the symbiotic learning kernel.

## What lives here

- **`beliefs/`** — our shared engineering principles, committed to git.
- **`goals/`** — what we are building and why.
- **`members/`** — who is in the community and their role.
- **`.zam/config.yaml`** — the repos every member clones locally.

## Joining

Add this community to your personal `.zam/config.yaml`:

```yaml
communities:
  - url: github:zam-os/zam-dev
    role: developer
```

Then run `/setup` in your personal instance. It will clone this repo and all
listed source repos automatically, and set up `npm link` so your local
`zam-core` source is used instead of the npm package.

## What setup clones

When you run `/setup` as a `zam-dev` member, these repos are cloned alongside
your personal instance:

| Repo | Purpose | Linked |
|------|---------|--------|
| `zam-os/zam` | zam-core source — CLI, kernel, FSRS engine | `npm link` |
| `zam-os/zam-personal` | Personal instance template | No |
| `zam-os/zam-community` | Community instance template | No |

## Workflow

Work happens in `zam-os/zam`. Changes to the kernel are proposed as PRs,
reviewed, and merged. The templates (`zam-personal`, `zam-community`) are
updated when setup or config schema changes.

See [`docs/TEMPLATES.md`](https://github.com/zam-os/zam/blob/main/docs/TEMPLATES.md)
for the full template/instance model.
