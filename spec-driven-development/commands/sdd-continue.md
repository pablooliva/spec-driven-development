# Continue Session from Progress

CONTINUE FROM PREVIOUS SESSION

This command resumes your work after using a compaction command and clearing your session.

## When to Use This Command

You should run `/sdd-continue` when:

- ✅ You've run a compact command (/sdd-planning-compact, /sdd-research-compact, /sdd-implementation-compact)
- ✅ You've cleared your Claude Code session
- ✅ You're starting fresh and want to resume where you left off

This is the REQUIRED next step after any compaction.

## Workflow Overview

```text
PHASE START          CONTEXT ~40%           SAVE WORK          CLEAR SESSION
    │                     │                     │                   │
    ▼                     ▼                     ▼                   ▼
[/sdd-start] ──────► [/sdd-compact] ──────► [/sdd-commit] ──────► [/clear]
                          │                                          │
                          └── Creates ────────┐                      │
                              progress.md &   │                      │
                              compaction file │                      │
                                              │                      │
                                              ▼                      ▼
                                                                FRESH START
                                                                     │
                                                                     ▼
                                                               [/sdd-continue]
                                                                     │
                                              ┌──────────────────────┘
                                              │ Reads both files
                                              │ (progress.md &
                                              │  compaction file)
                                              ▼
                                         [/sdd-complete]
                                              │
                                              ▼
                                         [/sdd-commit]
```

This workflow represents the complete development cycle:

- **Start**: Begin with `/sdd-start` for any phase (research/planning/implementation)
- **Compact**: When context approaches 40%, use `/sdd-compact` to compress session
- **Commit**: Save your work with `/sdd-commit` before clearing the session
- **Continue**: Resume work with `/sdd-continue` in a fresh session
- **Complete**: Finalize the current phase with `/sdd-complete`
- **Commit**: Create final commits with `/sdd-commit`

## Process

### 1. Load Progress and Compaction Files

1. **Read Main Progress File:**
   - Load `SDD/prompts/context-management/progress.md`
   - Identify current phase (research/planning/implementation)
   - Note completion status and next priorities
   - Check for any subagent delegations that need follow-up

2. **Locate Most Recent Compaction File:**
   - Check `SDD/prompts/context-management/` for latest compaction file:
     - Research phase: `research-compacted-[YYYY-MM-DD_HH-MM-SS].md`
     - Planning phase: `planning-compacted-[YYYY-MM-DD_HH-MM-SS].md`
     - Implementation phase: `implementation-compacted-[YYYY-MM-DD_HH-MM-SS].md`
   - Load the most recent file based on timestamp (24-hour format with underscores)
   - Note: Files use format `YYYY-MM-DD_HH-MM-SS` (e.g., `2025-10-01_14-30-45`)

### 2. Verify Model Requirements

**IMPORTANT: Model verification must happen before any other processing.**

- **Research phase:** Requires Claude Opus (claude-opus-*)
- **Planning phase:** Requires Claude Sonnet (claude-sonnet-*)
- **Implementation phase:** Requires Claude Sonnet (claude-sonnet-*)

If incorrect model detected:

```text
WARNING: [Phase] phase requires [Required Model] but you're using [current model].
Please switch models and try again.
```

**STOP all further processing if model is incorrect.**

### 3. Pre-Continuation Quality Check

Before resuming work, verify from compaction file:

- [ ] All essential files are listed with specific line ranges
- [ ] Current focus section clearly identifies the exact task to resume
- [ ] Any blocking items or unresolved questions are documented
- [ ] Subagent delegations (if any) have been noted for follow-up
- [ ] Priority list provides clear next steps

If any critical information is missing, ask user for clarification before proceeding.

### 4. Phase-Specific Context Loading

#### For Research Phase Continuation

1. **Load Research Context:**
   - Research document: `SDD/research/RESEARCH-[###]-[feature-name].md`
   - Files from "Essential Files to Reload" section in compaction
   - Recent investigation areas from "Next Session Priorities"
   - Any pending subagent research tasks from "Subagent Delegations Performed"

2. **Verify Research State:**
   - Review "Research Progress" section (completed/in-progress/planned)
   - Check "Outstanding Research Questions" checklist
   - Identify current investigation focus
   - Note any "System Behavior Discovered" insights

3. **Resume Research:**
   - Continue with exact investigation from "Current Focus" section
   - Follow up on any incomplete subagent delegations
   - Use Explore subagent for file discovery when context is high
   - Document findings in research document

#### For Planning Phase Continuation

