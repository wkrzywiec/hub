# hub

Workspace that groups all of Wojciech's repositories, managed with [mani](https://manicli.com). This repo only holds `mani.yaml`, shared tasks and context files; every project below is its own git repo, ignored here via `.gitignore`.

## Layout

- `private/` - personal apps and local infrastructure (`mankkoo`, `local-postgres`, `newsletters-triage`).
- `blog/` - the personal site (`wkrzywiec.github.io`) and the side projects written about on it.
- `blog/projects/` - sandbox projects (`farm-to-table`, `nutri-chef-ai`).

## Commands

Run from this folder:

- `mani sync` - clone missing repos and update `.gitignore`.
- `mani run sync-main --all` - fetch, checkout the default branch (main or master) and fast-forward every repo.
- `mani list projects` - show all registered repos.

## Rules

- Each subfolder is an independent git repo with its own branches and remotes. Never commit across repos; run git inside the repo you change.
- Add new repos to `mani.yaml`, then `mani sync`. Read the repo's own `AGENTS.md` before working in it.
