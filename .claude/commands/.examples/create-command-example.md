# Example: Using /create-command

This file demonstrates how to use the `/create-command` slash command.

## Basic Usage

```
/create-command review-pr "Review pull request for best practices"
```

This creates a simple command with:
- Name: `review-pr`
- Description: "Review pull request for best practices"
- Tools: Inherits all (no restriction)
- Model: Inherits from conversation

## With Tool Restrictions

```
/create-command test-runner "Run tests and fix failures" "Bash,Read,Edit" 
```

This creates a command that can only use Bash, Read, and Edit tools.

## With Model Selection

```
/create-command analyze-security "Deep security analysis" "Read,Grep" opus
```

This creates a command that:
- Uses only Read and Grep tools
- Forces the opus model for complex analysis

## Advanced Example

```
/create-command deploy-staging "Deploy current branch to staging environment" "Bash,Read" sonnet
```

Creates a deployment command with:
- Restricted to Bash and Read tools only
- Uses sonnet model for efficiency
- Clear purpose from the description

## Command Types

When you run `/create-command`, it will ask you what type of command:

1. **Workflow Command**: Multi-step processes
   - Example: deployment, release automation
   
2. **Analysis Command**: Review and audit tasks
   - Example: security review, code quality check
   
3. **Generation Command**: Create new content
   - Example: documentation generator, boilerplate creator
   
4. **Utility Command**: Simple tools
   - Example: format converter, quick calculations

## After Creation

The command will:
1. Create the file at `.claude/commands/<name>.md`
2. Show you how to use it
3. Provide links to documentation for customization

## Tips

- Start with simple commands and add complexity
- Test in `~/.claude/commands/` first (personal)
- Move to `.claude/commands/` when ready (project)
- Use descriptive names with hyphens
- Keep descriptions concise but clear

## See Also

- Full documentation: `.claude/docs/claude/slash-commands-guide.md`
- Quick reference: `.claude/docs/claude/slash-commands-quick-reference.md`
- Existing commands: `.claude/commands/`