1. **Load Planning Context:**
   - Specification document: `SDD/requirements/SPEC-[###]-[feature-name].md:[lines]`
   - Research document: `SDD/research/RESEARCH-[###]-[feature-name].md:[sections]`
   - Files from "Essential Files to Reload" with specific line ranges
   - Review "Subagent Delegations Performed" for any pending follow-ups

2. **Verify Specification State:**
   - Review "Specification Progress" (completed sections vs remaining)
   - Check "Specification Quality Checklist" status
   - Identify exact section being worked on
   - Review "Implementation Readiness Assessment" if present

3. **Resume Planning:**
   - Continue with section from "Current Focus"
   - Apply "Research Foundation Applied" findings
   - Address items in "Planning Priorities" list
   - Complete any pending subagent research tasks

#### For Implementation Phase Continuation

1. **Load Implementation Context:**
   - Implementation prompt: `SDD/prompts/PROMPT-[###]-[feature-name]-[date].md`
   - Specification: `SDD/requirements/SPEC-[###]-[feature-name].md`
   - Files from "Essential Files to Reload"
   - Review any "Technical Decisions" or "Critical Learnings" from compaction

2. **Verify Implementation State:**
   - Review completed vs remaining implementation tasks
   - Check "Tests Status" section for test coverage
   - Identify current implementation focus
   - Review "Specification Validation Remaining" checklist

3. **Resume Implementation:**
   - Continue with task from "Current Focus"
   - Follow implementation priorities list
   - Address any "Edge case handling" or "Performance considerations" noted
   - Maintain <40% context utilization

### 5. Quality Verification Before Resuming

Complete this checklist before starting work:

- [ ] Correct model is active for current phase
- [ ] All essential files successfully loaded
- [ ] Understanding of current phase status is clear
- [ ] Next priority task is specifically identified
- [ ] Previous session's critical learnings are understood
- [ ] Blocking items or questions are noted
- [ ] Any subagent delegations from previous session are acknowledged

If any verification fails, ask user for clarification before proceeding.

### 6. Resume Work with Context Management

1. **Continue Work:**
   - Execute the specific next task identified
   - Update relevant phase document as you progress
   - Maintain continuity with previous session's approach
   - Follow up on any incomplete subagent tasks

2. **Monitor Context Usage:**
   - Check context utilization regularly
   - If approaching 40%, prepare for compaction
   - Warn user when compaction is needed:

     ```text
     Context utilization is approaching [X]%.
     Please save your work and run the appropriate compact command:
     - Research: /sdd-research-compact
     - Planning: /sdd-planning-compact
     - Implementation: /sdd-implementation-compact
     ```

3. **Update Progress File:**
   - Add new accomplishments to progress.md
   - Update "Next Session Priorities" section
   - Note any new blocking items discovered
   - Document any new subagent delegations
   - **IMPORTANT: DO NOT reset or delete previous phase information - append to it**

### 7. Subagent Delegation Strategy

When context is high during continuation, use subagents strategically:

#### Explore Subagent (`subagent_type=Explore`)

Use for quick, focused searches:

- Finding files by pattern
- Searching for code implementations
- Discovering similar patterns in codebase
- Locating configuration files

Example: "Find all authentication implementations in src/"

#### General-Purpose Subagent (`subagent_type=general-purpose`)

Use for complex analysis tasks:

- Researching best practices
- Analyzing complex architectural decisions
- Finding similar implementations in current codebase
- Investigating technical constraints
- Understanding multi-file interactions

Example: "Analyze how error handling works across the authentication flow"

### 8. Session Continuity Best Practices

To ensure smooth continuation:

1. **Preserve Context Learnings:**
   - Reread "Critical Learnings" section carefully
   - Apply previous discoveries to current work
   - Avoid re-researching already discovered information

2. **Maintain Phase Momentum:**
   - Stay focused on current phase objectives
   - Don't backtrack to previous phases unless critical
   - Trust the work documented in compaction files

3. **Document Incremental Progress:**
   - Update progress.md after each significant milestone
   - Note any new discoveries or blockers immediately
   - Keep "Next Session Priorities" current

## Important Notes

- The progress.md file is the primary continuation point across all phases
- Compaction files provide detailed context from previous sessions
- Each phase builds upon previous phases - maintain continuity
- Always verify you're using the correct model for the current phase
- If multiple compaction files exist, use the most recent one based on timestamp
- Never reset or overwrite previous phase information in progress.md

## Error Recovery

If continuation fails or context is unclear:

1. Check for most recent compaction file in `SDD/prompts/context-management/`
2. Verify progress.md exists and contains phase information
3. Ask user which phase to continue if ambiguous
4. Request specific guidance on next task if priorities are unclear

## Usage

Simply invoke this command after starting a fresh Claude Code session to resume from where you left off. The command will automatically detect your current phase and load the appropriate context.
