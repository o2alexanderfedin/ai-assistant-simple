---
description: Initialize a memory bank structure for Claude Code with CLAUDE.md and supporting files
argument-hint: [type] (e.g., "project", "team", "personal")
allowed-tools: Write, Read, LS, Bash
---

# Initialize Memory Bank for Claude Code

You will set up a comprehensive memory bank structure to help Claude Code maintain context and knowledge about this project.

## Workflow Steps

### 1. Analyze Arguments
Parse the provided arguments: `$ARGUMENTS`
- If "project" or no argument: Initialize project-specific memory
- If "team": Initialize team-shared memory configuration
- If "personal": Initialize user-specific preferences

### 2. Check Existing Structure
Verify what already exists:
- Check for existing CLAUDE.md in project root
- Check for .claude/memory/ directory
- Check for docs/ directory

### 3. Create Memory Bank Structure

Based on the type, create the following structure:

#### Project Memory Bank (.claude/memory/)
```
.claude/
├── CLAUDE.md           # Main memory file (imports others)
├── memory/
│   ├── architecture.md # System architecture & design patterns
│   ├── conventions.md  # Coding standards & naming conventions
│   ├── workflows.md    # Development workflows & processes
│   ├── dependencies.md # Key dependencies & their usage
│   ├── testing.md      # Testing strategies & patterns
│   └── gotchas.md      # Known issues & workarounds
└── docs/               # Ad-hoc documentation (referenced as needed)
```

### 4. Initialize Root CLAUDE.md
Create or update the root CLAUDE.md with:
```markdown
# Project Memory Bank

This file maintains essential context for Claude Code sessions.

## Core Principles
- Follow SOLID, KISS, DRY, YAGNI principles
- Prefer updating existing files over creating new versions
- Make minimal, targeted changes
- Ask for clarification when requirements are ambiguous

## Project Overview
- **Purpose**: [Brief project description]
- **Tech Stack**: [Primary technologies used]
- **Key Directories**: [Important folders and their purposes]

## Imports
@.claude/memory/architecture.md
@.claude/memory/conventions.md
@.claude/memory/workflows.md
@.claude/memory/dependencies.md
@.claude/memory/testing.md
@.claude/memory/gotchas.md

## Quick Reference
- Build command: `[your build command]`
- Test command: `[your test command]`
- Lint command: `[your lint command]`

## Current Focus
- [ ] [Current task or feature being worked on]
- [ ] [Next priority item]
```

### 5. Initialize Memory Modules

Create each memory module with appropriate templates:

**architecture.md**:
```markdown
# System Architecture

## Design Patterns
- [Pattern used]: [Where and why]

## Component Structure
- [Component]: [Responsibility]

## Data Flow
- [Flow description]
```

**conventions.md**:
```markdown
# Coding Conventions

## Style Guide
- Indentation: [spaces/tabs, size]
- Line length: [max characters]
- File naming: [pattern]

## Code Organization
- [Specific patterns used]

## Git Conventions
- Commit format: [conventional commits, etc.]
- Branch naming: [pattern]
```

**workflows.md**:
```markdown
# Development Workflows

## Development Process
1. [Step-by-step workflow]

## Review Process
- [PR requirements]
- [Review checklist]

## Deployment Process
- [Deployment steps]
```

**dependencies.md**:
```markdown
# Key Dependencies

## Core Libraries
- [Library]: [Version] - [Usage]

## Development Tools
- [Tool]: [Purpose]

## Important Versions
- Node/Python/etc.: [version]
```

**testing.md**:
```markdown
# Testing Strategy

## Test Structure
- Unit tests: [location, framework]
- Integration tests: [location, framework]
- E2E tests: [location, framework]

## Coverage Requirements
- Target coverage: [percentage]
- Critical paths: [areas that must be tested]

## Test Commands
- Run all tests: `[command]`
- Run specific suite: `[command]`
```

**gotchas.md**:
```markdown
# Known Issues & Workarounds

## Common Pitfalls
- [Issue]: [Solution]

## Platform-Specific Issues
- [Platform]: [Issue and workaround]

## Configuration Gotchas
- [Config issue]: [Correct approach]
```

### 6. Create docs/ Directory
Create a docs/ directory for ad-hoc documentation:
```
docs/
├── README.md           # Guide to using the docs folder
└── examples/           # Example configurations, snippets
```

### 7. Report Completion

Provide a summary of:
- Files created
- Structure initialized
- Next steps for customization
- How to reference memories in conversations

## Best Practices to Include

- Keep memories specific and actionable
- Remove obsolete information regularly
- Use bullet points for clarity
- Group related items under headings
- Keep core memory files under 500 lines
- Use @docs/ references for occasional information
- Update memories when correcting Claude about project details

## Usage Instructions

After initialization:
1. Customize each memory file with project-specific information
2. Use `/memory` command to edit during sessions
3. Reference specific docs with @docs/filename when needed
4. Regularly audit and update as the project evolves

Remember: The memory bank is living documentation that helps Claude Code understand your project's unique context and requirements.