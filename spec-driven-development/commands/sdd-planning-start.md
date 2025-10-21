# Initialize Planning/Specification Phase

SPECIFICATION PHASE INITIALIZATION

Starting planning phase based on completed research.

IMPORTANT: This command requires Claude Sonnet. Before proceeding, check your current model ID in the system information. If you are NOT running on a Claude Sonnet model (e.g., claude-sonnet-*), immediately:

  1. Warn the user: "WARNING: This command requires Claude Sonnet but you're currently using [model name]. Please switch to Sonnet and try again."
  2. STOP all further processing - do not execute any of the instructions below.

## Initial Context Load

1. **Read Progress File:**
   - Load `SDD/prompts/context-management/progress.md` to understand research completion status
   - Identify the research document referenced
   - Note any important context from the research phase

2. **Update Progress for Planning Phase:**
   - Add a new planning section to `SDD/prompts/context-management/progress.md`
   - IMPORTANT: Preserve all research phase information - do NOT delete or reset it
   - Add reference to the SPEC document being created
   - Document the transition from research to planning phase

## Specification Setup

1. Create `SDD/requirements/SPEC-[###]-[feature-name].md` document where:
   - `[###]` matches the research document number (e.g., if using RESEARCH-042, create SPEC-042)
   - `[feature-name]` is a kebab-case description matching the research document (e.g., "user-authentication", "csv-export")
   - Full example: `SPEC-042-user-authentication.md`

## Prerequisite Verification

Before creating specification:

1. **Locate Research Document:**
   - Find the corresponding `SDD/research/RESEARCH-[###]-[feature-name].md` file
   - If multiple research documents exist, ask user which one to base the specification on
   - Verify the research document is complete (has all sections filled)

2. **Confirm Research Completeness:**
   - System Data Flow: Documented with specific file:line references
   - Stakeholder Mental Models: All perspectives captured
   - Production Edge Cases: Historical issues analyzed
   - Files That Matter: Core logic and tests identified
   - Security Considerations: Auth/privacy/validation documented
   - Testing Strategy: Test scenarios outlined
   - Documentation Needs: Section identifying future docs requirements is complete

3. **Validate Research Quality:**
   - If any research sections are missing or incomplete, warn the user
   - Check if `/sdd-research-complete` was run (look for completion marker in progress.md)
   - If not complete, warn: "Research phase may not be complete. Consider running /sdd-research-complete first if needed."
   - Suggest running `/sdd-research-complete` first if research is unfinished

## Specification Document Structure

Create the specification using this enhanced template:

```markdown
# SPEC-[###]-[feature-name]

## Executive Summary

- **Based on Research:** RESEARCH-[###]-[feature-name].md
- **Creation Date:** [YYYY-MM-DD]
- **Author:** Claude (with [user's name if known])
- **Status:** Draft/In Review/Approved

## Research Foundation

### Production Issues Addressed
- Issue #[XXX]: [Brief description from research]
- Issue #[YYY]: [Brief description from research]

### Stakeholder Validation
- Product Team: [Key requirements from research]
- Engineering Team: [Technical constraints from research]
- Support Team: [Common pain points from research]

### System Integration Points
- [List key integration points identified in research with file:line references]

## Intent

### Problem Statement
[Clear statement of the problem being solved, based on research findings]

### Solution Approach
[High-level approach to solving the problem]

### Expected Outcomes
[What will be different after implementation]

## Success Criteria

### Functional Requirements
- REQ-001: [Specific, testable requirement]
- REQ-002: [Another specific requirement]
- REQ-003: [Include measurable criteria where possible]

### Non-Functional Requirements
- PERF-001: [Performance requirement with specific metrics]
- SEC-001: [Security requirement from research]
- UX-001: [User experience requirement]

## Edge Cases (Research-Backed)

### Known Production Scenarios
- EDGE-001: **[Scenario name]**
  - Research reference: [Section from RESEARCH-XXX]
  - Current behavior: [What happens now]
  - Desired behavior: [What should happen]
  - Test approach: [How to verify]

- EDGE-002: **[Another scenario]**
  - Research reference: [Section from RESEARCH-XXX]
  - Current behavior: [What happens now]
  - Desired behavior: [What should happen]
  - Test approach: [How to verify]

## Failure Scenarios

### Graceful Degradation
- FAIL-001: **[Failure type]**
  - Trigger condition: [What causes this failure]
  - Expected behavior: [How system should handle it]
  - User communication: [Error messages/feedback]
  - Recovery approach: [How to recover]

- FAIL-002: **[Another failure type]**
  - Trigger condition: [What causes this failure]
  - Expected behavior: [How system should handle it]
  - User communication: [Error messages/feedback]
  - Recovery approach: [How to recover]

## Implementation Constraints

### Context Requirements
- **Maximum context utilization:** <40% during implementation
- **Essential files for implementation:**
  - [file path]:lines [why needed]
  - [file path]:lines [why needed]
- **Files that can be delegated to subagents:**
  - [file path] - [research task that can be delegated]

### Technical Constraints
- [Constraints from research - framework limitations, API restrictions, etc.]
- [Performance requirements from stakeholders]
- [Security requirements from research]

## Validation Strategy

### Automated Testing
- Unit Tests:
  - [ ] [Specific test scenario from research]
  - [ ] [Another test scenario]
- Integration Tests:
  - [ ] [Integration point test]
  - [ ] [Another integration test]
- Edge Case Tests:
  - [ ] Test for EDGE-001
  - [ ] Test for EDGE-002

### Manual Verification
- [ ] [User flow to verify]
- [ ] [Admin functionality to check]
- [ ] [Error handling to validate]

### Performance Validation
- [ ] [Metric to measure with target value]
- [ ] [Another metric with benchmark]

### Stakeholder Sign-off
- [ ] Product Team review
- [ ] Engineering Team review
- [ ] Security Team review (if applicable)
- [ ] Legal/Compliance review (if applicable)

## Dependencies and Risks

### External Dependencies
- [API/Service dependencies from research]
- [Third-party library dependencies]

### Identified Risks
- RISK-001: [Risk description and mitigation plan]
- RISK-002: [Another risk and mitigation]

## Implementation Notes

### Suggested Approach
[High-level implementation strategy based on research]

### Areas for Subagent Delegation
[Specific research tasks that can be delegated during implementation]

### Critical Implementation Considerations
[Important technical details from research that must be considered]
```

