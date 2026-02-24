# Version Control

Drop this section into your workspace-level `CLAUDE.md` (the one at the root of your project or workspace). Claude will proactively manage git operations — commits, changelogs, and releases — with human approval at every decision point.

**Nothing is pushed to the remote without your explicit approval.**

---

## Version Control

Claude **proactively manages** version control. You should not have to think about commits, changelogs, or releases — Claude handles the mechanics and prompts for approval at decision points.

### Sources of Truth

- `CHANGELOG.md` — [Keep a Changelog](https://keepachangelog.com/) format
- Git tags — annotated, `vX.Y.Z` semantic versioning

### Session Start

Check for **drift** between the latest git tag and `CHANGELOG.md` version heading. If out of sync, flag it immediately before doing anything else.

### Commits

- Use **conventional commits** (`<type>(<scope>): <description>`)
- After completing a logical unit of work, **suggest a commit** and wait for user approval
- On approval: stage, commit, and **auto-update** the `[Unreleased]` section of `CHANGELOG.md` (no separate prompt)
- When a commit adds, removes, or restructures a component — or changes how components depend on or communicate with each other — **update ARCHITECTURE.md in the same commit**
- When a commit changes build/dev/test commands, makes a technical decision that constrains future work, or changes the project's high-level shape — **update the project's CLAUDE.md** in the same commit
- After encountering a recurring issue or discovering a file that requires context to modify correctly — **suggest a CLAUDE.md addition** and wait for approval

### Releases

- After significant work, **suggest a release** with the appropriate semver bump and wait for approval
- On approval: update CHANGELOG, commit, tag, push, and create a GitHub Release via `gh`
- When preparing a release, review whether accumulated changes affect the README (new features, changed commands, updated scope) and **update README.md in the release commit** if so

### Standard Project Documents

Every project should have:

| File              | Purpose                                                          |
| ----------------- | ---------------------------------------------------------------- |
| `CLAUDE.md`       | AI workspace guidance (project-specific)                         |
| `.gitignore`      | Version control exclusions                                       |
| `README.md`       | Human-facing project overview                                    |
| `CHANGELOG.md`    | Change history ([Keep a Changelog](https://keepachangelog.com/)) |
| `ARCHITECTURE.md` | System design reference                                          |
