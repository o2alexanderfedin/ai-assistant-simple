---
description: Create a new slash command with proper structure and frontmatter
argument-hint: <name> <description> [tools] [model]
allowed-tools: Write, Read, Edit
---

# Create New Slash Command

You will create a new slash command based on the provided arguments.

## Arguments Provided
`$ARGUMENTS`

## Parse Arguments
Parse the arguments in this format:
1. **name** (required): Command name (will be filename without .md)
2. **description** (required): Brief description of what the command does
3. **tools** (optional): Comma-separated list of tools (default: inherit all)
4. **model** (optional): AI model to use (opus/sonnet/haiku, default: inherit)

Example: `create-command deploy-app "Deploy application to staging" "Bash,Read" sonnet`

## Documentation Reference
For complete slash command documentation, refer to:
- **Guide**: `.claude/docs/claude/slash-commands-guide.md`
- **Quick Reference**: `.claude/docs/claude/slash-commands-quick-reference.md`
- **Examples**: `.claude/commands/` directory

## Command Creation Steps

### 1. Validate Input
- Ensure command name is provided and valid (lowercase, hyphens/underscores only)
- Ensure description is provided
- If tools specified, validate they are valid tool names
- If model specified, ensure it's opus, sonnet, or haiku

### 2. Determine Command Type
Ask the user about the command's purpose to create an appropriate template:
- **Workflow Command**: Multi-step process with bash execution
- **Analysis Command**: Code review, security audit, etc.
- **Generation Command**: Create files, documentation, etc.
- **Utility Command**: Simple single-purpose tool

### 3. Create Command Structure

Based on the type and arguments, create a markdown file at `.claude/commands/<name>.md` with:

```yaml
---
description: [provided description]
argument-hint: [suggest based on command type]
allowed-tools: [if tools provided, otherwise omit]
model: [if model provided, otherwise omit]
---
```

### 4. Generate Command Body

Include these sections based on command type:

#### For Workflow Commands:
```markdown
# [Command Title]

## Context Gathering
[Include bash commands with !`command` syntax if needed]

## Task Execution
[Main workflow steps]
Handle arguments: $ARGUMENTS

## Validation
[How to verify success]
```

#### For Analysis Commands:
```markdown
# [Analysis Title]

## Files to Analyze
[Use @filepath or bash commands to gather files]

## Analysis Criteria
[What to look for]

## Report Format
[How to present findings]
```

#### For Generation Commands:
```markdown
# [Generation Title]

## Requirements
Parse arguments: $ARGUMENTS

## Generation Steps
[What to create and how]

## Output Location
[Where files should be created]
```

#### For Utility Commands:
```markdown
# [Utility Title]

## Task
[Single focused task]
Arguments: $ARGUMENTS

## Execution
[Simple steps]
```

### 5. Add Best Practices

Include in every command:
- Clear error handling instructions
- Security considerations if using Bash
- Validation of $ARGUMENTS if used
- Reference to documentation for complex features

### 6. Create the Command File

Write the complete command file with:
- Proper YAML frontmatter
- Clear sections with markdown headers
- Examples if helpful
- Links to related documentation

### 7. Provide Usage Instructions

After creating, show the user:
1. Command created at: `.claude/commands/<name>.md`
2. Usage: `/<name> [arguments]`
3. What the command does
4. Any special considerations
5. Link to documentation for customization

## Template Example

Here's a complete template for reference:

```markdown
---
description: Brief description here
argument-hint: [expected arguments]
allowed-tools: Tool1, Tool2
model: sonnet
---

# Command Title

## Overview
What this command does and why it's useful.

## Context
!`git status`
Current state: [describe]

## Requirements
- Requirement 1
- Requirement 2

## Implementation
Main task using $ARGUMENTS if needed.

## Validation
How to verify the command worked correctly.

## Related Documentation
- See: `.claude/docs/claude/slash-commands-guide.md`
```

## Important Guidelines

- **Security**: If allowing Bash, restrict to specific commands
- **Simplicity**: Follow KISS principle - one command, one purpose
- **Documentation**: Always reference the guides for users to learn more
- **Testing**: Suggest testing in personal commands first (`~/.claude/commands/`)
- **Naming**: Use descriptive, action-oriented names (e.g., `deploy-staging`, `review-pr`)

Now, create the slash command based on the provided arguments. If any required information is missing, ask for clarification.