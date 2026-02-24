# Version Control Module

A CLAUDE.md module that gives Claude Code proactive git management with human-in-the-loop approval.

## What It Does

Instead of manually managing commits, changelogs, and releases, Claude handles the mechanics:

- **Commits** — After completing work, Claude suggests a conventional commit and waits for your approval. On approval, it stages, commits, and updates `CHANGELOG.md` automatically.
- **Releases** — Claude suggests semver bumps at natural milestones. On approval, it updates the changelog, tags, pushes, and creates a GitHub Release.
- **Drift detection** — At session start, Claude checks that your latest git tag and changelog are in sync. If not, it flags the issue before doing anything else.
- **Doc co-evolution** — When commits affect architecture or project configuration, Claude updates `ARCHITECTURE.md` and `CLAUDE.md` in the same commit.

**The key guarantee: nothing is pushed to the remote without your explicit approval.**

## Installation

1. Open your workspace-level `CLAUDE.md` (at the root of your project or workspace)
2. Copy the `## Version Control` section from [`version-control.md`](version-control.md) into it
3. Create a `CHANGELOG.md` if you don't have one:

```markdown
# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/),
and this project adheres to [Semantic Versioning](https://semver.org/).

## [Unreleased]
```

4. Start a Claude Code session — it will pick up the new instructions immediately

## How It Compares to Auto-Sync

|                              | Auto-sync daemon      | This module                       |
| ---------------------------- | --------------------- | --------------------------------- |
| Push to remote               | Automatic, continuous | Only on explicit approval         |
| Commit granularity           | Every file save       | Logical units of work             |
| Commit messages              | Auto-generated        | Conventional commits with context |
| Changelog                    | Not maintained        | Auto-updated on every commit      |
| Releases                     | Not managed           | Semver tags + GitHub Releases     |
| Risk of overwriting branches | High                  | None — human approves every push  |
