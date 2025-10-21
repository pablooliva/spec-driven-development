# Initialize Implementation Phase

IMPLEMENTATION PHASE INITIALIZATION

Starting implementation phase based on completed specification.

IMPORTANT: This command requires Claude Sonnet. Before proceeding, check your current model ID in the system information. If you are NOT running on a Claude Sonnet model (e.g., claude-sonnet-*), immediately:

  1. Warn the user: "WARNING: This command requires Claude Sonnet but you're currently using [model name]. Please switch to Sonnet and try again."
  2. STOP all further processing - do not execute any of the instructions below.

## Context Utilization Check

Before loading any documents, check current context usage:

```text
Current context utilization: [X]%

If > 35%: ⚠️ Warning - Context usage is high ([X]%). Consider:
  - Running essential tasks only
  - Using subagents for research tasks
  - Being prepared to run /sdd-implementation-compact soon

If > 40%: ⚠️ CRITICAL - Context usage is too high ([X]%).
  - You should run /sdd-implementation-compact before starting
  - Clear session and use /sdd-continue to resume with fresh context
```

Proceed with caution if context is above 35%.

## Initial Context Load

1. **Read Progress File:**
   - Load `SDD/prompts/context-management/progress.md` to understand planning completion status
   - Identify the specification document referenced
   - Note any important context from the planning phase

2. **Update Progress for Implementation Phase:**
   - Add a new implementation section to `SDD/prompts/context-management/progress.md`
   - IMPORTANT: Preserve all research and planning phase information - do NOT delete or reset it
   - Add reference to the PROMPT document being created
   - Document the transition from planning to implementation phase

## Implementation Setup

1. **Check for Existing PROMPT Documents:**
   - Search for any existing `SDD/prompts/PROMPT-[###]-*.md` files
   - If a PROMPT document with the same number already exists:

     ```text
     ⚠️ WARNING: PROMPT document already exists!

     Found: SDD/prompts/PROMPT-[###]-[existing-name].md

     Options:
     1. Continue with existing PROMPT document
     2. Create new PROMPT with different number
     3. Archive existing and create new (if previous implementation was abandoned)

     Please clarify how to proceed.
     ```

   - Only proceed to create new PROMPT if no duplicate exists or user explicitly approves

2. Create `SDD/prompts/PROMPT-[###]-[feature-name]-[YYYY-MM-DD].md` document where:
   - `[###]` matches the specification and research document numbers (e.g., if using SPEC-042, create PROMPT-042)
   - `[feature-name]` is a kebab-case description matching the spec document (e.g., "user-authentication", "csv-export")
   - `[YYYY-MM-DD]` is today's date
   - Full example: `PROMPT-042-user-authentication-2025-10-20.md`

## Prerequisite Verification

Before starting implementation:

1. **Locate Specification Document:**
   - Find the corresponding `SDD/requirements/SPEC-[###]-[feature-name].md` file
   - If multiple specs exist, ask user which one to implement
   - Verify the specification is complete (has all sections filled)

2. **Confirm Specification Completeness:**
   - Executive Summary: Complete with research foundation reference
   - Intent: Clear problem statement and solution approach
   - Success Criteria: All functional and non-functional requirements defined
   - Edge Cases: Research-backed scenarios with desired behaviors (EDGE-XXX)
   - Failure Scenarios: Graceful degradation strategies defined (FAIL-XXX)
   - Implementation Constraints: Context requirements and essential files listed
   - Validation Strategy: Test scenarios and acceptance criteria defined

3. **Validate Specification Quality:**
   - If any specification sections are missing or incomplete, warn the user
   - Check if `/sdd-planning-complete` was run (look for completion marker in progress.md)
   - If not complete, warn: "Specification phase may not be complete. Consider running /sdd-planning-complete first if needed."
   - Suggest reviewing the specification for completeness before implementation

## Implementation Document Structure

Create the implementation tracking document using this enhanced template:

