# Research Progress Compaction

RESEARCH PROGRESS COMPACTION

Context is getting overloaded during research phase. Create permanent compaction record to preserve your work while freeing up context.

## Process

### 1. Create Timestamped Compaction File

Write to: `SDD/prompts/context-management/research-compacted-[YYYY-MM-DD_HH-MM-SS].md` where:

- `[YYYY-MM-DD_HH-MM-SS]` is the current timestamp (24-hour time)
- Example: `research-compacted-2025-10-01_14-30-45.md`

### 2. Document Structure

Use the following template:

```markdown
# Research Compaction - [Feature Name] - [Date/Time]

## Session Context

- Compaction trigger: [context %] utilization
- Research focus: [what we were investigating]
- Session duration: [approximate time/interactions]

## Recent Investigations
[List specific areas/files investigated with file:line references where relevant]
- Area 1: [brief description of what was discovered]
- Area 2: [brief description of what was discovered]

**Avoid large code blocks** - use file:line references instead

## Research Progress
- **Completed**: [research areas fully understood and documented]
- **In Progress**: [current investigation areas and their status]
- **Planned**: [remaining areas to investigate]

## System Behavior Discovered
[Key insights about how the system works]
- Architecture patterns: [important patterns found]
- Data flow: [how data moves through the system]
- Integration points: [how components interact]
- Performance characteristics: [bottlenecks, optimization opportunities]

## Critical Learnings
[Important discoveries that must be preserved - patterns, root causes, architectural insights]
- Critical files located: [specific paths:line numbers that matter]
- Production issues found: [concrete problems with issue numbers]
- Stakeholder insights: [what we learned about user/business needs]
- Technical constraints: [limitations discovered]
- Edge cases identified: [scenarios that need special handling]

## Critical References
[2-3 most important files/documents needed to understand this work]
- Key implementation file: [path to core file]
- Related documentation: [path if applicable]
- Research document in progress: SDD/research/RESEARCH-[###]-[feature-name].md

## Next Session Priorities

**Essential Files to Reload:**
- [Specific paths and line ranges needed to resume work]

**Current Focus:**
- Exact investigation being conducted: [specific area/question]
- Blocking questions: [if any]

**Research Priorities:**
1. [Specific next area to investigate]
2. [Following investigation]
3. [Subsequent investigation]

**Outstanding Research Questions:**
- [ ] [Question not yet answered]
- [ ] [Area not yet explored]
- [ ] [Hypothesis not yet validated]
- [ ] [Stakeholder input needed]

## Other Notes
[Any additional context, investigation approaches to try, or important information for continuation]
```

### 3. Update Current Progress

Also update `SDD/prompts/context-management/progress.md` with:

- Latest research state
- Current blocking questions
- Next session continuation point
- Reference to this compaction files

---

## Guidelines

- **Be thorough but concise** - capture key discoveries without overwhelming context
- **Avoid excessive code snippets** - prefer file:line references over large code blocks
- **Include precise references** - enable quick reload of critical files
- **Document insights** - preserve understanding of system behavior and patterns
- **Mark clear status** - distinguish completed vs. in-progress vs. planned research

This preserves complete research journey while enabling fresh context continuation.

## Next Steps After Compaction

After this compaction is complete:

1. **Clear the current session** - Close Claude Code or start a new conversation
2. **Start a fresh Claude Code session** with Claude Opus
3. **Run `/sdd-continue`** to resume from where you left off
4. The continue command will reload your progress from `progress.md` and the compaction file

Research phase continues - use `/sdd-research-complete` command when investigation is finished.
