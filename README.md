# Claude Code Enhancements

A collection of custom agents and skills that extend [Claude Code](https://docs.anthropic.com/en/docs/claude-code) with intelligent automation, self-improvement, and autonomous operation capabilities.

## What's Inside

### Agents

| Agent | Description |
|-------|-------------|
| **[AI Improvement Agent](agents/ai-improvement-agent.md)** | Evaluates, interrogates, and improves AI agent configurations. Provides structured improvement recommendations with options and reasoning before making any changes. Works with both Claude Code agents and ServiceNow AI configurations. |

### Skills

| Skill | Slash Command | Description |
|-------|---------------|-------------|
| **[Intelligent Model Router](skills/intelligent-model-router/)** | `/smartroute` | Autonomous model routing that analyzes task complexity (0-15 scoring), decomposes work into planning (Opus), execution (Sonnet), and simple (Haiku) phases. Achieves 60-80% cost savings vs all-Opus while maintaining quality where it matters. |
| **[Comprehensive Self-Improvement](skills/comprehensive-self-improvement/)** | *Auto-triggered* | Post-implementation learning system. Analyzes what was built, enhances specialist agent files with learned patterns, creates new sub-agents to fill coverage gaps, and logs all improvements for compounding knowledge. |
| **[Fully Autonomous Mode](skills/fullyautonomous/)** | `/fullyautonomous` | Status dashboard for autonomous mode. Displays current state, active behavioral directives, and safety boundaries that are always enforced. |
| **[Auto-On](skills/auto-on/)** | `/auto-on` | Enables fully autonomous mode — bypasses permission prompts for the session. Backs up current permissions, enables all behavioral directives, and maintains a full audit log. |
| **[Auto-Off](skills/auto-off/)** | `/auto-off` | Disables fully autonomous mode — restores standard permission prompts. Reverts behavioral directives and logs the action. |

## Installation

Copy the contents into your Claude Code configuration directory:

```bash
# Agents
cp -R agents/ ~/.claude/agents/

# Skills
cp -R skills/ ~/.claude/skills/
```

Restart Claude Code to pick up the new configurations.

## Directory Structure

```
.
├── agents/
│   └── ai-improvement-agent.md        # Agent interrogator & improvement advisor
└── skills/
    ├── auto-off/
    │   └── SKILL.md                    # Disable autonomous mode
    ├── auto-on/
    │   └── SKILL.md                    # Enable autonomous mode
    ├── comprehensive-self-improvement/
    │   └── SKILL.md                    # Post-execution learning system
    ├── fullyautonomous/
    │   ├── SKILL.md                    # Autonomous mode status & docs
    │   └── autonomous-config.json      # Runtime configuration state
    └── intelligent-model-router/
        └── SKILL.md                    # Smart model selection engine
```

## How It Works

### Intelligent Model Router

Routes every task to the optimal model based on complexity scoring:

- **Simple (0-3)** — File reads, lookups, formatting → **Haiku** (fastest, cheapest)
- **Standard (4-8)** — Code generation, analysis, refactoring → **Sonnet** (balanced)
- **Complex (9+)** — Architecture, multi-phase workflows → **Opus** (most capable)

Planning is always Opus. Execution defaults to Sonnet. Simple subtasks use Haiku.

### Autonomous Mode

A three-part system for controlling permission behavior:

1. `/fullyautonomous` — Check current status
2. `/auto-on` — Enable (bypasses confirmation prompts, maintains audit log)
3. `/auto-off` — Disable (restores standard permission flow)

Safety boundaries are **always enforced** regardless of mode — no credentials, SSH keys, API tokens, or destructive operations on protected paths.

### Self-Improvement System

Runs automatically after implementation cycles complete:

1. **Analyze** — Reviews what was built and identifies patterns
2. **Enhance** — Updates specialist agent files with learned improvements
3. **Expand** — Creates new sub-agents to fill discovered gaps
4. **Log** — Records all changes for traceability

### AI Improvement Agent

An interrogation-first approach to agent improvement:

1. **Deep read** — Analyzes every line of the target agent configuration
2. **Strategic questioning** — Probes for pain points, goals, and constraints
3. **Structured options** — Presents 2-4 improvement paths with trade-offs
4. **Approval gate** — Never modifies an agent without explicit consent

## Requirements

- [Claude Code CLI](https://docs.anthropic.com/en/docs/claude-code) installed and configured
- Claude API access (Opus, Sonnet, and/or Haiku models)

## License

Private repository. All rights reserved.
