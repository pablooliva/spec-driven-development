# Context Utilization Check

CONTEXT UTILIZATION ANALYSIS

Analyze current context utilization and provide compaction recommendations:

## Context Analysis

1. Estimate current context utilization percentage (target: <40%)
2. Identify what's consuming the most context space:
   - File contents loaded
   - Conversation history length
   - Tool outputs and search results
   - Code generation iterations

## Compaction Decision

1. Recommend if we should compact now based on:
   - Context utilization level
   - Logical stopping point reached
   - Phase completion status

2. If compaction recommended, identify current phase:
   - Research phase (system understanding)
   - Planning phase (specification creation)
   - Implementation phase (code development)

## Preservation Priority

1. List the most critical information that must be preserved:
   - Key insights about system behavior
   - Specification alignment context
   - Current blocking issues or bugs
   - Files and line numbers that matter

## Recommendation

Provide clear recommendation:

- CONTINUE WORKING (if <40% context utilization)
- COMPACT NOW (if >40% utilization) + specify which compact command to use

Include specific next action based on current phase and context state.
