# Initialize Research Phase

RESEARCH PHASE INITIALIZATION

Starting research phase for new feature/issue.

IMPORTANT: This command requires Claude Opus. Before proceeding, check your current model ID in the system information. If you are NOT running on a Claude Opus model (e.g., claude-opus-*), immediately:

  1. Warn the user: "WARNING: This command requires Claude Opus but you're currently using [model name]. Please switch to Opus and try again."
  2. STOP all further processing - do not execute any of the instructions below.

IMPORTANT: Before starting this phase, check if `SDD/prompts/context-management/progress.md` contains any important information. If it does, ask the user if they want to archive it before resetting. Then reset the file to only contain a heading: `# Research Progress`. We are starting on a new task and want to ensure that the progress file is clean.

Set up systematic investigation:

## Research Setup

1. Create `SDD/research/RESEARCH-[###]-[feature-name].md` document where:
   - `[###]` is the issue/ticket number if available, or use sequential numbering (001, 002, etc.)
   - `[feature-name]` is a kebab-case description (e.g., "user-authentication", "csv-export")

Use this structure for the research document:

```markdown
# RESEARCH-[###]-[feature-name]

## System Data Flow

- Key entry points: [files and line numbers]
- Data transformations: [how information flows]
- External dependencies: [APIs, databases, services]
- Integration points: [where this feature connects to existing systems]

## Stakeholder Mental Models

- Product Team perspective:
- Engineering Team perspective:
- Support Team perspective:
- User perspective:

## Production Edge Cases

- Historical issues: [issue numbers and patterns]
- Support tickets: [common problems]
- Error logs: [failure patterns]

## Files That Matter

- Core logic: [primary implementation files]
- Tests: [existing test coverage gaps]
- Configuration: [relevant config files]

## Security Considerations

- Authentication/Authorization: [auth requirements]
- Data Privacy: [sensitive data handling]
- Input Validation: [validation needs]

## Testing Strategy

- Unit tests: [what needs testing]
- Integration tests: [integration points]
- Edge cases: [specific scenarios to test]

## Documentation Needs

- User-facing docs: [what users need to know]
- Developer docs: [API/implementation docs]
- Configuration docs: [setup/config changes]
```

## Research Process

Begin systematic system understanding:

- Map data flows across codebase with specific file:line references
- Interview/research stakeholder needs and mental models
- Analyze production issues and error patterns
- Document existing edge cases with specific examples

## Context Management

1. Maintain <40% context utilization throughout research
2. Use the Explore subagent (Task tool with subagent_type=Explore) for file discovery and system mapping
3. Focus on understanding before any specification work

## Deliverable Target

Complete research document that enables specification creation without additional system investigation.

Begin research now - create the `SDD/research/RESEARCH-[###]-[feature-name].md` document and start systematic investigation.
