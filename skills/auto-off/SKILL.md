---
name: auto-off
description: |
  Disable Fully Autonomous Mode — restore standard permission prompts.
  Use /auto-on to enable, /auto-off to disable, /fullyautonomous for status.
---

# Disable Fully Autonomous Mode

You are disabling Fully Autonomous Mode. This restores standard permission-checking behavior.

## Actions to Take:

1. Read `~/.claude/skills/fullyautonomous/autonomous-config.json` — check current state
2. If already disabled, inform the user ("Autonomous mode is already off.") and exit early
3. Update `~/.claude/skills/fullyautonomous/autonomous-config.json`:
   - Set `"autonomous_mode": false`
   - Set all `behavioral_directives` to `false`:
     - `"skip_confirmation_prompts": false`
     - `"use_dangerously_disable_sandbox": false`
     - `"auto_approve_file_operations": false`
     - `"auto_approve_bash_commands": false`
   - Set `"last_updated"` to the current ISO 8601 timestamp
   - Set `"last_action": "disabled"`
   - Clear `"permissions_backup"` to `null`
   - Append to `"audit_log"`: `{"action": "disabled", "timestamp": "<current>", "source": "/auto-off"}`
4. Display the confirmation banner below

## Confirmation Banner:

```
============================================
   FULLY AUTONOMOUS MODE: DISABLED
============================================

   Standard permission checks restored.
   Claude will now ask for confirmation
   before executing commands and file
   operations as normal.

   Changes:
   - Bash sandbox bypass: OFF
   - Skip confirmations: OFF
   - Auto-approve file ops: OFF
   - Auto-approve commands: OFF

   Use /auto-on to re-enable autonomous mode.
============================================
```

## Behavioral Change for This Session:

After disabling autonomous mode, you MUST resume standard behavior:

1. **Bash commands**: Do NOT set `dangerouslyDisableSandbox: true` — use normal sandboxed execution
2. **File operations**: Follow standard permission flow for Write and Edit calls
3. **Destructive operations**: Always confirm before executing
4. **Multi-step tasks**: Pause for confirmation at appropriate points

Now execute the update.
