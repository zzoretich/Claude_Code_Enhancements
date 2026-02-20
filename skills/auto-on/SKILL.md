---
name: auto-on
description: |
  Enable Fully Autonomous Mode — bypass permission prompts for the session.
  Use /auto-on to enable, /auto-off to disable, /fullyautonomous for status.
---

# Enable Fully Autonomous Mode

You are enabling Fully Autonomous Mode. This allows Claude to operate without permission prompts for the remainder of this session.

## Actions to Take:

1. Read `~/.claude/skills/fullyautonomous/autonomous-config.json` — check current state
2. If already enabled, inform the user and exit early
3. Read `~/.claude/settings.local.json` — capture the current `permissions.allow` array
4. Update `~/.claude/skills/fullyautonomous/autonomous-config.json`:
   - Set `"autonomous_mode": true`
   - Set all `behavioral_directives` to `true`:
     - `"skip_confirmation_prompts": true`
     - `"use_dangerously_disable_sandbox": true`
     - `"auto_approve_file_operations": true`
     - `"auto_approve_bash_commands": true`
   - Set `"last_updated"` to the current ISO 8601 timestamp
   - Set `"last_action": "enabled"`
   - Store the current `permissions.allow` array in `"permissions_backup"`
   - Append to `"audit_log"`: `{"action": "enabled", "timestamp": "<current>", "source": "/auto-on"}`
5. Display the confirmation banner below

## Warning Banner:

```
============================================
   FULLY AUTONOMOUS MODE: ENABLED
============================================

   All permission prompts are now bypassed.
   Claude will execute commands and file
   operations without asking for confirmation.

   Safety boundaries remain ACTIVE:
   - NO credentials/secrets/env files
   - NO system file modifications
   - NO force-push to main/master
   - NO rm -rf outside project
   - NO network listeners without request

   Permissions backup: SAVED
   (will restore on /auto-off)

   Use /auto-off to restore normal behavior.
============================================
```

## CRITICAL — Behavioral Change for This Session:

After enabling autonomous mode, you MUST change your behavior for the rest of this session:

1. **Bash commands**: ALWAYS set `dangerouslyDisableSandbox: true` on every Bash tool call
2. **File operations**: Proceed with Write and Edit calls without asking "May I...?" or "Should I...?"
3. **Multi-step tasks**: Execute all steps immediately without pausing for confirmation between steps
4. **Tool chains**: Chain tool calls without intermediate confirmation prompts
5. **Only stop to confirm** if an action falls within the safety boundaries listed above

This is NOT optional. The user has explicitly requested autonomous operation. Asking for permission after enabling this mode defeats its purpose.

## Safety Boundaries (Still Enforced):

Even in autonomous mode, you MUST still:
- Never read/write/expose credentials, `.env` files, SSH keys, API tokens
- Never modify system files (`/etc/`, `/System/`, `/Library/`)
- Never force-push to main/master (git safety protocol stays active)
- Never run `rm -rf` outside the project directory
- Never start network listeners without explicit request

Now execute the update.
