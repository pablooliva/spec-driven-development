# Planning Phase Completion

PLANNING PHASE COMPLETION

Specification creation is complete and ready for implementation.

## 1. Verify Specification Document Completeness

Confirm that `SDD/requirements/SPEC-[###]-[feature-name].md` contains all required sections with complete information:

### Executive Summary

- [ ] Research foundation reference included `SDD/research/RESEARCH-[###]-[feature-name].md`
- [ ] Creation date and author documented
- [ ] Status marked as "In Review" or "Approved"

### Research Foundation

- [ ] Production issues from research listed with issue numbers
- [ ] Stakeholder validation summarized from all teams
- [ ] System integration points identified with file:line references

### Intent

- [ ] Clear problem statement derived from research
- [ ] Solution approach defined with rationale
- [ ] Expected outcomes specified and measurable

### Success Criteria

- [ ] Functional requirements (REQ-XXX) specific and testable
- [ ] Non-functional requirements (PERF-XXX, SEC-XXX, UX-XXX) with metrics
- [ ] All requirements traceable to research findings
- [ ] Each requirement has clear acceptance criteria

### Edge Cases (Research-Backed)

- [ ] All EDGE-XXX cases documented with research references
- [ ] Current behavior clearly described
- [ ] Desired behavior specified
- [ ] Test approach defined for each edge case
- [ ] Production scenarios from research all covered

### Failure Scenarios

- [ ] All FAIL-XXX scenarios documented
- [ ] Trigger conditions clearly identified
- [ ] Expected system behavior specified
- [ ] User communication/error messages defined
- [ ] Recovery approaches documented

### Implementation Constraints

- [ ] Context requirements specified (<40% target)
- [ ] Essential files for implementation listed with reasons
- [ ] Files suitable for subagent delegation identified
- [ ] Technical constraints from research documented

### Validation Strategy

- [ ] Unit test scenarios specified
- [ ] Integration test points identified
- [ ] Edge case test coverage defined
- [ ] Performance validation metrics specified
- [ ] Manual verification steps documented

### Dependencies and Risks

- [ ] External dependencies identified
- [ ] Risk assessment completed (RISK-XXX items)
- [ ] Mitigation strategies defined for each risk

### Implementation Notes

- [ ] Suggested implementation approach provided
- [ ] Areas for subagent delegation marked
- [ ] Critical implementation considerations from research included

## 2. Stakeholder Alignment Verification

Confirm stakeholder reviews and approvals:

### Review Checklist

- [ ] Product Team review completed
  - Requirements aligned with product vision
  - User experience considerations addressed
  - Success criteria approved

- [ ] Engineering Team review completed
  - Technical feasibility confirmed
  - Architecture approach validated
  - Performance requirements achievable

- [ ] Security Team review (if applicable)
  - Security requirements adequate
  - Data privacy considerations addressed
  - Authentication/authorization approach approved

- [ ] Legal/Compliance review (if applicable)
  - Regulatory requirements met
  - Data handling compliant
  - Terms of service considerations addressed

### Feedback Integration

Document any stakeholder feedback received and how it was addressed:

- Product feedback: [What was raised and how addressed]
- Engineering feedback: [Technical concerns and resolutions]
- Security feedback: [Security considerations and mitigations]

## 3. Implementation Readiness Assessment

Evaluate specification readiness for implementation phase:

### Ready for Implementation

- [ ] All required specification sections complete
- [ ] Success criteria clearly defined and measurable
- [ ] Edge cases have expected behaviors specified
- [ ] Failure scenarios include recovery approaches
- [ ] Test scenarios cover all requirements

### Implementation Guidance Clear

- [ ] Context management plan documented (<40% utilization)
- [ ] Essential files identified with line ranges
- [ ] Subagent delegation opportunities marked
- [ ] Implementation approach provides clear direction

### Blocking Items Resolved

- [ ] All "must have" requirements specified
- [ ] Critical technical decisions made
- [ ] External dependencies identified and understood
- [ ] Risk mitigation strategies defined

## 4. Quality Verification

Final quality check before completion:

### Specification Quality

- [ ] All research findings incorporated into specification
- [ ] Requirements are specific, measurable, achievable, relevant, time-bound (SMART)
- [ ] Edge cases cover all production scenarios from research
- [ ] Failure modes include graceful degradation strategies
- [ ] Testing strategy comprehensive and executable

### Traceability

- [ ] Every requirement traces back to research findings
- [ ] All stakeholder needs addressed in specification
- [ ] Production issues from research have corresponding solutions
- [ ] Edge cases mapped to historical incidents

### Completeness

- [ ] No placeholder text or TODOs remaining
- [ ] All sections have substantive content
- [ ] Cross-references between sections are accurate
- [ ] File path references include specific line numbers where helpful

## 5. Update Progress File for Phase Transition

Update `SDD/prompts/context-management/progress.md` with planning completion and implementation handoff:

```markdown
## Planning Phase - COMPLETE

### Specification Finalized
- Document: `SDD/requirements/SPEC-[###]-[feature-name].md`
- Completion timestamp: [YYYY-MM-DD HH:MM:SS]
- Stakeholder approvals: [List teams that approved]
- Implementation ready: YES

### Key Decisions Made
- [Major architectural decision]
- [Technology choice with rationale]
- [Trade-off decision made]

### Research Foundation Applied
- Production issues addressed: [Count]
- Edge cases specified: [Count]
- Test scenarios defined: [Count]

## Implementation Phase - READY TO START

### Implementation Priorities
1. [First component/feature to implement]
2. [Second priority]
3. [Third priority]

### Critical Implementation Notes
- [Key technical decision from spec]
- [Important constraint to remember]
- [Subagent delegation opportunity]

### Context Management Strategy
- Target utilization: <40%
- Essential files: [List with line ranges]
- Delegatable research: [Tasks for subagents]

### Known Risks for Implementation
- [RISK-001 with mitigation approach]
- [RISK-002 with mitigation approach]

### Next Steps
Planning phase complete. Ready for /sdd-implementation-start.
Specification provides comprehensive implementation guidance.
```

## 6. Final Checklist Before Completion

Before marking the planning phase as complete:

- [ ] Specification document fully populated (no TODOs or placeholders)
- [ ] All stakeholder reviews completed or explicitly waived
- [ ] Implementation readiness verified
- [ ] Progress file updated with transition information
- [ ] Quality verification passed
- [ ] Implementation priorities clearly defined

## Context Management Reminders

If context is becoming high during completion:

### Delegate to Subagents

Use these subagents (via Task tool) as needed:

1. **Explore subagent** (`subagent_type=Explore`)
   - Use for: Finding additional files or patterns
   - Example: Verifying integration points or configuration files
   - When to use: If you need to locate specific files referenced in the specification

2. **General-purpose subagent** (`subagent_type=general-purpose`)
   - Use for: Researching best practices or architectural patterns
   - Example tasks:
     - "Research industry standards for [pattern] implementation"
     - "Find similar implementations in the codebase"
     - "Analyze security considerations for [feature type]"
   - When to use: When you need to validate architectural decisions or research alternatives

### What Must Stay in Main Context

- Core specification decisions
- Stakeholder feedback and approvals
- Critical implementation guidance
- Risk assessments

## Phase Transition

Planning phase is now COMPLETE.

The specification in `SDD/requirements/SPEC-[###]-[feature-name].md` provides comprehensive guidance for implementation.

Next Claude Code session should:

1. Start fresh with Claude Sonnet
2. Run `/sdd-implementation-start` to begin coding
3. Reference the specification for all implementation decisions

---

Phase Status: FINISHED ✓
Next Command: `/sdd-implementation-start`