## Planning Process

1. **Load Research Foundation:**
   - Read the complete RESEARCH-XXX document
   - Extract all findings, edge cases, and stakeholder inputs
   - Note specific file:line references for implementation

2. **Transform Research into Requirements:**
   - Convert research findings into specific, testable requirements
   - Ensure every edge case from research has a corresponding specification
   - Map stakeholder needs to success criteria

3. **Define Clear Validation:**
   - Create specific test scenarios for each requirement
   - Include performance benchmarks where applicable
   - Define acceptance criteria for stakeholder sign-off

4. **Plan for Implementation:**
   - Identify which files need to be loaded during implementation
   - Mark research tasks that can be delegated to subagents
   - Ensure context requirements stay under 40%

## Context Management & Subagent Usage

### Context Target

- Maintain <40% context utilization during specification creation
- Focus on transformation: Convert research into actionable specification (avoid re-researching)
- Prepare for review: Structure specification for easy stakeholder validation

### Available Subagents for Planning Phase

Use these subagents (via Task tool) to enhance planning:

1. **Explore subagent** (`subagent_type=Explore`)
   - Use for: Additional codebase investigation if research gaps are found
   - Example: Finding related configuration files or API contracts
   - When to use: If you need to verify integration points or find additional context

2. **general-purpose subagent** (`subagent_type=general-purpose`)
   - Use for: Researching best practices and architectural patterns
   - Example tasks:
     - "Research best practices for implementing [pattern] in [framework]"
     - "Analyze trade-offs between [approach A] and [approach B] for [use case]"
     - "Find similar implementations or patterns in the current codebase that match our requirements"
     - "Research how existing features in this codebase handle similar scenarios"
     - "Identify reusable components or patterns from this project for the new feature"
     - "Research security considerations for [feature type]"
   - When to use: When you need complex analysis, pattern research, or architectural guidance

### Subagent Delegation Strategy

- Delegate research-heavy tasks to preserve main context for specification writing
- Use parallel subagent calls when investigating multiple independent aspects
- Document subagent findings directly in the relevant specification sections

## Deliverable Expectations

A complete specification must have:

- ✓ All template sections filled with specific, actionable content
- ✓ Every research finding reflected in requirements or edge cases
- ✓ Clear, measurable success criteria
- ✓ Specific test scenarios for validation
- ✓ Implementation guidance with context management plan
- ✓ Risk assessment and mitigation strategies

## Quality Checklist

Before considering the specification complete:

- [ ] All research findings are incorporated
- [ ] Requirements are specific and testable
- [ ] Edge cases have clear expected behaviors
- [ ] Failure scenarios include recovery approaches
- [ ] Context requirements are documented
- [ ] Validation strategy covers all requirements
- [ ] Implementation notes provide clear guidance
- [ ] Best practices have been researched (via general-purpose subagent if needed)
- [ ] Architectural decisions are documented with rationale

---

Begin specification creation now using the research foundation. Create the `SDD/requirements/SPEC-[###]-[feature-name].md` document and systematically transform research into executable specification.