```markdown
# PROMPT-[###]-[feature-name]: [Feature Description]

## Executive Summary

- **Based on Specification:** SPEC-[###]-[feature-name].md
- **Research Foundation:** RESEARCH-[###]-[feature-name].md
- **Start Date:** [YYYY-MM-DD]
- **Author:** Claude (with [user's name if known])
- **Status:** In Progress/Testing/Complete

## Specification Alignment

### Requirements Implementation Status
- [ ] REQ-001: [Requirement description] - Status: Not Started/In Progress/Complete
- [ ] REQ-002: [Requirement description] - Status: Not Started/In Progress/Complete
- [ ] PERF-001: [Performance requirement] - Status: Not Started/In Progress/Complete
- [ ] SEC-001: [Security requirement] - Status: Not Started/In Progress/Complete

### Edge Case Implementation
- [ ] EDGE-001: [Edge case name] - Implementation status
- [ ] EDGE-002: [Edge case name] - Implementation status

### Failure Scenario Handling
- [ ] FAIL-001: [Failure scenario] - Error handling implemented
- [ ] FAIL-002: [Failure scenario] - Error handling implemented

## Context Management

### Current Utilization
- Context Usage: [X]% (target: <40%)
- Essential Files Loaded:
  - [file path]:lines - [purpose]
  - [file path]:lines - [purpose]

### Files Delegated to Subagents
- [file path] - [research task delegated]
- [file path] - [research task delegated]

## Implementation Progress

### Completed Components
- [Component/Feature]: [Brief description and files modified]
- [Component/Feature]: [Brief description and files modified]

### In Progress
- **Current Focus:** [Specific component being implemented]
- **Files Being Modified:** [file paths with line ranges]
- **Next Steps:** [Immediate next actions]

### Blocked/Pending
- [Issue/Dependency]: [Description and resolution plan]

## Test Implementation

### Unit Tests
- [ ] [Test file]: Tests for [component/requirement]
- [ ] [Test file]: Tests for [edge case EDGE-XXX]

### Integration Tests
- [ ] [Test file]: Integration test for [feature flow]
- [ ] [Test file]: End-to-end test for [user scenario]

### Test Coverage
- Current Coverage: [X]%
- Target Coverage: [As specified in SPEC]
- Coverage Gaps: [Areas needing additional tests]

## Technical Decisions Log

### Architecture Decisions
- [Decision]: [Rationale based on specification constraints]
- [Decision]: [Trade-off analysis and choice made]

### Implementation Deviations
- [Deviation from spec]: [Reason and impact assessment]
- [Deviation from spec]: [Stakeholder approval needed/obtained]

## Performance Metrics

- [Metric from PERF-XXX]: Current: [value], Target: [value], Status: [Met/Not Met]
- [Metric from PERF-XXX]: Current: [value], Target: [value], Status: [Met/Not Met]

## Security Validation

- [ ] Authentication implemented per SEC-XXX requirements
- [ ] Input validation added for [specific inputs]
- [ ] Authorization checks in place for [specific operations]

## Documentation Created

- [ ] API documentation: [file path or N/A]
- [ ] User documentation: [file path or N/A]
- [ ] Configuration documentation: [file path or N/A]

## Session Notes

### Subagent Delegations
- [Timestamp]: Delegated [task] to [subagent type]
- [Timestamp]: Results: [summary of findings]

### Critical Discoveries
- [Discovery]: [Impact on implementation]
- [Discovery]: [Required specification adjustment]

### Next Session Priorities
1. [Specific task to complete next]
2. [Following priority]
3. [Subsequent priority]
```

## Implementation Process

1. **Load Specification Foundation:**
   - Read the complete SPEC-XXX document
   - Identify all requirements, edge cases, and failure scenarios
   - Note essential files and context constraints

2. **Set Up Development Environment:**
   - Load essential files identified in specification
   - Verify test framework is configured
   - Check for existing related code to build upon

3. **Begin Incremental Implementation:**
   - Start with core functionality (primary success path)
   - Implement one requirement at a time
   - Write tests alongside implementation
   - Validate against specification criteria continuously

4. **Track Progress Rigorously:**
   - Update PROMPT document after each component completion
   - Mark requirements as implemented in the tracking document
   - Document any deviations or discoveries immediately

## Context Management & Subagent Usage

### Context Target

- Maintain <40% context utilization during implementation
- Focus on implementation: Write code and tests based on specification (avoid re-researching or re-planning)
- Prepare for testing: Structure code for easy validation against spec criteria

### Available Subagents for Implementation Phase

Use these subagents (via Task tool) to preserve main context:

1. **Explore subagent** (`subagent_type=Explore`)
   - Use for: Finding implementation examples, locating test files, discovering utilities
   - Example: "Find all existing authentication implementations in this codebase"
   - When to use: When you need to understand existing patterns or find reusable components

2. **general-purpose subagent** (`subagent_type=general-purpose`)
   - Use for: Complex implementation research and analysis
   - Example tasks:
     - "Research how to implement [specific pattern] in [framework]"
     - "Analyze performance implications of [implementation approach]"
     - "Find and analyze similar features in this codebase for implementation patterns"
     - "Research testing strategies for [specific scenario]"
     - "Investigate error handling patterns used elsewhere in this project"
   - When to use: When you need implementation guidance or pattern analysis

### Subagent Delegation Strategy

- Delegate file discovery and pattern research to preserve context for coding
- Use parallel subagent calls when investigating independent implementation aspects
- Document subagent findings in the Session Notes section of PROMPT document

## Quality Checklist

During implementation, continuously verify:

- [ ] Each requirement from SPEC is being addressed
- [ ] Tests are written for each component/requirement
- [ ] Edge cases (EDGE-XXX) have specific handling code
- [ ] Failure scenarios (FAIL-XXX) have error handling
- [ ] Performance requirements (PERF-XXX) are being measured
- [ ] Security requirements (SEC-XXX) are implemented
- [ ] Code follows existing project patterns (discovered via subagents)
- [ ] Documentation is updated as needed

## Deliverable Expectations

A complete implementation must have:

- ✓ All specification requirements implemented and tested
- ✓ Complete PROMPT document tracking all progress
- ✓ All edge cases handled with tests
- ✓ All failure scenarios have graceful error handling
- ✓ Performance metrics meet specification targets
- ✓ Security requirements validated
- ✓ Test coverage meets project standards
- ✓ Documentation for any public APIs or configuration

## Implementation Workflow

### Phase Flow

```text
Load SPEC → Create PROMPT → Load Essential Files → Implement Requirements →
Write Tests → Validate Against Spec → Document Progress → Handle Edge Cases →
Measure Performance → Complete Implementation
```

### When Context Reaches ~40%

1. Run `/sdd-implementation-compact` to preserve progress
2. Clear session and start fresh
3. Run `/sdd-continue` to resume from compaction point

---

Begin implementation now using the specification as your authoritative guide. Create the `SDD/prompts/PROMPT-[###]-[feature-name]-[YYYY-MM-DD].md` document and start systematic implementation against specification criteria.
