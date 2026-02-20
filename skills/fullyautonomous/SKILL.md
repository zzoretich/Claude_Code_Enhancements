---
name: fullyautonomous
description: |
  Fully Autonomous Mode — operate without permission prompts.
  Use /fullyautonomous to check status. Use /auto-on to enable, /auto-off to disable.
---

# Fully Autonomous Mode — Status & Documentation

You are displaying the current status of Fully Autonomous Mode.

## Actions to Take:

1. Read the configuration file at `~/.claude/skills/fullyautonomous/autonomous-config.json`
2. Display the status banner below based on current state
3. Show usage instructions

## Status Banner:

Read `autonomous-config.json` and display the appropriate banner:

### If `autonomous_mode` is `true`:

```
============================================
   FULLY AUTONOMOUS MODE: ENABLED
============================================

Status:     ACTIVE
Enabled:    {last_updated}
Action:     {last_action}

Active Behavioral Directives:
   - Skip confirmation prompts: ON
   - Bash sandbox bypass: ON
   - Auto-approve file operations: ON
   - Auto-approve bash commands: ON

Safety Boundaries (ALWAYS enforced):
   - NO credentials, .env, SSH keys, API tokens
   - NO system files (/etc/, /System/, /Library/)
   - NO force-push to main/master
   - NO rm -rf outside project directory
   - NO network listeners without explicit request

Toggle: /auto-off to disable
============================================
```

### If `autonomous_mode` is `false`:

```
============================================
   FULLY AUTONOMOUS MODE: DISABLED
============================================

Status:     INACTIVE
Last changed: {last_updated or "Never enabled"}

All standard permission checks are active.
Claude will ask for confirmation before:
   - Running bash commands
   - Writing/editing files
   - Performing destructive operations

Toggle: /auto-on to enable
============================================
```

## What Autonomous Mode Changes:

| Behavior | Normal Mode | Autonomous Mode |
|----------|-------------|-----------------|
| Bash commands | Asks permission | Executes immediately with `dangerouslyDisableSandbox: true` |
| File writes/edits | May ask permission | Executes immediately |
| Destructive operations | Always confirms | Executes immediately (except safety boundaries) |
| Git operations | Follows git safety protocol | Same — git safety protocol ALWAYS active |

## Safety Boundaries (Never Bypassed):

These restrictions are **ALWAYS ENFORCED** regardless of autonomous mode:

1. **Credentials & Secrets**: Never read/write/expose `.env`, SSH keys, API tokens, credentials files
2. **System Files**: Never modify `/etc/`, `/System/`, `/Library/` system directories
3. **Git Force Push**: Never force-push to main/master branches
4. **Destructive Cleanup**: Never `rm -rf` outside the current project directory
5. **Network Listeners**: Never start network listeners without explicit user request

## Commands:

- `/auto-on` — Enable autonomous mode
- `/auto-off` — Disable autonomous mode
- `/fullyautonomous` — Show this status page

Now execute the status display.
