# Specification-Driven Development (SDD) Plugin for Claude Code

A [Claude Code plugin](https://docs.claude.com/en/docs/claude-code/plugins) that provides a comprehensive methodology for systematic software development through research, planning, and implementation phases. This plugin ensures consistent, high-quality development practices with intelligent context management and automated workflows.

This software engineering methodology is based on:

1. [The New Code — Sean Grove, OpenAI](https://www.youtube.com/watch?v=8rABwKRsec4)
2. [Advanced Context Engineering for Agents](https://youtu.be/IS_y40zY-hc?si=5u3ajN073rCu7f88)

An example of this process being used: [video](https://www.youtube.com/watch?v=zNZs19fIDHk) and [repo](https://github.com/ai-that-works/ai-that-works/tree/main/2025-10-14-no-vibes-allowed)

## Installation

Install from a marketplace:

```bash
/plugin install pablooliva/spec-driven-development
```

This will install the plugin system-wide, making it available in all your projects.

Or alternatively, install the plugin at the project level by following the instructions in [plugin-installation-scope.md](plugin-installation-scope.md).

## Overview

The Specification-Driven Development (SDD) plugin transforms how you work with Claude Code by providing:

- **Three-Phase Development Methodology**: Structured research, planning, and implementation workflow
- **Intelligent Context Management**: Automatic tracking and optimization to prevent session overload
- **Model-Optimized Phases**: Leverages Claude Opus for research and Claude Sonnet for planning/implementation
- **Automated Documentation**: Generates research documents, specifications, and progress tracking
- **Built-in Code Review**: Ensures implementations match specifications

## What is Specification-Driven Development?

SDD is a systematic approach that ensures features are thoroughly researched, properly specified, and correctly implemented. Each phase is optimized for different aspects of development:

1. **Research Phase** (Claude Opus) - Deep codebase investigation and pattern analysis
2. **Planning Phase** (Claude Sonnet) - Technical specification and design documentation
3. **Implementation Phase** (Claude Sonnet) - Code development following specifications

## SDD Workflow Overview

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

### Phase Progression

Each phase in the SDD workflow builds upon the previous:

```text
┌─────────────────────────────────────────────────────────────────┐
│                     RESEARCH PHASE (Opus)                       │
│  • Deep codebase exploration                                    │
│  • Pattern identification                                       │
│  • Architecture understanding                                   │
│  Output: SDD/research/RESEARCH-XXX-[feature].md                 │
└─────────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌─────────────────────────────────────────────────────────────────┐
│                    PLANNING PHASE (Sonnet)                      │
│  • Convert research to specifications                           │
│  • Design implementation approach                               │
│  • Define acceptance criteria                                   │
│  Output: SDD/requirements/SPEC-XXX-[feature].md                 │
└─────────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌─────────────────────────────────────────────────────────────────┐
│                 IMPLEMENTATION PHASE (Sonnet)                   │
│  • Write code following specifications                          │
│  • Implement tests                                              │
│  • Ensure quality standards                                     │
│  Output: Implemented feature + tests                            │
└─────────────────────────────────────────────────────────────────┘
```

## Core Commands

### Starting a Development Cycle

```bash
# Begin research on a new feature
/sdd-research-start

# Create specifications from research
/sdd-planning-start

# Start implementation from specifications
/sdd-implementation-start
```

### Managing Long Sessions

When context approaches 40%, use compaction commands to continue working:

```bash
# Compact and continue research
/sdd-research-compact

# Compact and continue planning
/sdd-planning-compact

# Compact and continue implementation
/sdd-implementation-compact
```

### Completing Phases

```bash
# Finalize research documentation
/sdd-research-complete

# Finalize specification
/sdd-planning-complete

# Complete implementation
/sdd-implementation-complete
```

### Utility Commands

```bash
# Resume work after clearing session
/sdd-continue

# Check current context utilization
/sdd-context-check

# Monitor progress across all phases
/sdd-monitor

# Review code against specifications
/sdd-code-review

# Create commits following conventions
/sdd-commit
```

## Workflow Example

### Complete Feature Development

1. **Start Research** (with Claude Opus):

   ```bash
   /sdd-research-start
   # Describe the feature you want to research
   ```

2. **Manage Context** (when approaching 40%):

   ```bash
   /sdd-research-compact
   /sdd-commit
   /clear
   /sdd-continue
   ```

3. **Complete Research**:

   ```bash
   /sdd-research-complete
   /sdd-commit
   ```

4. **Create Specification** (switch to Claude Sonnet):

   ```bash
   /sdd-planning-start
   # Review and refine the specification
   ```

5. **Implement Feature**:

   ```bash
   /sdd-implementation-start
   # Code is developed following the specification
   ```

6. **Review and Finalize**:

   ```bash
   /sdd-code-review
   /sdd-implementation-complete
   /sdd-commit
   ```

## Directory Structure

The plugin automatically creates and manages the following structure in your project:

```text
project/
└── SDD/                          # Root directory for all SDD artifacts
    ├── research/                 # Research phase documents
    │   └── RESEARCH-XXX-*.md     # Detailed investigation findings
    ├── requirements/             # Planning phase specifications
    │   └── SPEC-XXX-*.md         # Technical specifications
    └── prompts/                  # Session management
        ├── implementation-complete/  # Archived implementations
        └── context-management/   # Progress tracking
            ├── progress.md       # Current phase progress
            ├── *.compact.md      # Compacted session data
            └── subagent-calls/   # Subagent interaction logs
```

## Key Features

### Context Management

The plugin maintains <40% context utilization to ensure:

- Sufficient headroom for complex operations
- Effective subagent utilization
- Prevention of context overflow errors

### Automated Progress Tracking

- Automatic session compaction when context grows
- Progress persistence across session clears
- Seamless continuation of interrupted work

### Model Optimization

- **Research**: Uses Claude Opus for deep understanding
- **Planning/Implementation**: Uses Claude Sonnet for efficiency
- **Automatic Switching**: Commands handle model selection

### Documentation Generation

- Research documents capture codebase understanding
- Specifications define implementation requirements
- Progress files track session state
- Subagent calls are automatically logged

## Best Practices

### When to Use Full SDD Workflow

Use the complete three-phase workflow for:

- New features requiring research
- Complex architectural changes
- Breaking changes to existing functionality
- Features with unclear requirements

### Quick Implementation

For simple, well-understood changes:

- Skip directly to `/sdd-implementation-start`
- Provide clear requirements in the initial prompt

### Context Management Strategy

- Check context regularly with `/sdd-context-check`
- Compact proactively before hitting 40%
- Use `/sdd-continue` to resume seamlessly

### Commit Workflow

The `/sdd-commit` command ensures:

- Conventional Commits specification
- Proper co-authorship attribution
- Reference to specifications and research
- Clear change history

## Plugin Configuration

### Hooks

The plugin includes an automatic subagent logging hook that tracks all subagent interactions for debugging and progress monitoring.

### Settings

The plugin respects your Claude Code settings while providing additional safeguards for destructive operations during development.

## Version History

- **1.0.0** - Initial release with complete SDD methodology

## Author

**Pablo Oliva**
Email: <p.o@pablooliva.de>

## Support

For issues, feature requests, or questions:

- Create an issue in the plugin repository
- Contact the author directly
- Check the [Claude Code documentation](https://docs.claude.com/en/docs/claude-code/plugins)

## License

This plugin is provided as-is for use with Claude Code. See the repository for license details.

---

**Built for Claude Code** - Enhancing AI-assisted development with systematic methodology
