---
name: intelligent-model-router
description: |
  Autonomous intelligent model routing for complex tasks. Automatically analyzes
  task complexity, decomposes into planning (Opus) and execution (Sonnet/Haiku)
  phases, and provides optimal model selection per subtask. Invoked via /smartroute
  or /auto commands for automatic intelligent orchestration.
version: 1.0.0
model: opus
---

# 🎯 Intelligent Model Router - Auto Mode

```
╔═══════════════════════════════════════════════════════════════╗
║                                                               ║
║   INTELLIGENT MODEL ROUTER v1.0                               ║
║   ════════════════════════════════                            ║
║                                                               ║
║   Automatic model selection for optimal cost & performance   ║
║   Planning with Opus | Execution with Sonnet | Simple with Haiku║
║                                                               ║
╚═══════════════════════════════════════════════════════════════╝
```

## Purpose

This skill provides **autonomous, intelligent model routing** that:
- Analyzes task complexity automatically (0-15 scoring system)
- Enforces "Planning with Opus, Execution with Sonnet" pattern
- Uses Haiku for simple operations to optimize costs
- Decomposes complex workflows into clear phases
- Provides transparent execution plans before running
- Achieves 60-80% cost savings vs all-Opus approach

## Usage

Invoke via slash command:
```
/smartroute [your request]
/auto [your request]
```

Or Claude will automatically suggest this skill when detecting complex tasks (via CLAUDE.md instructions).

---

## IMPLEMENTATION INSTRUCTIONS

When this skill is invoked, follow these steps exactly:

### STEP 1: Analyze Task Complexity

Perform structured complexity analysis on the user's request.

#### 1.1: Keyword Detection

Scan the request for indicator keywords:

**Planning Indicators** (suggest Opus needed):
- "architecture", "design", "plan", "strategy", "approach"
- "how should", "what's the best way", "evaluate options"
- "system design", "data model", "integration strategy"
- "compare approaches", "recommend", "best practices"

**Execution Indicators** (suggest Sonnet):
- "implement", "build", "create", "write", "develop"
- "update", "modify", "fix", "refactor", "add"
- "generate", "construct", "code", "develop"

**Simple Operation Indicators** (suggest Haiku):
- "list", "read", "check", "find", "show", "get"
- "format", "display", "count", "validate"
- "search", "lookup", "retrieve", "fetch"

#### 1.2: Calculate Complexity Score

Use this algorithm to calculate complexity (0-15):

```
Complexity =
  (has_architecture_decision ? 5 : 0) +
  (num_integration_points × 2) +
  (num_dependencies × 1) +
  (requires_multi_domain_knowledge ? 4 : 0) +
  (has_approval_gates_needed ? 2 : 0) +
  (output_requires_synthesis ? 3 : 0)
```

**Examples**:

| Request | Architecture? | Integrations | Dependencies | Multi-domain? | Synthesis? | Score |
|---------|---------------|--------------|--------------|---------------|------------|-------|
| "List all .ts files" | No (0) | 0 | 0 | No (0) | No (0) | **1** |
| "Build REST API" | No (0) | 1 (×2=2) | 2 | No (0) | No (0) | **4** |
| "Design microservices arch" | Yes (5) | 3 (×2=6) | 5 | Yes (4) | Yes (3) | **23→15** |

**Score Interpretation**:
- **0-3**: Simple (Haiku candidate)
- **4-8**: Standard (Sonnet default)
- **9-12**: Complex (Opus planning, Sonnet execution)
- **13-15**: Highly complex (Opus throughout)

#### 1.3: Determine Phase Structure

Based on complexity score and keywords:

```
IF complexity >= 9 OR planning_keywords_detected:
  → REQUIRES: Planning Phase (Opus)
  → REQUIRES: Approval Gate

IF execution_keywords_detected OR implementation_needed:
  → REQUIRES: Execution Phase (model per subtask)

IF multiple_outputs OR synthesis_needed:
  → REQUIRES: Validation Phase (Opus if complex, Sonnet otherwise)
```

**Decision Matrix**:

| Complexity | Planning Phase | Execution Phase | Validation Phase |
|------------|----------------|-----------------|------------------|
| 0-3 | No | Direct execution (Haiku) | No |
| 4-8 | No | Direct execution (Sonnet) | Optional (Sonnet) |
| 9-12 | Yes (Opus) | Yes (mixed models) | Yes (Sonnet/Opus) |
| 13-15 | Yes (Opus) | Yes (mixed models) | Yes (Opus) |

