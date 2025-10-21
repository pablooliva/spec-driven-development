# Implementation Phase Completion

IMPLEMENTATION PHASE COMPLETION

Finalize implementation phase and prepare for deployment.

IMPORTANT: This command requires Claude Sonnet. Before proceeding, check your current model ID in the system information. If you are NOT running on a Claude Sonnet model (e.g., claude-sonnet-*), immediately:

  1. Warn the user: "WARNING: This command requires Claude Sonnet but you're currently using [model name]. Please switch to Sonnet and try again."
  2. STOP all further processing - do not execute any of the instructions below.

## Early Context Utilization Check

Before loading documents for completion verification:

```text
Current context utilization: [X]%

If > 35%: ⚠️ Warning - Context usage is high ([X]%).
  - Consider running /sdd-implementation-compact first
  - This will preserve your progress and free up context
  - Then use /sdd-continue to resume with fresh context

If > 40%: ⚠️ CRITICAL - Context too high for completion process ([X]%).
  - MUST run /sdd-implementation-compact before continuing
  - Completion process requires loading multiple documents for validation
  - Clear session and use /sdd-continue after compaction
```

Note: The completion process requires loading specification, PROMPT document, and creating summary documents, which needs available context.

## Workflow Position

```text
[/sdd-implementation-start] ──────► [/sdd-implementation-compact] ──────► [/sdd-continue]
         │                                      │                                │
         ▼                                      ▼                                ▼
   Create PROMPT-###                    Save progress &                   Resume work
                                       clear session
                                                                               │
                                          ┌────────────────────────────────────┘
                                          │
                                          ▼
                                 [/sdd-implementation-complete] ◄── YOU ARE HERE
                                          │
                                          ▼
                                   Validate all requirements
                                   Create summary documents
                                   Update specifications
                                          │
                                          ▼
                                   [/sdd-commit] ──────► DEPLOYMENT READY
```

## Initial Document Loading and Verification

### 1. Load Core Documents

**IMPORTANT: Load these documents BEFORE proceeding with any completion tasks.**

1. **Progress File:**
   - Load `SDD/prompts/context-management/progress.md`
   - Verify implementation phase is active
   - Check for any incomplete items or blockers
   - Note any recent compaction files referenced

2. **PROMPT Document:**
   - Load `SDD/prompts/PROMPT-[###]-[feature-name]-[date].md`
   - This is your PRIMARY verification source
   - Check "Status" field (should be "In Progress" or "Testing")
   - Review all requirement implementation statuses

3. **Specification Document:**
   - Load `SDD/requirements/SPEC-[###]-[feature-name].md`
   - Compare requirements against PROMPT document status
   - Verify all REQ-XXX, PERF-XXX, SEC-XXX, UX-XXX items

4. **Recent Compaction (if exists):**
   - Check for `SDD/prompts/context-management/implementation-compacted-*.md`
   - Load most recent file to understand any pending items
   - Review "Specification Validation Remaining" section

### 2. Pre-Completion Verification

**STOP and verify these conditions from the loaded documents:**

```text
COMPLETION READINESS CHECKLIST
────────────────────────────────────────────────────────────
□ All REQ-XXX requirements show "Complete" in PROMPT document
□ All PERF-XXX performance requirements show "Met" with metrics
□ All SEC-XXX security requirements show "Validated"
□ All UX-XXX user experience requirements show "Satisfied"
□ All EDGE-XXX edge cases show "Complete" implementation
□ All FAIL-XXX failure scenarios show error handling "Implemented"
□ Test coverage meets or exceeds target from specification
□ No "Blocked/Pending" items remain in PROMPT document
□ All subagent delegations have been completed and documented
────────────────────────────────────────────────────────────
```

If ANY items are not complete:

```text
⚠️ WARNING: Implementation is NOT ready for completion!

The following items are incomplete:
- [List specific incomplete items with their IDs]
- [Include which document shows the incomplete status]

Required Actions:
1. Complete remaining implementation tasks
2. Update PROMPT document with completion status
3. Verify all tests are passing
4. Then retry this completion command

Consider using /sdd-continue to resume implementation work.
```

