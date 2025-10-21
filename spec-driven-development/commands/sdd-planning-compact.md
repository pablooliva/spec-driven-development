# Planning Progress Compaction

PLANNING PROGRESS COMPACTION

Context is getting overloaded during specification creation. Create permanent compaction record to preserve your work while freeing up context.

## Process

### 1. Create Timestamped Compaction File

Write to: `SDD/prompts/context-management/planning-compacted-[YYYY-MM-DD_HH-MM-SS].md` where:

- `[YYYY-MM-DD_HH-MM-SS]` is the current timestamp (24-hour time)
- Example: `planning-compacted-2025-10-01_14-30-45.md`

### 2. Document Structure

Use the following template:

```markdown
# Planning Compaction - [Feature Name] - [Date/Time]

## Session Context

- Compaction trigger: [context %] utilization
- Specification focus: [which part of SPEC-[###] we're working on]
- Research foundation: RESEARCH-[###]-[feature-name].md
- Session duration: [approximate time/interactions]

## Recent Specification Work
[List specific specification sections/documents modified with file:line references where relevant]
- Requirements defined: [brief description of requirements added]
- Edge cases specified: [number of EDGE-XXX cases documented]
- Success criteria established: [areas covered]
- Validation strategy: [testing approach defined]

**Avoid large content blocks** - use file:line references instead

## Specification Progress

### Completed Sections
- Intent statements: [specific sections completed]
- Success criteria: [REQ-XXX items fully defined]
- Edge cases: [EDGE-XXX cases documented]
- Failure scenarios: [FAIL-XXX scenarios specified]
- Validation strategy: [test scenarios defined]

### In Progress
- Current section: [exact section being worked on]
- Completion status: [percentage or description]
- Blocking items: [what's preventing completion]

### Remaining Work
- [ ] [Specification section not yet started]
- [ ] [Stakeholder validation needed]
- [ ] [Edge case analysis required]
- [ ] [Success criteria to define]
- [ ] [Test scenarios to specify]

## Research Foundation Applied

### Production Issues Addressed
- Issue #[XXX]: [How it's being addressed in spec]
- Issue #[YYY]: [How it's being addressed in spec]

### Stakeholder Requirements Incorporated
- Product Team: [Requirements reflected in spec]
- Engineering Team: [Technical constraints applied]
- Support Team: [Pain points being resolved]

### Edge Cases from Research
- EDGE-001: [Based on research finding about...]
- EDGE-002: [Based on production scenario...]
- EDGE-003: [Based on stakeholder feedback...]

## Critical Learnings
[Important discoveries made during planning - research insights applied, constraint discoveries, stakeholder feedback]
- Research insights applied: [How research findings shaped specification]
- Technical constraints discovered: [New limitations found during spec writing]
- Stakeholder clarifications: [Key feedback that changed approach]
- Implementation considerations: [Technical details that affect the spec]

## Critical References
[Essential documents/files needed to continue]
- Research document: SDD/research/RESEARCH-[###]-[feature-name].md
- Specification in progress: SDD/requirements/SPEC-[###]-[feature-name].md:[lines]
- Related architecture docs: [path if applicable]
- Integration contracts: [API specs, interfaces if relevant]

## Subagent Delegations Performed
[Document any subagent research done during planning]
- Explore subagent: [What was searched/found]
- General-purpose subagent: [Complex analysis performed]
- Results integrated: [How findings affected spec]

## Next Session Priorities

**Essential Files to Reload:**
- SDD/requirements/SPEC-[###]-[feature-name].md:[specific line ranges]
- SDD/research/RESEARCH-[###]-[feature-name].md:[sections needed]
- [Any other critical files with line ranges]

**Current Focus:**
- Exact specification section being developed: [specific section name]
- Open questions requiring resolution: [list any blockers]
- Stakeholder feedback needed on: [specific areas]

**Planning Priorities:**
1. [Immediate: Complete current section - specify exactly what]
2. [Next: Following section/validation task]
3. [Then: Subsequent specification work]

**Specification Quality Checklist:**
- [ ] All research findings incorporated into requirements
- [ ] Edge cases have clear expected behaviors defined
- [ ] Success criteria are measurable and specific
- [ ] Failure scenarios include recovery approaches
- [ ] Validation strategy covers all requirements
- [ ] Implementation constraints documented (<40% context)
- [ ] Stakeholder requirements reflected accurately

## Implementation Readiness Assessment

### Ready for Implementation
- [Sections complete enough for coding to begin]

### Blocking Implementation
- [Sections that must be completed before coding]

### Can Be Refined During Implementation
- [Sections that can be iteratively improved]

## Other Notes
[Any additional context, unresolved questions, important considerations for continuation]
- Alternative approaches considered: [Options evaluated but not chosen]
- Deferred decisions: [Items postponed for later resolution]
- Dependencies identified: [External factors affecting the spec]
```