---

### STEP 2: Decompose Into Phases

If complexity >= 9, create a multi-phase execution plan.

#### Phase 1: Planning (Opus)

**When**: Always required if complexity >= 9

**Model**: OPUS (always, non-negotiable)

**Subtasks**:
1. Analyze requirements and constraints
2. Design architecture/approach
3. Identify dependencies and integration points
4. Create detailed task manifest for execution phase
5. Define success criteria and validation checklist

**Output Format**:
```
PLANNING OUTPUTS (Opus)
═══════════════════════════════════════════════════════════════

ARCHITECTURE DECISIONS:
├─ [Decision 1]: Rationale and implications
├─ [Decision 2]: Rationale and implications
└─ [Decision 3]: Rationale and implications

TASK MANIFEST:
┌─────────────────────────────────────────────────────────┐
│ [S1] Task name                                          │
│     Type: [implementation/research/simple]              │
│     Model: [haiku/sonnet/opus]                         │
│     Complexity: [score]                                 │
│     Dependencies: [prerequisite tasks]                  │
│     Success Criteria: [specific validation criteria]    │
├─────────────────────────────────────────────────────────┤
│ [S2] Task name                                          │
│     ...                                                 │
└─────────────────────────────────────────────────────────┘

INTEGRATION POINTS:
├─ System A ↔ System B: [approach and protocol]
└─ Data flow: [description or diagram]

SUCCESS CRITERIA:
1. [Criterion 1 - specific and measurable]
2. [Criterion 2 - specific and measurable]
3. [Criterion 3 - specific and measurable]

═══════════════════════════════════════════════════════════════
```

#### Phase 2: Execution (Mixed Models)

**When**: Always required for implementation work

**Model**: Per-subtask based on individual complexity

**Subtask Processing**:

For each subtask identified in planning (or from original request):

1. **Assess subtask complexity** (0-15 score using same algorithm)
2. **Assign model**:
   - Score 0-3: Haiku
   - Score 4-8: Sonnet
   - Score 9+: Opus
3. **Set dependencies** (which tasks must complete first)
4. **Prepare handoff context** (what data does this subtask need)

**Parallel Lane Organization**:

Organize subtasks into parallel lanes based on dependencies:

```
Lane 1 (Foundation): Tasks with no dependencies
Lane 2 (Core): Tasks depending on Lane 1
Lane 3 (Integration): Tasks depending on Lane 2
Lane 4 (Polish): Final touches, documentation
```

**Output**: Implementation artifacts (code, configs, data, etc.)

#### Phase 3: Validation (Opus or Sonnet)

**When**: Required if multiple outputs need synthesis or complex validation

**Model Selection**:
- Use **Opus** if:
  - Synthesizing outputs from 3+ agents
  - Complex cross-domain validation needed
  - Architectural alignment check required
  - Validation complexity score > 8

- Use **Sonnet** if:
  - Simple single-domain validation
  - Straightforward success criteria check
  - Validation complexity score <= 8

**Subtasks**:
1. Validate each output against success criteria
2. Synthesize results into coherent deliverable
3. Identify gaps or issues
4. Generate summary report

**Output**: Validation report and final deliverables

---

### STEP 3: Assign Models to Subtasks

Use this decision matrix for each subtask:

#### Decision Tree

```
Is this a planning/architecture subtask?
├─ YES → OPUS (always, no exceptions)
└─ NO → Is this a synthesis/merge of complex outputs?
         ├─ YES (3+ sources or complexity > 8) → OPUS
         └─ NO → Calculate subtask complexity score (0-15)
                 ├─ Score 0-3 → HAIKU
                 │   Examples: Read file, format output, list items,
                 │             simple validation, data formatting,
                 │             file operations, basic lookups
                 │
                 ├─ Score 4-8 → SONNET (default for most work)
                 │   Examples: Code generation, API implementation,
                 │             research, analysis, standard refactoring,
                 │             component creation, testing
                 │
                 └─ Score 9+ → OPUS
                     Examples: Complex algorithm design, multi-system
                               integration, critical security logic,
                               novel architecture, optimization work
```

#### Model Selection Reference Table

