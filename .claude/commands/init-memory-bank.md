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

Based on the type, create the following modular structure that follows SOLID principles (Single Responsibility - each file has ONE focused purpose):

#### Project Memory Bank (.claude/memory/)
```
.claude/
├── CLAUDE.md           # Main memory file (imports index files)
├── memory/
│   ├── architecture/
│   │   ├── index.md    # Architecture overview & imports
│   │   ├── patterns.md # Design patterns used
│   │   ├── structure.md # Component structure
│   │   └── data-flow.md # Data flow & state management
│   ├── conventions/
│   │   ├── index.md    # Conventions overview & imports
│   │   ├── javascript.md # JS/TS specific conventions
│   │   ├── python.md   # Python specific conventions
│   │   ├── git.md      # Git commit & branch conventions
│   │   └── naming.md   # General naming conventions
│   ├── workflows/
│   │   ├── index.md    # Workflows overview & imports
│   │   ├── development.md # Dev workflow
│   │   ├── testing.md  # Test workflow
│   │   ├── review.md   # Code review process
│   │   └── deployment.md # Deploy workflow
│   ├── dependencies/
│   │   ├── index.md    # Dependencies overview & imports
│   │   ├── runtime.md  # Runtime dependencies
│   │   ├── development.md # Dev dependencies
│   │   └── tools.md    # Build & tooling deps
│   ├── testing/
│   │   ├── index.md    # Testing overview & imports
│   │   ├── unit.md     # Unit test patterns
│   │   ├── integration.md # Integration test patterns
│   │   └── e2e.md      # E2E test patterns
│   └── gotchas/
│       ├── index.md    # Gotchas overview & imports
│       ├── platform.md # Platform-specific issues
│       ├── configuration.md # Config pitfalls
│       └── common.md   # Common mistakes
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
@.claude/memory/architecture/index.md
@.claude/memory/conventions/index.md
@.claude/memory/workflows/index.md
@.claude/memory/dependencies/index.md
@.claude/memory/testing/index.md
@.claude/memory/gotchas/index.md

## Quick Reference
- Build command: `[your build command]`
- Test command: `[your test command]`
- Lint command: `[your lint command]`

## Current Focus
- [ ] [Current task or feature being worked on]
- [ ] [Next priority item]
```

### 5. Initialize Memory Modules

Create index files and specific modules following Single Responsibility:

**architecture/index.md**:
```markdown
# Architecture Overview

Modular architecture documentation following SOLID principles.

## Imports
@.claude/memory/architecture/patterns.md
@.claude/memory/architecture/structure.md
@.claude/memory/architecture/data-flow.md
```

**architecture/patterns.md**:
```markdown
# Design Patterns

## Pattern: [Name]
- **Used in**: [Where]
- **Purpose**: [Why]
- **Implementation**: [How]
```

**conventions/index.md**:
```markdown
# Conventions Overview

Language-specific and general conventions.

## Imports
@.claude/memory/conventions/javascript.md
@.claude/memory/conventions/python.md
@.claude/memory/conventions/git.md
@.claude/memory/conventions/naming.md
```

**conventions/javascript.md**:
```markdown
# JavaScript/TypeScript Conventions

## Style
- Indentation: [2/4 spaces]
- Semicolons: [yes/no]
- Quotes: [single/double]

## Patterns
- [Specific JS patterns]
```

**workflows/index.md**:
```markdown
# Workflows Overview

Separate workflows for different processes.

## Imports
@.claude/memory/workflows/development.md
@.claude/memory/workflows/testing.md
@.claude/memory/workflows/review.md
@.claude/memory/workflows/deployment.md
```

**workflows/development.md**:
```markdown
# Development Workflow

## Local Setup
1. [Step]

## Daily Process
1. [Step]
```

**dependencies/index.md**:
```markdown
# Dependencies Overview

Categorized dependency management.

## Imports
@.claude/memory/dependencies/runtime.md
@.claude/memory/dependencies/development.md
@.claude/memory/dependencies/tools.md
```

**dependencies/runtime.md**:
```markdown
# Runtime Dependencies

## Core Libraries
- [Library]: [Version]
  - Purpose: [Why needed]
  - Usage: [How used]
```

**testing/index.md**:
```markdown
# Testing Overview

Modular testing documentation.

## Imports
@.claude/memory/testing/unit.md
@.claude/memory/testing/integration.md
@.claude/memory/testing/e2e.md
```

**testing/unit.md**:
```markdown
# Unit Testing

## Framework
- Tool: [Jest/Pytest/etc.]
- Location: [test directory]

## Patterns
- [Pattern]: [Usage]

## Commands
- Run: `[command]`
```

**gotchas/index.md**:
```markdown
# Gotchas Overview

Categorized known issues and solutions.

## Imports
@.claude/memory/gotchas/platform.md
@.claude/memory/gotchas/configuration.md
@.claude/memory/gotchas/common.md
```

**gotchas/common.md**:
```markdown
# Common Pitfalls

## Issue: [Name]
- **Symptom**: [What happens]
- **Cause**: [Why it happens]
- **Solution**: [How to fix]
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
- Keep each file focused on ONE responsibility (SOLID)
- Split large files into smaller, focused modules
- Use index.md files to aggregate related memories
- Keep individual memory files under 100 lines
- Use @docs/ references for occasional information
- Update memories when correcting Claude about project details

## Usage Instructions

After initialization:
1. Customize each memory file with project-specific information
2. Use `/memory` command to edit during sessions
3. Reference specific docs with @docs/filename when needed
4. Regularly audit and update as the project evolves

Remember: The memory bank is living documentation that helps Claude Code understand your project's unique context and requirements.