## 🔄 WORKFLOW CHECKPOINT - CRITICAL NEXT STEPS

You've just created a compaction file to preserve your work. Now you MUST:

### Step 1: SAVE YOUR WORK

✅ Compaction file created: `planning-compacted-[timestamp].md`
✅ Progress file updated: `SDD/prompts/context-management/progress.md`

### Step 2: CLEAR THIS SESSION (Required)

Choose one:

- Close Claude Code completely, OR
- Start a new conversation (Cmd/Ctrl + K → "New Chat")

### Step 3: START FRESH AND CONTINUE

1. Open a new Claude Code session
2. Run `/sdd-continue` immediately
3. Your work will resume exactly where you left off

⚠️ **Why this matters:** Your context is nearly full. Continuing without clearing would lead to:

- Degraded performance
- Potential context overflow errors
- Loss of work if context limit is hit

This workflow ensures you maintain a clean <40% context throughout your work.

## Workflow Overview

```text
PHASE START          CONTEXT ~40%         CLEAR SESSION       FRESH START
    │                     │                     │                  │
    ▼                     ▼                     ▼                  ▼
[/sdd-start] ──────► [/sdd-compact] ──────► [Close] ──────► [/sdd-continue]
                          │                                        │
                          └── Creates ──────────────────────────► Reads
                              progress.md &                       both files
                              compaction file
```

### 3. Update Current Progress

Also update `SDD/prompts/context-management/progress.md` with:

- Latest specification state (sections completed vs remaining)
- Key decisions made during this session
- Next session continuation point
- Reference to this compaction file
- DO NOT reset previous phase information - add to it

## Guidelines

- **Be thorough but concise** - capture key specification decisions without overwhelming context
- **Avoid excessive content blocks** - prefer file:line references over large specification excerpts
- **Include precise references** - enable quick reload of research and spec documents
- **Document insights** - preserve critical learnings from research and stakeholder feedback
- **Mark clear status** - distinguish completed vs. in-progress vs. planned sections
- **Track research foundation** - show how research findings are being applied to the spec
- **Note subagent usage** - document delegated research to avoid repetition

## Context Management During Planning

### Subagent Usage Reminder

When context is high, consider delegating to subagents:

1. **Explore subagent** (`subagent_type=Explore`)
   - Finding related configuration files
   - Locating API contracts or interfaces
   - Discovering similar patterns in codebase

2. **general-purpose subagent** (`subagent_type=general-purpose`)
   - Researching best practices for specific patterns
   - Analyzing architectural trade-offs
   - Finding similar implementations in current codebase
   - Researching security considerations

### What to Preserve vs. Delegate

**Must Preserve in Main Context:**

- Core specification decisions
- Critical research findings being applied
- Stakeholder requirements and feedback
- Key technical constraints

**Can Delegate to Subagents:**

- Searching for code patterns
- Researching best practices
- Finding configuration examples
- Exploring edge implementations

## Next Steps After Compaction

After this compaction is complete:

1. **Clear the current session** - Close Claude Code or start a new conversation
2. **Start a fresh Claude Code session** with Claude Sonnet
3. **Run `/sdd-continue`** to resume from where you left off
4. The continue command will reload your progress from `progress.md` and the compaction file

Planning phase continues - use `/sdd-planning-complete` command when specification is finished and ready for stakeholder review.

## Quality Verification

Before compacting, ensure:

- [ ] All template sections above have meaningful content
- [ ] File references include specific line numbers where helpful
- [ ] Progress accurately reflects current state
- [ ] Critical learnings are captured
- [ ] Next priorities are clearly defined
- [ ] Research foundation tracking is complete

## ✅ Compaction Complete

Your work has been saved. You MUST now:

1. Close this Claude Code session
2. Start fresh
3. Run `/sdd-continue` to resume

DO NOT continue working in this session - context is too high!