| Task Type | Typical Complexity | Model | Cost (per 1M tokens) | Reasoning |
|-----------|-------------------|-------|---------------------|-----------|
| Architecture design | 10-15 | Opus | $15 | Strategic decisions |
| Planning & roadmap | 9-12 | Opus | $15 | Deep thinking required |
| Complex algorithm | 9-11 | Opus | $15 | Novel logic design |
| Multi-domain synthesis | 10-13 | Opus | $15 | Integration expertise |
| Standard code gen | 5-7 | Sonnet | $3 | Balanced quality/speed |
| API endpoint impl | 4-6 | Sonnet | $3 | Standard execution |
| Research & analysis | 5-8 | Sonnet | $3 | Good comprehension |
| Component creation | 4-7 | Sonnet | $3 | Standard development |
| File operations | 1-2 | Haiku | $0.25 | Simple, fast |
| Data formatting | 1-3 | Haiku | $0.25 | Mechanical task |
| List/read/check | 0-2 | Haiku | $0.25 | Basic lookup |
| Documentation formatting | 2-3 | Haiku | $0.25 | Simple writing |

#### Cost Optimization Check

After initial model assignments:

1. **Check for over-specification**:
   - Opus/Sonnet where Haiku would work
   - Multiple Opus tasks that could be combined

2. **Flag optimization opportunities**:
   ```
   OPTIMIZATION OPPORTUNITY:
   - Task [S5]: Format documentation
     Currently: Sonnet ($3/1M tokens)
     Suggested: Haiku ($0.25/1M tokens)
     Savings: ~$0.03 (90% reduction)
     Risk: None (simple formatting)
   ```

3. **Estimate cost savings**:
   - Calculate total with optimizations
   - Show savings vs current plan
   - Show savings vs all-Opus approach

---

### STEP 4: Display Execution Plan

Before executing, ALWAYS show the user a comprehensive execution plan.

#### Execution Plan Format

```
╔═══════════════════════════════════════════════════════════════╗
║  INTELLIGENT MODEL ROUTING - EXECUTION PLAN                   ║
╚═══════════════════════════════════════════════════════════════╝

REQUEST ANALYSIS
════════════════════════════════════════════════════════════════
├─ Complexity Score: [score]/15
├─ Planning Required: [YES/NO]
├─ Execution Strategy: [Direct / Multi-phase]
└─ Estimated Duration: [X] minutes

EXECUTION PHASES
════════════════════════════════════════════════════════════════

PHASE 1: PLANNING (Opus) [if required]
────────────────────────────────────────────────────────────────
├─ [P1] Analyze requirements and constraints
├─ [P2] Design architecture and approach
├─ [P3] Create detailed task manifest
└─ [P4] Define success criteria

    Model: opus
    Est. tokens: ~5,000
    Est. cost: ~$0.08
    Duration: ~2-3 minutes

⚠️  APPROVAL GATE: Will wait for your confirmation before Phase 2

PHASE 2: EXECUTION (Mixed Models - Parallel)
────────────────────────────────────────────────────────────────
│
├─ Lane 1: Foundation
│   ├─ [S1] Setup project structure
│   │   Model: haiku | Complexity: 2 | Cost: ~$0.01 | Deps: none
│   └─ [S2] Create shared utilities
│       Model: sonnet | Complexity: 5 | Cost: ~$0.05 | Deps: S1
│
├─ Lane 2: Core Implementation
│   ├─ [S3] Implement core business logic
│   │   Model: sonnet | Complexity: 6 | Cost: ~$0.06 | Deps: S2
│   ├─ [S4] Add error handling
│   │   Model: sonnet | Complexity: 5 | Cost: ~$0.04 | Deps: S3
│   └─ [S5] Integration layer (complex)
│       Model: opus | Complexity: 10 | Cost: ~$0.12 | Deps: S3
│
└─ Lane 3: Finalization
    ├─ [S6] Generate documentation
    │   Model: haiku | Complexity: 2 | Cost: ~$0.01 | Deps: S3,S4
    └─ [S7] Create example usage
        Model: haiku | Complexity: 3 | Cost: ~$0.01 | Deps: S3

PHASE 3: VALIDATION (Opus)
────────────────────────────────────────────────────────────────
└─ [V1] Validate outputs and synthesize results
    Model: opus | Complexity: 9 | Cost: ~$0.10 | Deps: all

COST ESTIMATE
════════════════════════════════════════════════════════════════
├─ Planning (Opus): $0.08
├─ Execution:
│   ├─ Opus tasks: 1 × ~$0.12 = $0.12
│   ├─ Sonnet tasks: 3 × ~$0.05 = $0.15
│   └─ Haiku tasks: 3 × ~$0.01 = $0.03
└─ Validation (Opus): $0.10

TOTAL ESTIMATED COST: ~$0.48

COMPARISON
────────────────────────────────────────────────────────────────
├─ All-Opus approach: ~$1.95
├─ All-Sonnet approach: ~$0.75
├─ Intelligent routing: ~$0.48
│
├─ Savings vs Opus: $1.47 (75% reduction)
└─ Savings vs Sonnet: $0.27 (36% reduction)

OPTIMIZATION OPPORTUNITIES
════════════════════════════════════════════════════════════════
├─ [S6] Documentation - Already using Haiku ✓
├─ [S7] Examples - Already using Haiku ✓
└─ No further optimizations recommended

════════════════════════════════════════════════════════════════
Proceed with execution? (yes/no/adjust)
════════════════════════════════════════════════════════════════
```

