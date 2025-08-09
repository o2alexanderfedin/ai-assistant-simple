# Claude Code Slash Commands - Complete Guide

A comprehensive guide to creating and managing custom slash commands in Claude Code.

## Table of Contents

1. [Overview](#overview)
2. [Command Types](#command-types)
3. [Creating Custom Commands](#creating-custom-commands)
4. [YAML Frontmatter](#yaml-frontmatter)
5. [Advanced Features](#advanced-features)
6. [Best Practices](#best-practices)
7. [Examples](#examples)
8. [Troubleshooting](#troubleshooting)

## Overview

Slash commands in Claude Code allow you to create reusable prompts and workflows that can be triggered with a simple `/command` syntax. They enable automation, standardization, and efficiency in your development workflow.

### Key Benefits
- **Reusability**: Define once, use many times
- **Consistency**: Standardize common operations across your team
- **Efficiency**: Reduce repetitive typing and prompt engineering
- **Shareability**: Project commands can be version controlled and shared

## Command Types

### 1. Built-in Commands
Pre-defined commands that come with Claude Code:
- `/help` - Show available commands
- `/clear` - Clear the conversation
- `/review` - Review files or code
- `/model` - Switch AI model
- `/think` - Enable extended thinking mode
- `/thinker` - Toggle thinking visibility

### 2. Project Commands
- **Location**: `.claude/commands/` in your repository
- **Scope**: Available to all team members working on the project
- **Display**: Shows "(project)" suffix in `/help`
- **Version Control**: Can be committed to git

### 3. Personal Commands
- **Location**: `~/.claude/commands/` in your home directory
- **Scope**: Available across all your projects
- **Display**: Shows "(user)" suffix in `/help`
- **Privacy**: Not shared with team

## Creating Custom Commands

### Basic Structure

1. **Create a markdown file** in the appropriate commands directory
2. **Name determines command**: `fix-issue.md` becomes `/fix-issue`
3. **Add content**: The markdown body becomes the prompt

### File Naming Rules
- Use lowercase letters
- Replace spaces with hyphens or underscores
- Avoid special characters
- Extension must be `.md`

### Directory Structure
```
.claude/commands/
├── save-and-release.md      # /save-and-release
├── init-memory-bank.md       # /init-memory-bank
└── git/                      # Namespacing
    ├── commit.md            # /git/commit
    └── sync.md              # /git/sync
```

## YAML Frontmatter

Frontmatter provides metadata and configuration for your commands.

### Complete Frontmatter Reference

```yaml
---
# Tool Restrictions (optional)
# Specify which tools the command can use
# Format: ToolName or ToolName(specific-command:pattern)
allowed-tools: Bash, Read, Write, Edit, Grep

# Restricted tool example with specific commands
allowed-tools: Bash(git add:*), Bash(git commit:*), Read

# Argument Hint (optional)
# Shows expected arguments in autocomplete
argument-hint: [type] [message]
argument-hint: <required> [optional]
argument-hint: add [tagId] | remove [tagId] | list

# Description (optional)
# Brief explanation shown in /help
# If omitted, uses first line of command body
description: Create a comprehensive test suite

# Model Selection (optional)
# Choose specific AI model for this command
# Options: opus, sonnet, haiku, or specific model ID
model: sonnet
model: claude-3-5-sonnet-20241022

# For subagents only
name: agent-name
tools: tool1, tool2, tool3  # If omitted, inherits all tools
---
```

### Frontmatter Behaviors

#### allowed-tools
- **Default**: Inherits all tools from conversation
- **Restrictive**: When specified, ONLY listed tools are available
- **Granular Control**: Can restrict to specific commands
  ```yaml
  allowed-tools: Bash(npm test), Bash(npm run:*), Read
  ```

#### argument-hint
- Displayed during command autocomplete
- Helps users understand expected inputs
- Supports multiple formats:
  ```yaml
  # Single argument
  argument-hint: [message]
  
  # Multiple arguments
  argument-hint: [type] [scope] [description]
  
  # Alternative syntax
  argument-hint: create <name> | delete <id> | list [filter]
  ```

#### description
- Shown in `/help` command list
- Should be concise (one line)
- If omitted, extracts first line from command body

#### model
- Forces specific model for command execution
- Overrides conversation model
- Useful for:
  - Cost optimization (use haiku for simple tasks)
  - Quality requirements (use opus for complex analysis)
  - Consistency (ensure same model across team)

## Advanced Features

### 1. Dynamic Arguments with $ARGUMENTS

Pass runtime arguments to commands:

```markdown
---
description: Fix a GitHub issue
argument-hint: [issue-number]
---

Please analyze and fix GitHub issue #$ARGUMENTS following our coding standards.
```

Usage: `/fix-issue 123`

### 2. Bash Command Execution with !

Execute commands before the prompt runs:

```markdown
---
allowed-tools: Bash(git:*), Read, Write
---

## Current State
- Status: !`git status`
- Branch: !`git branch --show-current`
- Recent commits: !`git log --oneline -5`

Based on the above, create a meaningful commit.
```

**Important**: Must include `Bash` in `allowed-tools`

### 3. File Inclusion with @

Reference file contents in prompts:

```markdown
---
description: Review code changes
---

Review these files for best practices:
- Implementation: @src/feature.js
- Tests: @tests/feature.test.js
- Documentation: @docs/feature.md

Ensure they follow our coding standards.
```

### 4. Namespacing with Subdirectories

Organize related commands:

```
.claude/commands/
├── git/
│   ├── commit.md      # /git/commit
│   ├── pr.md          # /git/pr
│   └── sync.md        # /git/sync
├── test/
│   ├── unit.md        # /test/unit
│   └── e2e.md         # /test/e2e
└── deploy/
    ├── staging.md     # /deploy/staging
    └── production.md  # /deploy/production
```

### 5. Combining Features

Complex command example:

```markdown
---
description: Smart commit with conventional commits
allowed-tools: Bash(git:*), Read
argument-hint: [type] [scope] [breaking]
model: sonnet
---

## Repository State
!`git status`
!`git diff --cached`

## Recent Commits (for style reference)
!`git log --oneline -10`

## Commit Type
Type: ${ARGUMENTS[0]:-feat}
Scope: ${ARGUMENTS[1]:-general}
Breaking: ${ARGUMENTS[2]:-false}

Create a conventional commit following the pattern in @.github/COMMIT_CONVENTION.md
```

## Best Practices

### 1. Command Design
- **Single Responsibility**: Each command should do one thing well
- **Clear Naming**: Use descriptive, action-oriented names
- **Consistent Style**: Follow naming conventions across all commands
- **Documentation**: Include clear descriptions and argument hints

### 2. Tool Management
- **Principle of Least Privilege**: Only allow necessary tools
- **Specific Permissions**: Use granular command restrictions when possible
- **Security**: Never allow dangerous commands without restrictions
  ```yaml
  # Good
  allowed-tools: Bash(npm test), Bash(npm run build)
  
  # Risky
  allowed-tools: Bash
  ```

### 3. Project vs Personal Commands
- **Project Commands**: Team workflows, project-specific tasks
- **Personal Commands**: Individual preferences, experimental features
- **Migration Path**: Start personal, promote to project when proven

### 4. Version Control
- Commit `.claude/commands/` to repository
- Document command changes in commit messages
- Consider command versioning for breaking changes
- Review command changes in PRs

### 5. Performance
- Use appropriate models (haiku for simple, opus for complex)
- Minimize bash execution in prompts
- Cache frequently accessed file contents
- Avoid recursive or expensive operations

## Examples

### Example 1: Automated Testing
```markdown
---
description: Run tests and fix failures
allowed-tools: Bash(npm test), Bash(npm run:*), Read, Edit
model: sonnet
---

Run the test suite and if any tests fail:
1. Analyze the failure
2. Fix the code
3. Re-run tests to confirm
4. Create a summary of changes
```

### Example 2: PR Creation
```markdown
---
description: Create a pull request
argument-hint: [branch-name] [title]
allowed-tools: Bash(git:*), Bash(gh pr:*)
---

## Current branch
!`git branch --show-current`

## Changes
!`git log origin/main..HEAD --oneline`
!`git diff origin/main...HEAD --stat`

Create a PR from current branch to main with title: $ARGUMENTS
Generate a comprehensive PR description based on the commits.
```

### Example 3: Code Review
```markdown
---
description: Review code for security and performance
allowed-tools: Read, Grep
model: opus
---

Review all recently modified files for:
1. Security vulnerabilities
2. Performance issues
3. Best practice violations

Files to review:
!`git diff --name-only HEAD~5..HEAD | grep -E '\.(js|ts|py)$'`
```

### Example 4: Documentation Generator
```markdown
---
description: Generate API documentation
allowed-tools: Read, Write, Grep
argument-hint: [output-format]
---

Scan the codebase for API endpoints:
!`grep -r "app\.(get|post|put|delete)" --include="*.js" .`

Generate ${ARGUMENTS:-markdown} documentation for all endpoints.
Include parameters, responses, and examples.
```

## Troubleshooting

### Command Not Found
- Check file location (`.claude/commands/` or `~/.claude/commands/`)
- Verify file extension is `.md`
- Ensure no syntax errors in filename
- Restart Claude Code if needed

### Frontmatter Not Working
- Validate YAML syntax (proper indentation, quotes)
- Ensure `---` delimiters are on their own lines
- Check for invisible characters or wrong encoding
- Test with minimal frontmatter first

### Tool Permissions Issues
- Verify tool names are spelled correctly
- Check allowed-tools syntax for specific commands
- Ensure required tools are included
- Test with broader permissions, then restrict

### Arguments Not Substituting
- Use exact `$ARGUMENTS` keyword (case-sensitive)
- For multiple arguments, parse within the prompt
- Test with simple echo commands first
- Check argument-hint matches expected usage

### Performance Issues
- Review bash commands for efficiency
- Consider using lighter model (haiku)
- Minimize file operations
- Cache or pre-compute when possible

## Command Development Workflow

1. **Start with personal command** for testing
   ```bash
   mkdir -p ~/.claude/commands
   echo "Test prompt" > ~/.claude/commands/test.md
   ```

2. **Iterate and refine** the prompt and frontmatter

3. **Test with various inputs** and edge cases

4. **Move to project** when ready
   ```bash
   mv ~/.claude/commands/test.md .claude/commands/
   git add .claude/commands/test.md
   git commit -m "feat: add test command for team use"
   ```

5. **Document** in team wiki or README

## Security Considerations

### Tool Restrictions
- Never allow unrestricted `Bash` for commands that accept user input
- Validate and sanitize `$ARGUMENTS` usage
- Restrict file operations to project directories
- Avoid commands that could modify system files

### Safe Patterns
```yaml
# Good: Specific, safe operations
allowed-tools: Bash(npm test), Read(./src/*), Write(./output/*)

# Bad: Too permissive
allowed-tools: Bash, Write
```

### Review Checklist
- [ ] Tools are minimally scoped
- [ ] No sensitive data in prompts
- [ ] Arguments are validated
- [ ] File paths are restricted
- [ ] Commands are idempotent when possible

## Integration with CI/CD

Commands can be used in automation:

```bash
# In GitHub Actions
- name: Run Claude Code command
  run: |
    claude-code /deploy/staging --no-interactive
```

## Future Considerations

As Claude Code evolves, watch for:
- New frontmatter options
- Additional tool types
- Enhanced argument parsing
- Command composition/chaining
- Conditional execution
- Command marketplace/sharing

## References

- [Official Anthropic Documentation](https://docs.anthropic.com/en/docs/claude-code/slash-commands)
- [Claude Code Settings](https://docs.anthropic.com/en/docs/claude-code/settings)
- [Subagents Documentation](https://docs.anthropic.com/en/docs/claude-code/sub-agents)
- [Common Workflows](https://docs.anthropic.com/en/docs/claude-code/common-workflows)