**STOP processing if verification fails.**

## Completion Process

### 1. Finalize PROMPT Document

Update `SDD/prompts/PROMPT-[###]-[feature-name]-[date].md`:

#### Update Header Section

```markdown
## Executive Summary

- **Based on Specification:** SPEC-[###]-[feature-name].md
- **Research Foundation:** RESEARCH-[###]-[feature-name].md
- **Start Date:** [Original date]
- **Completion Date:** [YYYY-MM-DD]
- **Implementation Duration:** [X days]
- **Author:** Claude (with [user's name if known])
- **Status:** Complete ✓
- **Final Context Utilization:** [X]% (maintained <40% target)
```

#### Add Completion Summary

```markdown
## Implementation Completion Summary

### What Was Built
[2-3 paragraph summary of the implemented feature, focusing on:
- Core functionality delivered
- How it meets the specification intent
- Key architectural decisions made]

### Requirements Validation
All requirements from SPEC-[###] have been implemented and tested:
- Functional Requirements: [X/X] Complete
- Performance Requirements: [X/X] Met
- Security Requirements: [X/X] Validated
- User Experience Requirements: [X/X] Satisfied

### Test Coverage Achieved
- Unit Test Coverage: [X]% (Target was [Y]%)
- Integration Test Coverage: [X]%
- Edge Case Coverage: [X/X] scenarios tested
- Failure Scenario Coverage: [X/X] scenarios handled

### Subagent Utilization Summary
Total subagent delegations: [X]
- Explore subagent: [X] tasks (file discovery, pattern search)
- General-purpose subagent: [X] tasks (complex analysis, research)
[Note any particularly valuable subagent contributions]
```

### 2. Update Specification Document

Add implementation results to `SDD/requirements/SPEC-[###]-[feature-name].md`:

```markdown
## Implementation Summary

### Completion Details
- **Completed:** [YYYY-MM-DD]
- **Implementation Duration:** [X days]
- **Final PROMPT Document:** SDD/prompts/PROMPT-[###]-[feature-name]-[date].md
- **Implementation Summary:** SDD/prompts/implementation-complete/IMPLEMENTATION-SUMMARY-[###]-[YYYY-MM-DD_HH-MM-SS].md

### Requirements Validation Results
Based on PROMPT document verification:
- ✓ All functional requirements: Complete
- ✓ All non-functional requirements: Complete
- ✓ All edge cases: Handled
- ✓ All failure scenarios: Implemented

### Performance Results
[Pull from PROMPT document's Performance Metrics section]
- PERF-001: Achieved [value] ms (Target: [value] ms) ✓
- PERF-002: Achieved [value] req/s (Target: [value] req/s) ✓

### Implementation Insights
[From PROMPT document's Critical Discoveries section]
1. [Key architectural pattern that worked well]
2. [Performance optimization discovered]
3. [Testing approach that was effective]

### Deviations from Original Specification
[From PROMPT document's Implementation Deviations section]
- [Any approved changes with rationale]
- [Trade-offs made and why]
```

### 3. Create Implementation Summary Document

Save to `SDD/prompts/implementation-complete/IMPLEMENTATION-SUMMARY-[###]-[YYYY-MM-DD_HH-MM-SS].md`:

Format: `IMPLEMENTATION-SUMMARY-[###]-YYYY-MM-DD_HH-MM-SS.md` (24-hour format with underscores)
Example: `IMPLEMENTATION-SUMMARY-042-2025-10-21_14-30-45.md`