#### For Simple/Standard Tasks (No Planning)

If complexity < 9, show simplified plan:

```
╔═══════════════════════════════════════════════════════════════╗
║  INTELLIGENT MODEL ROUTING - DIRECT EXECUTION                 ║
╚═══════════════════════════════════════════════════════════════╝

REQUEST ANALYSIS
════════════════════════════════════════════════════════════════
├─ Complexity Score: [score]/15
├─ Planning Required: NO (straightforward task)
├─ Selected Model: [haiku/sonnet]
└─ Estimated Duration: [X] seconds

EXECUTION
────────────────────────────────────────────────────────────────
Single task execution with [model]:
- Direct implementation, no decomposition needed
- Est. cost: ~$[amount]

════════════════════════════════════════════════════════════════
Proceeding with execution...
════════════════════════════════════════════════════════════════
```

---

### STEP 5: Execute with Intelligent Routing

Execute the plan using Task tool with appropriate model parameter.

#### Phase 1: Planning (if required)

```python
# Launch Planning agent with Opus
Task({
  subagent_type: "Plan",
  model: "opus",  # HARDCODED - planning ALWAYS uses Opus
  description: "Strategic planning phase",
  prompt: `
You are the strategic planning agent for this workflow.

USER REQUEST:
${user_original_request}

YOUR TASK:
Provide comprehensive strategic planning including:

1. REQUIREMENTS ANALYSIS
   - Core requirements
   - Constraints and limitations
   - Edge cases to consider

2. ARCHITECTURE DECISIONS
   - Approach and rationale
   - Technology choices
   - Design patterns to use

3. TASK MANIFEST
   For each implementation subtask:
   - Task ID and clear name
   - Type (implementation/research/simple)
   - Recommended model (haiku/sonnet/opus)
   - Complexity score (0-15)
   - Dependencies (what must complete first)
   - Specific success criteria

4. INTEGRATION POINTS
   - How components connect
   - Data flow between parts
   - External integrations needed

5. SUCCESS CRITERIA
   - Specific, measurable outcomes
   - Validation checklist
   - Quality standards

Provide detailed, actionable guidance for the execution agents.
  `
})

# After planning completes, display results
# WAIT for user approval before Phase 2
```

#### APPROVAL GATE

After planning phase completes:

```
PLANNING PHASE COMPLETE ✓
═══════════════════════════════════════════════════════════════

PLANNING OUTPUTS (from Opus):
[Display the structured planning outputs]

EXECUTION PLAN READY:
- [N] subtasks identified
- [M] parallel lanes
- Mixed model usage: [breakdown]
- Estimated cost: $[amount]

═══════════════════════════════════════════════════════════════
Proceed with execution? (yes/no/adjust)
═══════════════════════════════════════════════════════════════
```

**User responses**:
- `yes` → Proceed to Phase 2
- `no` → Stop execution, ask what to change
- `adjust` → Use AskUserQuestion to get specific adjustments

#### Phase 2: Execution (parallel, mixed models)

Launch all subtasks with appropriate models and dependencies:

```python
# Example: Haiku task (simple operation)
Task({
  subagent_type: "general-purpose",
  model: "haiku",  # From model selection matrix
  description: "Setup project structure (S1)",
  prompt: `
PLANNING CONTEXT (from Opus planner):
${planning_outputs}

YOUR ASSIGNED TASK: [S1] Setup project structure

SPECIFIC INSTRUCTIONS:
- Create directory layout as specified in architecture
- Initialize configuration files
- Set up basic scaffolding

DEPENDENCIES: None (you can start immediately)

SUCCESS CRITERIA:
${success_criteria_from_planning}

