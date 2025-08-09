# AI Assistant Simple - Project Memory Bank

This file maintains essential context for Claude Code sessions on the AI Assistant Simple project.

## Core Principles
- Follow SOLID, KISS, DRY, YAGNI principles religiously
- Prefer updating existing files over creating new versions
- Make minimal, targeted changes - surgical precision over wholesale rewrites
- Ask for clarification when requirements are ambiguous
- Create new artifacts ONLY to fix principle violations

## Project Overview
- **Purpose**: Agent management system for Claude AI with specialized agents
- **Tech Stack**: Markdown-based agent definitions, YAML frontmatter, Git/GitHub
- **Key Directories**: 
  - `.claude/agents/` - Agent definitions
  - `.claude/commands/` - Custom slash commands
  - `.claude/memory/` - Memory bank modules (when initialized)

## Agent Creation Standards
- Every agent MUST include Core Engineering Principles section
- Every agent MUST include Handling Uncertainties section  
- Every agent MUST include Granular Update Philosophy section
- Agents must have single, focused responsibility
- Tool selection must be minimal and justified

## Slash Commands
- `/save-and-release` - Automated gitflow commit, push, and release
- `/init-memory-bank` - Initialize memory bank structure

## Quick Reference
- Build command: N/A (markdown-based project)
- Test command: N/A (no automated tests yet)
- Lint command: N/A
- Release command: `/save-and-release`

## Git Conventions
- Commit format: Conventional commits (feat:, fix:, chore:, etc.)
- Branch strategy: Gitflow (feature/, fix/, hotfix/, release/)
- Version tracking: VERSION file + GitHub releases

## Current Focus
- [x] Create agent-hr-manager for agent workforce management
- [x] Implement core principles enforcement
- [x] Add granular update philosophy
- [x] Create memory bank initialization
- [ ] Expand agent library with more specialized agents
- [ ] Add agent testing framework

## Important Files
- `VERSION` - Current version number (for releases)
- `.claude/agents/agent-hr-manager.md` - HR manager for creating agents
- `.claude/agents/agent-software-engineer-in-test.md` - SDET specialist
- `.claude/commands/save-and-release.md` - Release automation
- `.claude/commands/init-memory-bank.md` - Memory bank setup

## Memory Imports
@.claude/memory/architecture/index.md
@.claude/memory/conventions/index.md
@.claude/memory/workflows/index.md
@.claude/memory/dependencies/index.md
@.claude/memory/testing/index.md
@.claude/memory/gotchas/index.md

## Project-Specific Rules
1. Agents must explicitly state adherence to engineering principles
2. New agents require thorough tool analysis
3. File updates preferred over recreations
4. Minimal changes only - no scope creep
5. Principle violations are the ONLY valid reason for new artifacts