```markdown
# Implementation Summary: [Feature Name]

## Feature Overview
- **Specification:** SDD/requirements/SPEC-[###]-[feature-name].md
- **Research Foundation:** SDD/research/RESEARCH-[###]-[feature-name].md
- **Implementation Tracking:** SDD/prompts/PROMPT-[###]-[feature-name]-[date].md
- **Completion Date:** [YYYY-MM-DD HH:MM:SS]
- **Context Management:** Maintained <40% throughout implementation

## Requirements Completion Matrix

### Functional Requirements
| ID | Requirement | Status | Validation Method |
|----|------------|---------|------------------|
| REQ-001 | [Description] | ✓ Complete | Unit tests in [file] |
| REQ-002 | [Description] | ✓ Complete | Integration test [file] |

### Performance Requirements
| ID | Requirement | Target | Achieved | Status |
|----|------------|--------|----------|---------|
| PERF-001 | [Description] | [value] | [value] | ✓ Met |
| PERF-002 | [Description] | [value] | [value] | ✓ Met |

### Security Requirements
| ID | Requirement | Implementation | Validation |
|----|------------|---------------|------------|
| SEC-001 | [Description] | [How implemented] | [How tested] |

## Implementation Artifacts

### New Files Created

```text
[path/to/file1.ext] - [Primary purpose]
[path/to/file2.ext] - [Primary purpose]
```

### Modified Files

```text
[path/to/file.ext]:lines [start-end] - [What was changed]
[path/to/file.ext]:lines [start-end] - [What was changed]
```

### Test Files

```text
[path/to/test1.test.ext] - Tests [component/requirement]
[path/to/test2.test.ext] - Tests [edge cases EDGE-XXX]
```

## Technical Implementation Details

### Architecture Decisions
[From PROMPT document's Technical Decisions Log]
1. **[Decision]:** [Rationale and impact]
2. **[Pattern Used]:** [Why chosen over alternatives]

### Key Algorithms/Approaches
- [Algorithm/approach]: [Where used and why]

### Dependencies Added
- [package/library]: [version] - [purpose]

## Subagent Delegation Summary

### Total Delegations: [X]

#### Explore Subagent Tasks
1. [Timestamp]: Found [what] - Result: [outcome]
2. [Timestamp]: Searched for [pattern] - Result: [findings]

#### General-Purpose Subagent Tasks
1. [Timestamp]: Researched [topic] - Applied: [how used]
2. [Timestamp]: Analyzed [component] - Insight: [discovery]

### Most Valuable Delegations
- [Which delegation provided most value and why]

## Quality Metrics

### Test Coverage
- Unit Tests: [X]% coverage ([Y] tests)
- Integration Tests: [X]% coverage ([Y] tests)
- Edge Cases: [X]/[Y] scenarios covered
- Failure Scenarios: [X]/[Y] handled

### Code Quality
- Linting: [Pass/Fail with issues if any]
- Type Safety: [Coverage if applicable]
- Documentation: [Status]

## Deployment Readiness

### Environment Requirements

- Environment Variables:

  ```text
  [VAR_NAME_1]: [purpose]
  [VAR_NAME_2]: [purpose]
  ```

- Configuration Files:

  ```text
  [config.file]: [required settings]
  ```

### Database Changes
- Migrations: [list or "None"]
- Schema Updates: [list or "None"]

### API Changes
- New Endpoints: [list with methods]
- Modified Endpoints: [list with changes]
- Deprecated: [list or "None"]

## Monitoring & Observability

### Key Metrics to Track
1. [Metric]: Expected range [value]
2. [Metric]: Alert threshold [value]

### Logging Added
- [Component]: [What is logged]

### Error Tracking
- [Error scenario]: [How it's tracked]

## Rollback Plan

### Rollback Triggers
- [Condition that would trigger rollback]

### Rollback Steps
1. [Specific step]
2. [Specific step]

### Feature Flags
- [Flag name]: Controls [what]

## Lessons Learned

### What Worked Well
1. [Approach/pattern that was effective]
2. [Tool/technique that helped]

### Challenges Overcome
1. [Challenge]: [Solution applied]
2. [Challenge]: [Solution applied]

### Recommendations for Future
- [Recommendation based on this implementation]
- [Pattern to reuse or avoid]

## Next Steps

### Immediate Actions
1. Deploy to staging environment
2. Run smoke tests
3. Monitor initial metrics

### Production Deployment
- Target Date: [If known]
- Deployment Window: [If planned]
- Stakeholder Sign-off: [Required from whom]

### Post-Deployment
- Monitor [specific metrics]
- Validate [specific behaviors]
- Gather user feedback on [specific aspects]
```