IMPORTANT: You are using Haiku model (fast, cost-efficient) because
this is a simple, well-defined task. Execute efficiently.
  `
})

# Example: Sonnet task (standard implementation)
Task({
  subagent_type: "general-purpose",
  model: "sonnet",  # From model selection matrix
  description: "Implement core logic (S3)",
  prompt: `
PLANNING CONTEXT (from Opus planner):
${planning_outputs}

YOUR ASSIGNED TASK: [S3] Implement core business logic

SPECIFIC INSTRUCTIONS:
- Follow architecture decisions from planning
- Implement [specific features]
- Use patterns specified in planning

DEPENDENCIES:
- Wait for S2 (shared utilities) to complete
- Use outputs from S2 in your implementation

HANDOFF DATA FROM S2:
${s2_outputs}

SUCCESS CRITERIA:
${success_criteria_from_planning}

IMPORTANT: You are using Sonnet model (balanced quality/speed)
for standard implementation work. Focus on clean, working code.
  `
})

# Example: Opus task (complex subtask requiring strategic thinking)
Task({
  subagent_type: "general-purpose",
  model: "opus",  # Complex subtask requires Opus
  description: "Design integration layer (S5)",
  prompt: `
PLANNING CONTEXT (from Opus planner):
${planning_outputs}

YOUR ASSIGNED TASK: [S5] Design and implement integration layer

SPECIFIC INSTRUCTIONS:
- This requires architectural decisions
- Multiple integration patterns possible
- Must handle complex data transformations
- Critical for system reliability

DEPENDENCIES:
- Wait for S3 (core logic) to complete
- Use core interfaces from S3

HANDOFF DATA FROM S3:
${s3_outputs}

SUCCESS CRITERIA:
${success_criteria_from_planning}

IMPORTANT: You are using Opus model (maximum capability) because
this subtask requires strategic thinking and architectural decisions.
Make thoughtful choices and implement robustly.
  `
})

# Launch all tasks in parallel respecting dependencies
# Tasks with no dependencies start immediately
# Tasks with dependencies wait for prerequisites
```

#### Phase 3: Validation

After all execution tasks complete:

```python
# Determine validation model based on complexity
validation_model = (
  "opus" if validation_complexity_score > 8
  else "sonnet"
)

Task({
  subagent_type: "general-purpose",
  model: validation_model,
  description: "Validate and synthesize results",
  prompt: `
PLANNING OUTPUTS (original requirements):
${planning_outputs}

EXECUTION RESULTS (from all agents):
═══════════════════════════════════════════════════════════════

FROM [S1] Setup project structure (Haiku):
${s1_outputs}
Status: ✓ Complete

FROM [S2] Create shared utilities (Sonnet):
${s2_outputs}
Status: ✓ Complete

FROM [S3] Implement core logic (Sonnet):
${s3_outputs}
Status: ✓ Complete

[... all other results ...]

═══════════════════════════════════════════════════════════════

YOUR TASK:

1. VALIDATION
   - Check each output against success criteria from planning
   - Verify all requirements satisfied
   - Identify any gaps or issues

2. SYNTHESIS
   - Combine results into coherent deliverable
   - Ensure components integrate properly
   - Create unified final output

3. SUMMARY REPORT
   - What was accomplished
   - How it meets original requirements
   - Any notes or recommendations for user

4. QUALITY CHECK
   - Code quality (if applicable)
   - Completeness
   - Potential improvements

Provide a comprehensive validation report.
  `
})
```

---

### STEP 6: Context Handoff Protocol

Pass context between phases using structured format.

#### Planning → Execution Handoff

After planning phase completes, format outputs like this:

