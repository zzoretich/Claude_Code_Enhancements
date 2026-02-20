---
name: comprehensive-self-improvement
description: |
  Auto-enhancement system that runs after every JARVIS implementation.
  Analyzes execution results, identifies improvements, enhances specialist
  agent files with learned patterns, and creates new sub-agents to fill
  coverage gaps. Continuous learning that compounds over time.
---

# Comprehensive Self-Improvement System

## Purpose

This skill provides JARVIS with the ability to learn from every implementation and continuously improve its specialist agent files. After each implementation cycle completes (Step 7: Documentation Generation), this system automatically:

1. **Analyzes** what was built, what worked, and what didn't
2. **Enhances** existing specialist agent .md files with learned patterns
3. **Creates new sub-agents** to fill discovered coverage gaps
4. **Logs** all improvements for traceability and compounding knowledge

This is **Phase 3** of the JARVIS workflow:
```
Phase 1: Strategic Planning (with user approval)
Phase 2: Parallel Dispatch Execution (autonomous)
Phase 3: Self-Improvement (automatic)  <-- THIS SKILL
```

---

## When This Skill Runs

**Trigger:** Automatically after Step 7 (Documentation Generation) completes in the orchestrator workflow.

**Model:** Opus (for strategic-level analysis)

**Frequency:** After every implementation cycle

**Duration:** Runs autonomously — no user approval required for analysis. User confirmation required before modifying agent files.

---

## Implementation Instructions

**WHEN THIS SKILL IS INVOKED (after Step 7 completes):**

### STEP 1: Gather Implementation Context

Read the implementation artifacts from the Instance Projects folder:

```
[Instance Projects]/[INSTANCE_NAME]/
├── docs/[PROJECT_NAME]/
│   ├── implementation-summary.md    ← What was built
│   ├── technical-readme.md          ← Technical details
│   └── demo-script.md              ← Demo narrative (if applicable)
├── scans/                           ← Instance state before/after
├── rollbacks/                       ← Rollback plans generated
└── PROJECT_INDEX.md                 ← Master index
```

**Actions:**
1. Read `~/.claude/servicenow-config.json` to get Instance Projects path
2. Read the latest implementation summary for the current instance
3. Read the task list (TaskList) to review all completed tasks and their outcomes
4. Note which specialist agents were activated during this implementation
5. Identify any errors, workarounds, or manual interventions that occurred
6. **If Agent Teams were used:** Read team execution logs — check for teammate message history, task claiming patterns, and cross-domain handoff data in task descriptions (look for `OUTPUTS:` JSON blocks)

---

### STEP 2: Analysis Framework

Analyze the implementation across **6 dimensions** (plus team coordination if applicable):

#### 2a. Execution Quality
- Did each activated specialist agent complete its tasks correctly?
- Were MCP tool calls successful on first attempt or did they require retries?
- Did the generated records match the requirements?
- Were validation checks (UAT) passing?

#### 2b. Gap Detection
- Were there tasks that no specialist agent could handle?
- Did any agent lack specific capabilities needed for this implementation?
- Were there ServiceNow features or modules with no agent coverage?
- Did the orchestrator have to improvise without agent guidance?

#### 2c. Pattern Recognition
- What new implementation patterns emerged?
- What MCP tool combinations worked well together?
- What data creation sequences were most efficient?
- What configuration approaches produced the best results?

#### 2d. Error Analysis
- What failed during execution and why?
- Were there API errors, permission issues, or data conflicts?
- What workarounds were needed?
- Could these errors be prevented with better agent guidance?

#### 2e. Efficiency Review
- Could more tasks have been parallelized?
- Were there unnecessary sequential dependencies?
- Did any agent do redundant work?
- What was the optimal task ordering discovered?

#### 2f. Team Coordination Quality (if Agent Teams were used)
- **Communication Effectiveness:** Did teammates send clear, structured completion messages with all required outputs?
- **Task Claiming Patterns:** Did teammates claim tasks promptly as dependencies resolved? Were there starvation periods where teammates sat idle?
- **Domain Clustering Accuracy:** Were the right agents in the right clusters? Did any task require knowledge from a different cluster?
- **Cross-Domain Handoffs:** Were dependency outputs passed correctly between clusters? Did the leader need to intervene frequently?
- **Deadlock Detection:** Were there circular waits or tasks that couldn't proceed due to coordination failures?
- **Cluster Recommendations:** Should any agents be moved between clusters based on this implementation's patterns?
- **Team Size Efficiency:** Were too many or too few teammates spawned? Did any teammate have too little work?

#### 2g. Mastery Knowledge Alignment

Cross-reference the implementation against the ServiceNow Mastery knowledge base to verify that agents followed authoritative best practices, used correct license tiers, applied current configuration patterns, and avoided deprecated features.

**Reference Files (read from `~/.claude/servicenow-config.json` → `mastery_path`):**
- `mastery-index.json` — Product-to-agent mapping and Mastery doc paths
- `license-intelligence.json` — License tier data, prerequisites, and add-on requirements
- `zurich-deprecation-index.json` — Deprecated features, EOL dates, and migration paths
- `product-integration-graph.json` — Cross-product dependencies and integration points

**Alignment Checks:**

