# Research Phase Completion

RESEARCH PHASE COMPLETION

Research phase is complete and ready for specification creation.

## 1. Verify Research Document Completeness

Confirm that `SDD/research/RESEARCH-[###]-[feature-name].md` contains all required sections with complete information:

### System Data Flow

- [ ] Key data flows identified with specific file:line references and how data moves
- [ ] Key entry points documented with specific file:line references
- [ ] Data transformations explained
- [ ] External dependencies identified
- [ ] Integration points documented (where this feature connects to existing systems)

### Stakeholder Mental Models

- [ ] Product team perspective captured
- [ ] Engineering team perspective captured
- [ ] Support team perspective captured
- [ ] User perspective captured

### Production Edge Cases

- [ ] Historical issues analyzed with issue numbers
- [ ] Support ticket patterns documented
- [ ] Error log failure patterns identified

### Files That Matter

- [ ] Core logic files identified with significance explained
- [ ] Existing test coverage gaps documented
- [ ] Configuration files noted

### Security Considerations

- [ ] Authentication/authorization requirements documented
- [ ] Data privacy concerns identified
- [ ] Input validation needs specified

### Testing Strategy

- [ ] Unit test requirements defined
- [ ] Integration test points identified
- [ ] Edge case scenarios specified

### Documentation Needs

- [ ] User-facing documentation requirements identified
- [ ] Developer documentation needs specified
- [ ] Configuration documentation requirements noted

## 2. Finalize Research Document

Ensure all investigation questions are answered and the research document provides sufficient foundation for specification creation without requiring additional system investigation.

## 3. Record Phase Transition

Write brief transition note to `SDD/prompts/context-management/progress.md`:

"Research phase complete. RESEARCH-[###]-[feature-name].md finalized. Ready for /sdd-planning-start."

## Phase Complete

Research phase FINISHED. Next Claude Code session should begin SPEC-[###]-[feature-name] creation using this research foundation.