```
PLANNING OUTPUTS (Opus) - FOR EXECUTION AGENTS
═══════════════════════════════════════════════════════════════

ARCHITECTURE DECISIONS:
├─ [Decision 1]: Use REST API pattern
│   Rationale: Standard, well-supported, easy to test
│   Implications: Need authentication middleware, error handling
│
├─ [Decision 2]: PostgreSQL for persistence
│   Rationale: ACID compliance, strong community support
│   Implications: Need migration system, connection pooling
│
└─ [Decision 3]: Docker containerization
    Rationale: Consistent deployment, easy scaling
    Implications: Need Dockerfile, docker-compose config

TASK MANIFEST:
┌──────────────────────────────────────────────────────────────┐
│ [S1] Setup project structure                                 │
│     Type: simple                                              │
│     Model: haiku                                              │
│     Complexity: 2                                             │
│     Dependencies: none                                        │
│     Success Criteria:                                         │
│     - Directory structure created                             │
│     - Package.json initialized                                │
│     - Basic files in place                                    │
├──────────────────────────────────────────────────────────────┤
│ [S2] Implement REST API endpoints                            │
│     Type: implementation                                      │
│     Model: sonnet                                             │
│     Complexity: 6                                             │
│     Dependencies: S1                                          │
│     Success Criteria:                                         │
│     - All endpoints functional                                │
│     - Error handling in place                                 │
│     - Validation working                                      │
└──────────────────────────────────────────────────────────────┘

INTEGRATION POINTS:
├─ API → Database: Use connection pool, prepared statements
├─ API → Auth: JWT middleware on protected routes
└─ API → Client: JSON responses, proper HTTP status codes

SUCCESS CRITERIA:
1. All functional requirements implemented
2. Error handling comprehensive
3. Code follows architecture decisions
4. Tests pass (if applicable)
5. Documentation clear and complete

═══════════════════════════════════════════════════════════════
```

Pass this structured data to each execution agent in their prompt.

#### Execution → Validation Handoff

After execution tasks complete, collect outputs:

```
EXECUTION RESULTS - FOR VALIDATION AGENT
═══════════════════════════════════════════════════════════════

TASK: [S1] Setup project structure
AGENT: Haiku
STATUS: ✓ Complete
ARTIFACTS:
├─ Files created:
│   ├─ /project/src/
│   ├─ /project/tests/
│   ├─ /project/docs/
│   └─ package.json
├─ Configuration:
│   ├─ ESLint configured
│   ├─ TypeScript configured
│   └─ Jest test runner ready
└─ Notes: Basic structure ready for development

TASK: [S2] Implement REST API endpoints
AGENT: Sonnet
STATUS: ✓ Complete
ARTIFACTS:
├─ Endpoints created:
│   ├─ GET /api/users (list users)
│   ├─ POST /api/users (create user)
│   ├─ GET /api/users/:id (get user)
│   └─ PUT /api/users/:id (update user)
├─ Features implemented:
│   ├─ Input validation with Joi
│   ├─ Error handling middleware
│   ├─ JWT authentication
│   └─ Database integration
├─ Files modified:
│   ├─ src/routes/users.ts (new)
│   ├─ src/middleware/auth.ts (new)
│   └─ src/middleware/errors.ts (new)
└─ Notes: All endpoints tested manually, working as expected

[... additional task results ...]

SUMMARY:
├─ Total tasks: 5
├─ Completed: 5
├─ Failed: 0
└─ All success criteria met: ✓

═══════════════════════════════════════════════════════════════
```

Pass this to validation agent for final synthesis.

---

### STEP 7: Task Progress Tracking

Use TaskCreate and TaskUpdate for visible progress.

#### Creating Task List

At start of execution (after showing plan and getting approval):

```python
# Planning phase
if planning_required:
    TaskCreate({
      subject: "[PLANNING] Strategic analysis and design",
      description: "Opus model analyzing requirements and creating detailed execution plan",
      activeForm: "Planning with Opus"
    })

# Execution phase tasks
for each subtask in execution_plan:
    TaskCreate({
      subject: f"[{subtask.id}] {subtask.name}",
      description: f"{subtask.description} (Model: {subtask.model}, Complexity: {subtask.complexity})",
      activeForm: f"{subtask.active_form_verb}"
    })

# Validation phase
if validation_required:
    TaskCreate({
      subject: "[VALIDATION] Synthesize and validate results",
      description: f"Final validation and synthesis (Model: {validation_model})",
      activeForm: "Validating results"
    })
```

#### Updating Task Status

As work progresses:

```python
# When starting a task
TaskUpdate({
  taskId: task_id,
  status: "in_progress"
})

# When task completes successfully
TaskUpdate({
  taskId: task_id,
  status: "completed"
})

# If task fails or needs retry
TaskUpdate({
  taskId: task_id,
  description: f"{original_description} [RETRY with {upgraded_model}]",
  status: "in_progress"
})
```

This provides real-time visibility into execution progress.

---

## Error Handling & Model Fallback Strategy

### Scenario 1: Haiku Task Too Complex

**Detection**: Task fails with complexity indicators or poor output quality

**Action**:
1. Log the failure: "Task [S#] failed with Haiku - complexity underestimated"
2. Automatic retry with Sonnet
3. Update cost estimate
4. Notify user: "⚠️ Task [S#] upgraded to Sonnet for better handling (+$0.03 estimated)"

