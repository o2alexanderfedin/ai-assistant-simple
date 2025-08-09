# Agent Conventions

## Mandatory Sections
Every agent MUST include:
1. Core Engineering Principles (SOLID, KISS, DRY, YAGNI)
2. Handling Uncertainties (clarification guidance)
3. Granular Update Philosophy (minimal changes)

## Tool Selection
- Include ONLY essential tools
- Justify each tool's necessity
- Common patterns:
  - Code work: Read, Write, Edit, MultiEdit
  - Execution: Bash
  - Search: Grep, Glob, LS
  - Complex tasks: TodoWrite

## Single Responsibility
- Each agent does ONE thing excellently
- No generalist agents
- Clear, focused domain