### 4. Update Progress File

Update `SDD/prompts/context-management/progress.md`:

```markdown
## Implementation Phase - COMPLETE ✓

### Feature: [Feature Name]
- **Specification:** SDD/requirements/SPEC-[###]-[feature-name].md
- **Implementation:** SDD/prompts/PROMPT-[###]-[feature-name]-[date].md
- **Summary:** SDD/prompts/implementation-complete/IMPLEMENTATION-SUMMARY-[###]-[timestamp].md
- **Completion:** [YYYY-MM-DD HH:MM:SS]

### Final Status
- All requirements: ✓ Implemented
- All tests: ✓ Passing
- Performance targets: ✓ Met
- Security requirements: ✓ Validated
- Documentation: ✓ Complete

### Subagent Utilization
- Total delegations: [X]
- Context saved through delegation: ~[Y]%
- Most valuable delegation type: [Explore/General-purpose]

### Implementation Metrics
- Duration: [X] days
- Context management: Maintained <40% throughout
- Test coverage achieved: [X]%
- Files modified: [X]
- New files created: [Y]

### Deployment Readiness
✓ Feature is specification-validated and production-ready
✓ All acceptance criteria met
✓ Rollback plan documented
✓ Monitoring configured

### Next Steps
- Ready for staging deployment
- Production deployment checklist available
- Post-deployment validation plan ready

---

## Phase Transition

Implementation phase COMPLETE for [Feature Name].

To start next feature:
- Research new feature: `/sdd-research-start`
- Plan another feature: `/sdd-planning-start` (if research exists)
- Implement another feature: `/sdd-implementation-start` (if spec exists)
```

## Error Recovery

### If Completion Cannot Proceed

When requirements are not met:

1. **Document Blockers:**
   ```markdown
   ## Incomplete Items Blocking Completion
   - [REQ-XXX]: [What's missing]
   - [EDGE-XXX]: [What needs handling]
   - [Test Coverage]: [Current]% needs to reach [Target]%
   ```

2. **Save Progress:**
   - Run `/sdd-implementation-compact` to save current state
   - Clear session if context is high
   - Use `/sdd-continue` to resume implementation

3. **Address Blockers:**
   - Complete missing implementations
   - Add required tests
   - Fix failing validations

4. **Retry Completion:**
   - Once all blockers resolved
   - Run this command again

## Quality Gates

Final verification before marking complete:

### Code Quality

- [ ] All code follows project patterns and standards
- [ ] No TODO or FIXME comments remain unaddressed
- [ ] Documentation is complete (inline and external)

### Testing

- [ ] All unit tests passing
- [ ] All integration tests passing
- [ ] Edge cases have specific test coverage
- [ ] Performance benchmarks validated

### Specification Compliance

- [ ] Every requirement is demonstrably working
- [ ] All acceptance criteria met
- [ ] No unapproved deviations from spec

### Operational Readiness

- [ ] Deployment requirements documented
- [ ] Monitoring plan in place
- [ ] Rollback procedure defined
- [ ] Error handling comprehensive

## Important Notes

- This command should only be run when ALL implementation work is complete
- The PROMPT document is the source of truth for completion status
- Implementation summary uses timestamped format (YYYY-MM-DD_HH-MM-SS)
- All subagent delegations should be reviewed and documented
- Context should be managed throughout (<40% utilization)

---

Once all checks pass and documents are updated, the implementation phase is COMPLETE. The feature is specification-validated, thoroughly tested, and ready for deployment.