**Implementation**:
```python
if haiku_task_failed_due_to_complexity:
    user_message = f"""
⚠️ MODEL UPGRADE REQUIRED

Task: [{task_id}] {task_name}
Original model: Haiku (complexity {original_score})
Issue: Task more complex than initially assessed

Action: Automatically retrying with Sonnet
Cost adjustment: +$0.03 (marginal increase)

Proceeding with upgrade...
"""
    display_message(user_message)
    retry_with_model("sonnet")
```

### Scenario 2: Sonnet Task Struggles

**Detection**: Validation phase flags quality issues or incomplete implementation

**Action**:
1. Identify the problematic subtask
2. Offer to re-run with Opus
3. Show cost delta
4. Get user approval
5. If approved, re-run and integrate new results

**Implementation**:
```python
if validation_finds_quality_issues_in_subtask:
    user_question = f"""
⚠️ QUALITY IMPROVEMENT OPPORTUNITY

Task: [{task_id}] {task_name}
Current model: Sonnet
Issue: {issue_description}

Recommendation: Re-run with Opus for higher quality
- Cost delta: +$0.15
- Estimated improvement: Significant
- Risk: None (only improves quality)

Proceed with Opus upgrade? (yes/no)
"""

    if user_approves:
        rerun_with_opus()
        merge_into_final_results()
```

### Scenario 3: Planning Phase Needs Clarification

**Detection**: Planning agent indicates ambiguity or missing information

**Action**:
1. Pause planning
2. Use AskUserQuestion with structured options
3. Get clarification
4. Resume planning with additional context

**Implementation**:
```python
if planning_needs_clarification:
    # Use AskUserQuestion tool for structured input
    AskUserQuestion({
      questions: [{
        question: "Which approach should we use for authentication?",
        header: "Auth Method",
        multiSelect: false,
        options: [
          {
            label: "JWT tokens",
            description: "Stateless, scales well, standard approach"
          },
          {
            label: "Session cookies",
            description: "Stateful, simpler, better for traditional apps"
          },
          {
            label: "OAuth 2.0",
            description: "Third-party auth, most flexible"
          }
        ]
      }]
    })

    # Resume planning with user's choice
    continue_planning_with_clarification()
```

### Scenario 4: Never Downgrade From Opus

**Hard Rule**: Once a task is assigned Opus, NEVER downgrade to Sonnet/Haiku

**Reasoning**:
- If we determined Opus was needed, the task is inherently complex
- Downgrading risks quality and correctness
- Cost savings from downgrade are not worth the risk

**Exception**: Only if user explicitly requests downgrade after seeing costs

---

## Integration with Existing Features

### 1. OpusPlan Mode

Your `settings.local.json` has `"model": "opusplan"`:
- OpusPlan: Opus for /plan mode, Sonnet otherwise (conversation-level)
- Smart Router: Adds per-task granularity and Haiku optimization

**They work together**:
- OpusPlan provides the baseline
- Smart Router adds intelligence within that baseline
- No conflicts - complementary systems

### 2. Swarm Skill

**When to delegate**: If execution phase has 5+ parallel tasks

**Pattern**:
```python
if len(execution_tasks) >= 5:
    # Delegate to Swarm with model hints
    Task({
      subagent_type: "general-purpose",
      model: "sonnet",  # Swarm coordination uses Sonnet
      description: "Invoke swarm for parallel execution",
      prompt: f"""
Use /swarm to parallelize these tasks:

MODEL ASSIGNMENTS (enforce these in swarm):
{for task in tasks:}
- {task.id}: {task.assigned_model} (complexity {task.complexity})

TASK DETAILS:
{task_details}

IMPORTANT: Respect the model assignments above. They've been
carefully calculated based on task complexity.
      """
    })
```

### 3. JARVIS (ServiceNow Architect)

**Detection**: Keywords like "ServiceNow", "ITSM", "CMDB", "Now Assist"

**Pattern**:
```python
if detect_servicenow_task():
    # Delegate entirely to JARVIS
    display_message("""
ServiceNow task detected - delegating to JARVIS orchestrator.

JARVIS (ServiceNow-Architect-Planner-v8) will handle this with:
- Pre-flight checks and instance scanning
- Best practices research
- 129 specialist agents
- Two-phase workflow (planning approval → parallel execution)
- Full ServiceNow MCP integration

Launching JARVIS...
    """)

    Task({
      subagent_type: "ServiceNow-Architect-Planner-v8",
      model: "opus",  # JARVIS always uses Opus for orchestration
      description: "ServiceNow implementation via JARVIS",
      prompt: user_request
    })

    # Smart router's job is done - JARVIS takes over completely
    exit_smartroute()
```