- **Best Practice Adherence:** Did activated agents follow the implementation best practices documented in their corresponding Mastery docs? Cross-reference the implementation steps against the "Implementation Best Practices" and "Configuration Guide" sections of the relevant Mastery doc (located via `mastery-index.json`).

- **Configuration Pattern Consistency:** Were configuration values (system properties, business rules, ACLs, workflow settings) consistent with the "Common Configuration Patterns" and "Configuration Guide" sections in Mastery docs? Flag any deviations from documented recommended values.

- **License Tier Accuracy:** Did the implementation activate plugins or features that require a higher license tier than what was specified? Cross-reference activated features against `license-intelligence.json` to verify that:
  - Base tier features were not mistakenly flagged as requiring higher tiers
  - Pro/Enterprise features were correctly identified as requiring upgrades
  - Now Assist features were only configured when the Now Assist add-on was confirmed
  - Add-on products were correctly identified as separate SKUs

- **Deprecated Feature Avoidance:** Did any agent configure or reference deprecated/EOL features? Cross-reference against `zurich-deprecation-index.json` to verify:
  - No deprecated plugins were activated (e.g., Legacy Workflows instead of Flow Designer)
  - No EOL products were implemented (e.g., Cloud Observability instead of Service Observability)
  - Migration paths were followed when replacing deprecated features
  - Deprecated UI frameworks were not used (e.g., Legacy Studio instead of ServiceNow IDE)

- **Cross-Product Integration Accuracy:** When multiple products were configured together, were the integration points consistent with `product-integration-graph.json`? Verify that:
  - Required prerequisite products were configured first
  - Integration dependencies were satisfied (e.g., ITOM Visibility before ITOM Health)
  - Shared data models (CMDB classes, tables) were configured correctly for cross-product use

**Mastery Alignment Score:**
Rate each sub-check on a 3-point scale:
- **Aligned** — Implementation matches Mastery guidance
- **Partial** — Implementation mostly matches but has minor deviations
- **Misaligned** — Implementation contradicts or ignores Mastery guidance

**Improvement Actions (when misalignment detected):**
1. Log the misalignment with specific Mastery doc reference (file path + section)
2. Append corrective guidance to the relevant specialist agent's "Learned Improvements" section
3. If a pattern of misalignment is detected across multiple implementations, escalate to agent file revision (update core guidance, not just learned improvements)
4. Update `license-intelligence.json` or `zurich-deprecation-index.json` if the reference data itself was found to be incomplete or incorrect

---

### STEP 3: Enhance Existing Agent Files

For each specialist agent that was activated during the implementation:

1. **Read** the current agent file from `~/.claude/skills/servicenow-architect-agent/references/`
2. **Identify** specific improvements based on the analysis
3. **Append** improvements in a clearly marked section at the end of the agent file

**Improvement Append Format:**
```markdown
---

## Learned Improvements

### [YYYY-MM-DD] - [Instance Name] - [Project Name]

#### New Patterns Discovered
- [Pattern description with specific MCP tool calls or configuration steps]

#### Best Practices Confirmed
- [Practice that worked well and should be reinforced]

#### Known Issues & Workarounds
- [Issue encountered] → [Workaround applied] → [Root cause if known]

#### Recommended Defaults
- [Setting/configuration that should be the default going forward]
```

**Domain-Aware Tagging for Consolidated Agents:**

For consolidated agent files (e.g., telecom-operations-agent.md, financial-services-agent.md), always include the DOMAIN tag to keep improvements organized by sub-domain within the unified file. Use this format instead:

```markdown
### [YYYY-MM-DD] - [Instance] - [Project] - DOMAIN: [ITOM|BANKING|INSURANCE|FSO|HEALTHCARE|LIFE-SCIENCES|TELECOM-CSM|TELECOM-NETWORK|TELECOM-ORDERS|MANUFACTURING|RETAIL|ENERGY-UTILITIES|PUBLIC-SECTOR|TECH-PROVIDER|WORKPLACE|VISITOR-MGMT|SPACE-MGMT|SOURCING|SUPPLIERS|CONTRACTS|LEGAL-SERVICE|LEGAL-MATTERS|E-BILLING|AP|PAYMENTS|FINANCE-CLOSE|ENVIRONMENTAL|SOCIAL]
```

> **Note:** For consolidated agent files (e.g., telecom-operations-agent.md, financial-services-agent.md), always include the DOMAIN tag to keep improvements organized by sub-domain within the unified file.

### Step 3.1: Mastery Validation of Enhancement Output

**BEFORE writing any enhanced agent file**, run this validation:

1. **Read the corresponding Mastery doc** for the agent being modified:
   - Look up the agent in `mastery-index.json` to find its primary Mastery doc (`mastery_doc` path)
   - Read the Mastery doc's "Implementation Best Practices" section
   - Read the "Scripting & Customization" section
   - Read the "Configuration Guide" recommended values

2. **Cross-reference proposed enhancements:**
   - Do new patterns align with Mastery's recommended configuration approaches?
   - Do new scripts follow Mastery's API usage examples?
   - Do new pitfall notes match or complement Mastery's "Common Pitfalls"?
   - Do recommended defaults match Mastery's "Configuration Guide" values?

