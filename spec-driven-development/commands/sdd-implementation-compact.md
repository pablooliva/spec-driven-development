# Implementation Progress Compaction

IMPLEMENTATION PROGRESS COMPACTION

Context is getting overloaded during implementation. Create permanent compaction record to preserve your work while freeing up context.

## Context Status

This command is specifically designed for when context utilization is high (typically >35-40%). Current situation:

```text
Expected context utilization: >35% (reason for running this command)
Target after session restart: <10% (fresh context)
```

If context is NOT high, consider continuing work instead of compacting.

## Process

### 1. Create Timestamped Compaction File

Write to: `SDD/prompts/context-management/implementation-compacted-[YYYY-MM-DD_HH-MM-SS].md`

Format: `implementation-compacted-YYYY-MM-DD_HH-MM-SS.md` (24-hour time format)
Example: `implementation-compacted-2025-10-01_14-30-45.md`

### 2. Document Structure

Use the following template:

```markdown
# Implementation Compaction - [Feature Name] - [Date/Time]

## Session Context

- Compaction trigger: [context %] utilization
- Implementation focus: [specific feature/component being coded]
- Specification reference: [SPEC-XXX being implemented]
- Session duration: [approximate time/interactions]

## Recent Changes
[List specific files modified with line references where relevant - e.g., `src/auth/login.ts:45-67`]
- File 1: [brief description of changes]
- File 2: [brief description of changes]

**Avoid large code blocks** - use file:line references instead

## Implementation Progress
- **Completed**: [features/components fully implemented and tested]
- **In Progress**: [current work items and their status]
- **Planned**: [next tasks from specification]

## Tests Status
- Tests added: [list test files and what they cover]
- Tests passing: [X/Y passing]
- Coverage gaps: [areas needing tests]

## Critical Learnings
[Important discoveries made during implementation - patterns found, root causes identified, architectural insights]
- How implementation differed from spec: [key differences]
- Edge case handling: [how EDGE-XXX scenarios were implemented]
- Technical decisions: [conscious trade-offs and why]
- Performance considerations: [optimization decisions]

## Critical References
[2-3 most important documents/files needed to understand this work]
- Specification: [path to spec document]
- Related architecture: [path if applicable]
- Key implementation file: [path to core file]

## Next Session Priorities

**Essential Files to Reload:**
- [Specific paths and line ranges needed to resume work]

**Current Focus:**
- Exact problem being solved: [specific bug/feature]
- Blocking issue: [if any]

**Implementation Priorities:**
1. [Specific next code to write]
2. [Following task]
3. [Subsequent task]

**Specification Validation Remaining:**
- [ ] [Success criterion not yet met]
- [ ] [Edge case not yet implemented]
- [ ] [Performance requirement not yet validated]

## Other Notes
[Any additional context, gotchas, or important information for continuation]
```

### 3. Update Current Progress

Also update `SDD/prompts/context-management/progress.md` with:

- Latest implementation state
- Working functionality status
- Next development priorities
- Reference to this compaction file

---

## Guidelines

- **Be thorough but concise** - capture key details without overwhelming context
- **Avoid excessive code snippets** - prefer file:line references over large diffs
- **Include precise references** - enable quick reload of necessary context
- **Document learnings** - preserve insights for future sessions
- **Mark clear status** - distinguish completed vs. in-progress vs. planned work

This preserves complete implementation journey while enabling fresh context continuation.

## Important: Commit Your Code Changes

**Before clearing your session:**

1. **Run `/sdd-commit`** to commit any code changes you've made
2. This ensures your implementation work is safely saved in version control
3. The commit message will be automatically formatted according to project conventions

## Next Steps After Compaction

After compaction and commit are complete:

1. **Commit your changes** - Run `/sdd-commit` if you haven't already
2. **Clear the current session** - Close Claude Code or start a new conversation
3. **Start a fresh Claude Code session** with Claude Sonnet
4. **Run `/sdd-continue`** to resume from where you left off
5. The continue command will reload your progress from `progress.md` and the compaction file

Implementation phase continues - use `/sdd-implementation-complete` command when feature is finished.