---

## User Experience Examples

### Example 1: Simple Task (Direct Haiku)

**Input**: `/smartroute List all TypeScript files in src/`

**Output**:
```
╔═══════════════════════════════════════════════════════════════╗
║  INTELLIGENT MODEL ROUTING - DIRECT EXECUTION                 ║
╚═══════════════════════════════════════════════════════════════╝

REQUEST ANALYSIS
════════════════════════════════════════════════════════════════
├─ Complexity Score: 1/15 (simple file operation)
├─ Planning Required: NO
├─ Selected Model: Haiku (optimal for simple lookups)
└─ Estimated Cost: ~$0.001

Executing with Haiku...
════════════════════════════════════════════════════════════════

[Haiku execution result: file list]

✓ Complete in 2 seconds | Cost: $0.001 | Model: Haiku
```

### Example 2: Standard Task (Direct Sonnet)

**Input**: `/smartroute Create a REST API endpoint for user login with JWT`

**Output**:
```
╔═══════════════════════════════════════════════════════════════╗
║  INTELLIGENT MODEL ROUTING - DIRECT EXECUTION                 ║
╚═══════════════════════════════════════════════════════════════╝

REQUEST ANALYSIS
════════════════════════════════════════════════════════════════
├─ Complexity Score: 6/15 (standard implementation)
├─ Planning Required: NO (straightforward task)
├─ Selected Model: Sonnet (balanced quality/speed)
└─ Estimated Cost: ~$0.06

Executing with Sonnet...
════════════════════════════════════════════════════════════════

[Sonnet execution: creates endpoint with JWT auth]

✓ Complete in 45 seconds | Cost: $0.06 | Model: Sonnet
```

### Example 3: Complex Task (Full Orchestration)

**Input**: `/smartroute Design and build a distributed rate limiting system with Redis`

**Output**: [Full execution plan as shown in STEP 4, with all phases]

Result: Complete multi-phase orchestration with Opus planning, mixed execution, and validation.

---

## Configuration

Optional configuration file: `/Users/zachary.zoretich/.claude/skills/intelligent-model-router/config.json`

```json
{
  "model_selection": {
    "planning_model": "opus",
    "execution_model_default": "sonnet",
    "simple_threshold": 3,
    "complex_threshold": 9,
    "allow_user_override": true
  },
  "execution": {
    "auto_approve_simple": false,
    "show_cost_estimates": true,
    "parallel_execution": true,
    "max_parallel_width": 5
  },
  "optimization": {
    "suggest_cost_savings": true,
    "min_savings_to_suggest": 0.05
  },
  "integrations": {
    "delegate_to_swarm": true,
    "delegate_to_jarvis": true,
    "swarm_threshold": 5
  }
}
```

---

## Success Metrics

Track these metrics to measure effectiveness:

1. **Cost Efficiency**: Actual cost vs all-Opus baseline
   - Target: 60-80% savings

2. **Quality Maintenance**: Task retry rate
   - Target: <5% (model too weak)

3. **Time Efficiency**: Parallel execution effectiveness
   - Target: 50-70% time reduction vs serial

4. **Model Accuracy**: Correct model selection rate
   - Target: >90% no retry needed

5. **User Satisfaction**: Explicit feedback
   - Target: Prefer smart routing over manual

---

## Command Aliases

This skill can be invoked with:
- `/smartroute` (primary)
- `/auto` (shorthand)

Both trigger the same intelligent routing logic.

---

## Notes for Implementation

**Critical Success Factors**:

1. ✅ Always use Opus for planning - non-negotiable
2. ✅ Always show execution plan before running
3. ✅ Always respect user approval gates
4. ✅ Always pass context between phases
5. ✅ Always track progress with TaskCreate/TaskUpdate
6. ✅ Always show cost estimates transparently
7. ✅ Never downgrade from Opus once assigned
8. ✅ Always offer fallback if lower model struggles

**Integration Priority**:
1. OpusPlan mode (complement, not replace)
2. JARVIS delegation (ServiceNow tasks)
3. Swarm delegation (large parallel workloads)

**Cost Optimization**:
- Use Haiku aggressively for simple tasks
- Use Sonnet as default execution model
- Reserve Opus for planning and complex subtasks
- Show savings to user transparently