3. **Conflict resolution:**
   - If a proposed enhancement **CONTRADICTS** Mastery guidance → **Discard the enhancement** and log the conflict
   - If a proposed enhancement **EXTENDS** Mastery guidance → **Keep and annotate** as "extends Mastery baseline"
   - If a proposed enhancement **MATCHES** Mastery → **Keep as-is** (best outcome)
   - If Mastery has **NO COVERAGE** for the learned pattern → **Keep as novel learning** (the enhancement proceeds normally)

4. **Log validation results** to the improvement archive (included in Step 6.5 JSON output):
   ```json
   {
     "agent": "agent-name.md",
     "enhancements_proposed": 5,
     "enhancements_validated": 4,
     "enhancements_discarded": 1,
     "mastery_conflicts": ["Proposed custom assignment rule conflicts with Mastery's recommended OOB skills-based routing"],
     "mastery_extensions": ["Added shift-calendar-aware escalation pattern not in Mastery"],
     "mastery_matches": ["Confirmed SLA attachment order matches Mastery best practice"],
     "novel_learnings": ["Bulk import optimization for 1000+ CI records — no Mastery coverage"]
   }
   ```

**Safety Rules for Agent Enhancement:**
- NEVER remove or modify existing content in agent files
- ONLY append new content in the "Learned Improvements" section
- Each improvement entry is timestamped and traced to a specific implementation
- If a "Learned Improvements" section already exists, append to it (don't create duplicate sections)

**Team Configuration Recommendations (if applicable):**
If Agent Teams were used and dimension 2f analysis reveals improvements:
- Update `~/.claude/servicenow-config.json` with recommended `team_complexity_threshold` adjustments
- Log cluster reassignment recommendations (e.g., "Move {agent} from {cluster_a} to {cluster_b}")
- Note optimal team sizes for different project types in the improvement log
- Flag communication pattern improvements for the TEAM EXECUTION PROTOCOL in the orchestrator

---

### STEP 4: Gap Analysis — Identify Missing Agent Coverage

Review the implementation for areas where no specialist agent existed:

**Gap Detection Criteria:**
1. The orchestrator had to create implementation steps without referencing any agent file
2. A ServiceNow module or feature was configured that has no dedicated agent
3. A cross-product integration pattern was needed but not covered by any agent
4. An industry-specific workflow was required but no industry agent matched
5. A new ServiceNow capability (recent release) has no agent coverage

**Gap Documentation Format:**
```
GAP IDENTIFIED:
  Domain: [ServiceNow module/feature/capability]
  Detected During: [What task or step revealed the gap]
  Impact: [How the implementation was affected]
  Recommendation: Create new agent | Extend existing agent
  Priority: Critical | High | Medium | Low
  Rationale: [Why this gap matters for future implementations]
```

---

### STEP 5: Create New Sub-Agents

For each gap identified with recommendation "Create new agent":

#### 5a. Agent File Generation

Use Claude (Opus) to generate a new specialist agent .md file. The new agent MUST follow the established template structure derived from existing agents:

**Required Sections for New Agents:**

```markdown
# [Agent Name]

[One-line description of specialization]

## Capabilities

### [Capability Area 1]
- [Specific capability with details]

### [Capability Area 2]
- [Specific capability with details]

## Implementation Patterns

### [Pattern Name]
[Detailed implementation steps with MCP tool usage]

## MCP Tools Used

List the specific `mcp__servicenow__*` tools this agent relies on:
- `mcp__servicenow__servicenow_query_table` — [How used]
- `mcp__servicenow__servicenow_create_record` — [How used]
- [Additional tools as needed]

## Configuration Steps

### Step 1: [First configuration step]
[Detailed instructions]

### Step 2: [Next step]
[Detailed instructions]

## Validation

### Pre-Implementation Checks
- [Check 1]
- [Check 2]

### Post-Implementation Validation
- [Validation query or check 1]
- [Validation query or check 2]

## Rollback

### If Rollback Needed
- [Rollback step 1 with specific MCP tool calls]
- [Rollback step 2]

## Dependencies
- [Other agents this agent depends on]
- [Required ServiceNow plugins or features]

## Keywords
[Comma-separated routing keywords for the orchestrator's SKILL.md]
```

#### 5b. Agent File Naming Convention

- Format: `[domain]-agent.md` (lowercase, hyphenated)
- Examples: `workplace-analytics-agent.md`, `cmdb-health-agent.md`, `custom-app-agent.md`
- Save to: `~/.claude/skills/servicenow-architect-agent/references/`

#### 5c. Update Routing Table

After creating a new agent, update the routing logic in `~/.claude/skills/servicenow-architect-agent/SKILL.md`:
- Add the new agent to the appropriate product category section
- Add routing keywords that map to the new agent
- Add the agent to the agent count

#### 5d. Agent Creation Log

For each new agent created, log:
```
NEW AGENT CREATED:
  File: [filename].md
  Domain: [ServiceNow area covered]
  Triggered By: [Implementation that revealed the gap]
  Keywords: [Routing keywords added]
  Date: [YYYY-MM-DD]
  Rationale: [Why this agent was needed]
  Status: Draft (requires validation in next implementation)
```

---

### STEP 6: Log All Improvements

Save a comprehensive improvement log to the Instance Projects folder:

**Log Location:**
```
[Instance Projects]/[INSTANCE_NAME]/improvements/
├── YYYY-MM-DD_improvement-log.md      ← Detailed log
└── improvement-index.md               ← Running index of all improvements
```

**Improvement Log Format:**
```markdown
# Self-Improvement Log — [Date]

## Implementation Context
- **Instance:** [instance name]
- **Project:** [project name]
- **Agents Activated:** [count] of [total available]
- **Tasks Completed:** [count]
- **Errors Encountered:** [count]

## Analysis Summary

### Execution Quality Score
[Assessment of overall execution quality]

### Gaps Detected
[List of coverage gaps found]

### Patterns Learned
[New patterns discovered]

### Mastery Alignment
| Check | Status | Details |
|-------|--------|---------|
| Best Practice Adherence | [Aligned/Partial/Misaligned] | [specifics] |
| Configuration Consistency | [Aligned/Partial/Misaligned] | [specifics] |
| License Tier Accuracy | [Aligned/Partial/Misaligned] | [specifics] |
| Deprecated Feature Avoidance | [Aligned/Partial/Misaligned] | [specifics] |
| Cross-Product Integration | [Aligned/Partial/Misaligned] | [specifics] |

## Changes Made

### Agent Files Enhanced
| Agent File | Changes Made | Rationale |
|------------|-------------|-----------|
| [filename] | [description] | [why] |

### New Agents Created
| Agent File | Domain | Keywords | Rationale |
|------------|--------|----------|-----------|
| [filename] | [area] | [keywords] | [why] |

### Routing Updates
| Change | Location | Details |
|--------|----------|---------|
| [type] | [SKILL.md section] | [what changed] |

## Metrics
- **Improvements Applied:** [count]
- **New Agents Created:** [count]
- **Routing Keywords Added:** [count]
- **Total Agent Count (Updated):** [new total]

## Next Implementation Recommendations
- [Recommendation 1]
- [Recommendation 2]
```

---

### STEP 6.5: Versioned Archival

After writing the markdown improvement log (Step 6), persist a structured JSON archive for programmatic access and historical trend analysis.

**Archive Location:**
```
[Instance Projects]/jarvis-improvements/
├── improvement-log-YYYY-MM-DDTHH-MM-SS.json   ← Timestamped archive
├── improvement-log-YYYY-MM-DDTHH-MM-SS.json   ← (one per implementation)
└── archive-index.json                          ← Running index of all archives
```

> Note: Archives are stored at the top level of Instance Projects (not per-instance) so they can be queried across all instances for trend analysis.

**Archive JSON Format:**
```json
{
  "archive_version": "1.0",
  "timestamp": "2026-02-13T14:30:00Z",
  "instance": "[instance name]",
  "project": "[project name]",
  "orchestrator_version": "10.0",
  "agents_activated": ["incident-agent", "change-agent", "..."],
  "agents_total": 84,
  "tasks_completed": 12,
  "errors_encountered": 1,
  "analysis": {
    "execution_quality": { "score": 4, "notes": "..." },
    "gap_detection": { "gaps_found": 1, "details": ["..."] },
    "pattern_recognition": { "patterns_found": 3, "details": ["..."] },
    "error_analysis": { "errors": 1, "preventable": true, "details": ["..."] },
    "efficiency_review": { "score": 4, "notes": "..." },
    "team_coordination": { "used": false },
    "mastery_alignment": {
      "best_practices": "aligned",
      "config_consistency": "aligned",
      "license_accuracy": "aligned",
      "deprecation_avoidance": "aligned",
      "cross_product_integration": "partial",
      "overall_score": 4.6
    }
  },
  "changes_made": {
    "agents_enhanced": [
      { "file": "incident-agent.md", "changes": "...", "rationale": "..." }
    ],
    "agents_created": [],
    "routing_updates": []
  },
  "mastery_validation": [
    {
      "agent": "incident-agent.md",
      "enhancements_proposed": 3,
      "enhancements_validated": 2,
      "enhancements_discarded": 1,
      "mastery_conflicts": ["..."],
      "mastery_extensions": ["..."],
      "novel_learnings": ["..."]
    }
  ],
  "metrics": {
    "improvements_applied": 5,
    "new_agents_created": 0,
    "routing_keywords_added": 0,
    "total_agent_count": 84
  },
  "recommendations": ["..."]
}
```

**Archive Index (`archive-index.json`) Format:**
```json
{
  "index_version": "1.0",
  "last_updated": "2026-02-13T14:30:00Z",
  "total_archives": 5,
  "archives": [
    {
      "file": "improvement-log-2026-02-13T14-30-00.json",
      "timestamp": "2026-02-13T14:30:00Z",
      "instance": "dev12345",
      "project": "ITSM Pro+ Demo",
      "improvements_applied": 5,
      "agents_created": 0,
      "mastery_alignment_score": 4.6
    }
  ],
  "cumulative_metrics": {
    "total_improvements_applied": 42,
    "total_agents_created": 3,
    "total_routing_keywords_added": 12,
    "average_mastery_alignment": 4.3,
    "implementations_analyzed": 5
  }
}
```

**Archival Steps:**
1. Read `~/.claude/servicenow-config.json` to get `instance_projects_path`
2. Create `jarvis-improvements/` directory if it doesn't exist: `mkdir -p [instance_projects_path]/jarvis-improvements/`
3. Generate the timestamped JSON archive file
4. Read existing `archive-index.json` (if it exists) or initialize a new one
5. Append the new archive entry to the index
6. Update `cumulative_metrics` with running totals

**Archival Safety:**
- Archives are append-only — never modify or delete existing archive files
- If `archive-index.json` is corrupted, rebuild it by scanning all `improvement-log-*.json` files in the directory
- Timestamp uses ISO 8601 format with hyphens replacing colons in filenames (filesystem-safe)

---

### STEP 6.7: Execution Replay & Lessons Learned

After archival, replay the implementation to generate structured "lessons learned" by comparing what Mastery recommended versus what was actually implemented. Feed divergences and insights back into `pattern-library.json`.

**Replay Process:**

#### 1. Reconstruct the Recommendation-vs-Implementation Map

For each product/feature configured during the implementation:

```
REPLAY ENTRY:
  Product: [product name]
  Mastery Doc: [path from mastery-index.json]
  Mastery Recommended:
    - Implementation Order: [what Mastery said to do first/second/third]
    - Configuration Approach: [OOB / basic / intermediate / advanced pattern from Mastery]
    - Prerequisites: [what Mastery listed as required before this product]
    - License Tier: [what license-intelligence.json says is needed]
  Actually Implemented:
    - Implementation Order: [what actually happened — from task execution log]
    - Configuration Approach: [what was actually configured]
    - Prerequisites Met: [yes/no — were prereqs done before this?]
    - License Tier Used: [what was assumed during implementation]
  Divergence: [none / minor / significant]
  Outcome: [success / partial / failed]
```

#### 2. Classify Divergences

For each divergence found, classify it:

| Classification | Meaning | Action |
|---------------|---------|--------|
| **Positive Divergence** | Implementation deviated from Mastery but produced a better outcome | Candidate for pattern-library.json addition |
| **Neutral Divergence** | Different approach, same outcome | Log for awareness, no action needed |
| **Negative Divergence** | Deviated from Mastery and caused issues | Append corrective guidance to agent file |
| **Mastery Gap** | Mastery had no guidance for this scenario | Flag for Mastery knowledge base update |

#### 3. Generate Lessons Learned

Produce a structured lessons-learned record:

```json
{
  "lessons_learned": [
    {
      "lesson_id": "LL-2026-02-13-001",
      "product": "incident-management",
      "mastery_doc": "03-technology-workflows/incident-management.md",
      "category": "positive_divergence",
      "summary": "Bulk incident creation via batch API 5x faster than individual creates",
      "mastery_said": "Create incidents using servicenow_create_record for each record",
      "we_did": "Used servicenow_batch_create_records for 20 incidents in one call",
      "outcome": "5x faster, no data quality issues",
      "recommendation": "Update Mastery doc and agent file with batch pattern for 10+ records",
      "pattern_library_candidate": true
    },
    {
      "lesson_id": "LL-2026-02-13-002",
      "product": "change-management",
      "mastery_doc": "03-technology-workflows/change-management.md",
      "category": "negative_divergence",
      "summary": "Skipped CAB approval workflow setup, caused change collisions",
      "mastery_said": "Configure CAB Workbench before enabling parallel change windows",
      "we_did": "Enabled parallel changes without CAB Workbench",
      "outcome": "Two changes scheduled on same CI at same time — conflict detected late",
      "recommendation": "Enforce Mastery prerequisite order in change-agent.md",
      "pattern_library_candidate": false
    }
  ]
}
```

#### 4. Feed Insights into pattern-library.json

For lessons classified as `positive_divergence` with `pattern_library_candidate: true`:

1. Read `~/.claude/skills/servicenow-architect-agent/references/pattern-library.json`
2. Check if a similar pattern already exists (match on product + description keywords)
3. If new: append the pattern to the appropriate domain section
4. If existing: increment the `confirmed_count` or add implementation reference

**Pattern Library Entry Format:**
```json
{
  "pattern_id": "PAT-[domain]-[sequential]",
  "product": "[product name]",
  "domain": "[domain folder]",
  "name": "[short pattern name]",
  "description": "[what to do and why]",
  "discovered": "2026-02-13",
  "confirmed_count": 1,
  "source_lessons": ["LL-2026-02-13-001"],
  "mastery_status": "extends_baseline",
  "agents_updated": ["incident-agent.md"]
}
```

#### 5. Feed Negative Divergences Back to Agents

For lessons classified as `negative_divergence`:

1. Read the relevant specialist agent file
2. Append to the agent's "Learned Improvements" section under "Known Issues & Workarounds"
3. Include the Mastery reference so future implementations follow the correct order

#### 6. Flag Mastery Gaps for Knowledge Base Updates

For lessons classified as `mastery_gap`:

1. Log to `{instance_projects_path}/jarvis-improvements/mastery-gaps.json`:
   ```json
   {
     "gaps": [
       {
         "gap_id": "MG-2026-02-13-001",
         "product": "[product]",
         "mastery_doc": "[path]",
         "missing_section": "[which section lacks coverage]",
         "description": "[what guidance is needed]",
         "discovered_during": "[project name]",
         "date": "2026-02-13"
       }
     ]
   }
   ```
2. These gaps can be used to prioritize future Mastery knowledge base documentation work

**Replay Safety:**
- Execution replay is read-only analysis — it does not re-execute any implementation steps
- Pattern library updates are append-only
- Mastery gap logs are append-only
- Agent file updates follow the same safety rules as Step 3 (append to "Learned Improvements" only)

---

### STEP 6.9: Performance Benchmarking

Collect and persist execution metrics for this implementation. Metrics are stored in a dedicated directory for cross-implementation trending and performance regression detection.

**Metrics Storage Location:**
```
[Instance Projects]/jarvis-metrics/
├── benchmark-YYYY-MM-DDTHH-MM-SS.json   ← Per-implementation metrics
├── benchmark-YYYY-MM-DDTHH-MM-SS.json   ← (one per implementation)
└── metrics-index.json                    ← Running index with trend data
```

> Note: Stored at Instance Projects root (alongside `jarvis-improvements/`) for cross-instance analysis.

#### 1. Collect Execution Metrics

Gather the following from the completed implementation:

```json
{
  "benchmark_version": "1.0",
  "timestamp": "2026-02-13T14:30:00Z",
  "instance": "[instance name]",
  "project": "[project name]",
  "orchestrator_version": "10.0",

  "dispatch_metrics": {
    "tasks_dispatched": 12,
    "tasks_completed": 11,
    "tasks_failed": 1,
    "tasks_retried": 2,
    "retry_rate": 0.167,
    "avg_task_completion_seconds": 45,
    "slowest_task": { "name": "Create 20 incidents", "seconds": 120 },
    "fastest_task": { "name": "Activate plugin", "seconds": 8 },
    "parallel_tasks_max": 4,
    "sequential_bottlenecks": ["SLA creation blocked by assignment rules"]
  },

  "agent_metrics": {
    "agents_activated": 5,
    "agents_total_available": 84,
    "agent_utilization_rate": 0.06,
    "agents_used": [
      { "agent": "incident-agent.md", "tasks_handled": 4, "success_rate": 1.0 },
      { "agent": "change-agent.md", "tasks_handled": 3, "success_rate": 0.67 }
    ]
  },

  "mcp_tool_metrics": {
    "total_mcp_calls": 87,
    "successful_calls": 82,
    "failed_calls": 5,
    "mcp_success_rate": 0.943,
    "calls_by_tool": {
      "servicenow_create_record": 45,
      "servicenow_query_table": 22,
      "servicenow_update_record": 12,
      "servicenow_batch_create_records": 3,
      "servicenow_execute_script": 5
    },
    "avg_call_latency_ms": 340,
    "retries_by_tool": {
      "servicenow_create_record": 2,
      "servicenow_execute_script": 1
    }
  },

  "mastery_metrics": {
    "mastery_docs_consulted": 6,
    "mastery_docs_available": 206,
    "mastery_lookup_rate": 0.029,
    "license_catches": 2,
    "license_catches_detail": [
      "Virtual Agent flagged as requiring ITSM Pro (user had Standard)",
      "Performance Analytics flagged as requiring Pro tier"
    ],
    "deprecation_warnings": 1,
    "deprecation_warnings_detail": [
      "Legacy Workflows reference detected — migration to Flow Designer recommended"
    ],
    "best_practice_validations_passed": 8,
    "best_practice_validations_failed": 1,
    "pattern_library_hits": 3
  },

  "quality_metrics": {
    "validation_checks_run": 15,
    "validation_checks_passed": 14,
    "validation_checks_failed": 1,
    "rollback_plans_generated": 3,
    "rollback_plans_executed": 0,
    "mastery_alignment_score": 4.6,
    "enhancements_proposed": 5,
    "enhancements_validated": 4,
    "enhancements_discarded": 1
  },

  "team_metrics": {
    "team_mode_used": false,
    "teammates_spawned": 0,
    "cross_domain_handoffs": 0,
    "leader_interventions": 0
  },

  "user_satisfaction": {
    "implementation_accepted": true,
    "user_modifications_after": 0,
    "rollback_requested": false,
    "notes": "[Any user feedback captured during Step 7 display]"
  }
}
```

#### 2. Calculate Derived Metrics

After collecting raw metrics, compute:

- **Overall Success Rate:** `tasks_completed / tasks_dispatched`
- **Efficiency Score:** `1 - (tasks_retried / tasks_dispatched)` (higher is better)
- **Mastery Coverage:** `mastery_docs_consulted / agents_activated` (ratio of agents with Mastery backing)
- **Safety Score:** `(license_catches + deprecation_warnings) / tasks_dispatched` (higher means more proactive catches)
- **MCP Reliability:** `mcp_success_rate` (target: > 0.95)

#### 3. Persist Benchmark File

1. Read `~/.claude/servicenow-config.json` to get `instance_projects_path`
2. Create `jarvis-metrics/` directory if it doesn't exist: `mkdir -p [instance_projects_path]/jarvis-metrics/`
3. Write the benchmark JSON file with timestamp in filename

#### 4. Update Metrics Index

Read or initialize `{instance_projects_path}/jarvis-metrics/metrics-index.json`:

```json
{
  "index_version": "1.0",
  "last_updated": "2026-02-13T14:30:00Z",
  "total_benchmarks": 5,
  "benchmarks": [
    {
      "file": "benchmark-2026-02-13T14-30-00.json",
      "timestamp": "2026-02-13T14:30:00Z",
      "instance": "dev12345",
      "project": "ITSM Pro+ Demo",
      "success_rate": 0.917,
      "mastery_alignment": 4.6,
      "mcp_reliability": 0.943
    }
  ],
  "trends": {
    "avg_success_rate": 0.94,
    "avg_mastery_alignment": 4.3,
    "avg_mcp_reliability": 0.96,
    "avg_retry_rate": 0.12,
    "total_license_catches": 8,
    "total_deprecation_warnings": 3,
    "total_mastery_docs_consulted": 42,
    "total_mcp_calls": 523,
    "implementations_tracked": 5
  },
  "regressions": [
    {
      "metric": "mcp_reliability",
      "current": 0.943,
      "average": 0.96,
      "delta": -0.017,
      "severity": "minor",
      "note": "Slight increase in MCP failures — check instance connectivity"
    }
  ]
}
```

#### 5. Detect Performance Regressions

Compare current benchmark against rolling averages in `metrics-index.json`:

| Metric | Regression Threshold | Severity |
|--------|---------------------|----------|
| `success_rate` | < avg - 0.10 | **critical** |
| `mcp_reliability` | < avg - 0.05 | **warning** |
| `retry_rate` | > avg + 0.15 | **warning** |
| `mastery_alignment` | < avg - 0.5 | **warning** |
| `avg_task_completion_seconds` | > avg * 2.0 | **minor** |

If regression detected:
- Log to `regressions` array in metrics-index.json
- Include regression details in Step 7 display summary
- For critical regressions: flag as "Review Recommended" in improvement log

**Benchmarking Safety:**
- Metrics collection is read-only — it does not modify implementation artifacts
- Benchmark files are append-only — never modify or delete existing benchmarks
- User satisfaction is captured from observable signals only (acceptance, modifications, rollback) — no intrusive prompts

---

### STEP 7: Display Summary to User

After all improvements are applied, display a summary:

```
===============================================================
JARVIS Self-Improvement Complete
===============================================================

Implementation Analyzed: [Project Name] on [Instance]

Improvements Applied:
  Agent files enhanced: [count]
  New agents created:   [count]
  Routing keywords added: [count]

New Agents Created:
  [For each: filename — domain — rationale]

Key Learnings:
  [Top 3 patterns or insights from this implementation]

Lessons Learned (Execution Replay):
  Divergences found:    [count] ([positive] positive, [neutral] neutral, [negative] negative)
  Patterns fed to library: [count]
  Mastery gaps flagged:    [count]

Performance Benchmark:
  Success rate:         [X]% ([completed]/[dispatched] tasks)
  MCP reliability:      [X]% ([successful]/[total] calls)
  Retry rate:           [X]%
  Mastery alignment:    [score]/5
  License catches:      [count]
  Deprecation warnings: [count]
  Regressions:          [count detected or "none"]

Full log saved to:
  [Instance Projects]/[instance]/improvements/[date]_improvement-log.md

Archive saved to:
  [Instance Projects]/jarvis-improvements/improvement-log-[timestamp].json
  [Instance Projects]/jarvis-metrics/benchmark-[timestamp].json
  (Implementation #[N] — cumulative: [total] improvements across [count] implementations)

Total Agent Count: [updated count]
===============================================================
```

---

## Safety Controls

### Before Modifying Any Agent File
1. Read the current file content
2. Verify the file exists and is a valid agent .md file
3. Only append to the "Learned Improvements" section — never modify existing content
4. If the file has no "Learned Improvements" section, create one at the end

### Before Creating New Agents
1. Verify no existing agent already covers the identified gap (search by keywords)
2. Use the established template structure (never create freeform agents)
3. New agents are logged as "Draft" status until validated in a future implementation
4. Each new agent must have a Rollback section

### General Safety
- All changes are logged with timestamps and rationale
- No destructive operations — only additions and appends
- Improvement logs provide full audit trail
- If uncertain about a change, flag it in the log as "Review Recommended" rather than applying it

---

## Improvement Categories

The system looks for and applies these types of improvements:

| Category | Description | Example |
|----------|-------------|---------|
| **New Patterns** | Implementation approaches discovered during execution | "Create SLA definitions before assignment rules for proper attachment" |
| **Default Configs** | Better default values for common configurations | "Set incident auto-close to 7 days instead of 3 for healthcare" |
| **Validation Checks** | Additional checks to add to agent validation sections | "Verify CMDB CI operational status before creating relationships" |
| **MCP Tool Usage** | New or better ways to use MCP tools | "Use batch_create_records for 10+ records instead of individual creates" |
| **Cross-Agent Coordination** | Improved handoff patterns between agents | "CMDB agent should pass CI sys_ids to Incident agent via execution context" |
| **Industry Refinements** | Industry-specific adaptations | "Healthcare incidents require PHI flag check before resolution" |
| **New Agent Coverage** | Entirely new domains needing dedicated agents | "No agent covers Workspace Experience — create one" |
| **Error Prevention** | Proactive checks to prevent known failure modes | "Check for duplicate category names before creating catalog categories" |
| **Mastery Alignment** | Corrections based on Mastery knowledge base validation | "Agent configured Legacy Workflows — should use Flow Designer per Mastery deprecation index" |
| **License Correction** | License tier mismatches caught by license-intelligence.json | "Virtual Agent requires ITSM Pro tier, not Standard — corrected agent guidance" |
| **Execution Replay** | Lessons from comparing Mastery guidance vs actual implementation | "Batch API divergence from Mastery proved 5x faster — added to pattern-library.json" |

---

## Integration with Orchestrator

### How This Skill Connects to the Workflow

```
Orchestrator Step 6: UAT Validation
         ↓
Orchestrator Step 7: Documentation Generation
         ↓
    ┌─────────────────────────────────────┐
    │  THIS SKILL ACTIVATES AUTOMATICALLY │
    │  (Phase 3: Self-Improvement)        │
    └─────────────────────────────────────┘
         ↓
    Step 1: Gather implementation context
         ↓
    Step 2: Analyze across 6+ dimensions (including Mastery alignment)
         ↓
    Step 3: Enhance existing agent files
         ↓
    Step 4: Gap analysis
         ↓
    Step 5: Create new sub-agents (if gaps found)
         ↓
    Step 6: Log all improvements
         ↓
    Step 6.5: Versioned archival (JSON)
         ↓
    Step 6.7: Execution replay & lessons learned
         ↓
    Step 6.9: Performance benchmarking
         ↓
    Step 7: Display summary to user
         ↓
    IMPLEMENTATION CYCLE COMPLETE
```

### Invocation by Orchestrator

The orchestrator should invoke this skill after Step 7 using:
```
Task tool with:
  subagent_type: "comprehensive-self-improvement"
  model: "opus"
  description: "Post-implementation self-improvement analysis"
  prompt: |
    Implementation just completed for [INSTANCE_NAME] / [PROJECT_NAME].

    Agents activated: [list]
    Tasks completed: [count]
    Errors encountered: [list or "none"]

    Run comprehensive self-improvement analysis.
    Instance Projects path: [path from config]
```

---

## Examples

### Example 1: Agent Enhancement
```
During an ITSM implementation, the incident-agent was used to create 20 incidents.
The system discovered that using mcp__servicenow__servicenow_batch_create_records
was 5x faster than individual creates for bulk data.

Improvement Applied:
  → Appended to incident-agent.md: "For bulk incident creation (10+), use
    servicenow_batch_create_records instead of individual servicenow_create_record calls."
```

### Example 2: New Agent Creation
```
During a healthcare demo, the orchestrator needed to configure Clinical Device
Management but no agent covered this area.

New Agent Created:
  → clinical-device-management-agent.md
  → Keywords: clinical device, medical equipment, biomedical, device lifecycle
  → Routing added to SKILL.md under Healthcare Industry section
```

### Example 3: Cross-Agent Coordination
```
The CMDB agent created CIs but the Incident agent couldn't reference them
because sys_ids weren't passed through the execution context.

Improvement Applied:
  → Updated inter-agent-coordination.md with new context passing pattern:
    "CMDB agent MUST store created CI sys_ids in execution context registry
     for downstream agents to reference."
```

---

## Continuous Learning Compound Effect

Over time, this system creates a **compounding knowledge base**:

```
Implementation 1: Base agent files
         ↓
Implementation 2: +5 improvements, +1 new agent
         ↓
Implementation 3: +8 improvements, +2 new agents (builds on #2's learnings)
         ↓
Implementation N: Agents become increasingly refined and comprehensive
```

Each implementation makes future implementations better because:
- Agent files contain more patterns and best practices
- New agents cover previously uncovered domains
- Error prevention checks catch issues earlier
- Routing keywords become more precise
- Cross-agent coordination improves

---

## Related Components

- **Main Orchestrator:** ServiceNow-Architect-Planner-v9 (triggers this skill)
- **Main Skill:** servicenow-architect-agent (routing logic — updated by this skill)
- **Agent References:** `~/.claude/skills/servicenow-architect-agent/references/` (enhanced by this skill)
- **Trusted Resources:** servicenow-trusted-resources (used for best practice validation)
- **Instance Projects:** Configured in `~/.claude/servicenow-config.json` (improvement logs stored here)
- **Mastery Knowledge Base:** Configured in `~/.claude/servicenow-config.json` → `mastery_path` (authoritative reference for dimension 2g)
- **Mastery Reference Files** (in `references/` alongside agent files):
  - `mastery-index.json` — Product-to-agent mapping, Mastery doc paths
  - `license-intelligence.json` — License tiers, prerequisites, add-ons
  - `zurich-deprecation-index.json` — Deprecated features and migration paths
  - `product-integration-graph.json` — Cross-product dependency graph

---

**Skill:** comprehensive-self-improvement
**Version:** 3.0
**Introduced in:** JARVIS v9.0 | **Updated:** v10.0 (Mastery alignment dimension)
**Model:** Opus (for strategic analysis)
**Trigger:** Automatic after Step 7
**Output:** Enhanced agents, new agents, improvement logs, Mastery alignment reports
