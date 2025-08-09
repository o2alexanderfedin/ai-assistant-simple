# Slash Commands Quick Reference

## Creating a Command

1. Create `.md` file in `.claude/commands/`
2. Filename = command name (e.g., `deploy.md` → `/deploy`)
3. Add optional YAML frontmatter
4. Write prompt in markdown body

## Frontmatter Cheat Sheet

```yaml
---
description: One-line description for /help menu
argument-hint: [optional] <required> | alternative
allowed-tools: Bash, Read, Write, Edit, Grep, Glob, LS
model: opus | sonnet | haiku
---
```

## Tool Restrictions

```yaml
# Allow all tools (default)
# (no allowed-tools specified)

# Allow specific tools only
allowed-tools: Read, Write, Edit

# Allow specific bash commands
allowed-tools: Bash(git:*), Bash(npm test)

# Complex restrictions
allowed-tools: Bash(git add:*), Read(./src/*), Write(./output/*)
```

## Special Syntax

| Syntax | Purpose | Example |
|--------|---------|---------|
| `$ARGUMENTS` | Insert command arguments | `Fix issue #$ARGUMENTS` |
| `` !`command` `` | Execute bash before prompt | `` !`git status` `` |
| `@filepath` | Include file contents | `@src/main.js` |
| `/` in path | Create namespaces | `git/commit.md` → `/git/commit` |

## Command Locations

| Location | Scope | Shows as | Version Control |
|----------|-------|----------|-----------------|
| `.claude/commands/` | Project | `(project)` | ✅ Yes |
| `~/.claude/commands/` | Personal | `(user)` | ❌ No |

## Common Patterns

### Basic Command
```markdown
---
description: Run tests
---
Run all tests and fix any failures
```

### With Arguments
```markdown
---
description: Create feature branch
argument-hint: [feature-name]
---
Create branch: feature/$ARGUMENTS
```

### With Bash Execution
```markdown
---
allowed-tools: Bash(git:*)
---
Current status: !`git status`
Create appropriate commit
```

### With File Reference
```markdown
---
description: Review PR
---
Review changes in @src/feature.js
```

### Restricted Tools
```markdown
---
allowed-tools: Read, Edit
model: haiku
---
Refactor code (no file creation)
```

## Model Selection

| Model | Use Case | Speed | Cost |
|-------|----------|-------|------|
| `haiku` | Simple tasks | Fast | Low |
| `sonnet` | General purpose | Medium | Medium |
| `opus` | Complex analysis | Slow | High |

## Directory Structure Example

```
.claude/commands/
├── commit.md           # /commit
├── review.md           # /review
├── git/
│   ├── sync.md        # /git/sync
│   └── pr.md          # /git/pr
├── test/
│   ├── unit.md        # /test/unit
│   └── e2e.md         # /test/e2e
└── deploy/
    ├── staging.md     # /deploy/staging
    └── prod.md        # /deploy/prod
```

## Built-in Commands

| Command | Purpose |
|---------|---------|
| `/help` | Show available commands |
| `/clear` | Clear conversation |
| `/review` | Review files or code |
| `/model` | Switch AI model |
| `/think` | Extended thinking mode |
| `/thinker` | Toggle thinking visibility |

## Debugging Tips

1. **Command not found?**
   - Check file location
   - Verify `.md` extension
   - Restart Claude Code

2. **Frontmatter issues?**
   - Validate YAML syntax
   - Check `---` delimiters
   - Remove special characters

3. **Tools not working?**
   - Verify tool names
   - Check allowed-tools syntax
   - Test with broader permissions

4. **Arguments not substituting?**
   - Use exact `$ARGUMENTS`
   - Case-sensitive
   - No spaces around

## Security Best Practices

✅ **DO:**
- Restrict tools to minimum needed
- Use specific bash commands
- Validate argument usage
- Limit file access paths

❌ **DON'T:**
- Allow unrestricted `Bash`
- Include sensitive data
- Use overly broad file patterns
- Skip validation of inputs

## Examples Repository

Check `.claude/commands/` in this project for real examples:
- `save-and-release.md` - Complex git workflow
- `init-memory-bank.md` - Project initialization

## Quick Command Template

```markdown
---
description: TODO: Brief description
argument-hint: TODO: [expected-args]
allowed-tools: TODO: List needed tools
model: sonnet
---

# Task Title

## Context
TODO: Gather necessary context
!`echo "Bash commands here"`

## Requirements
TODO: Define what needs to be done
- Requirement 1
- Requirement 2

## Implementation
TODO: Main prompt instructions using $ARGUMENTS if needed

## Validation
TODO: How to verify success
```

Copy and customize this template for new commands!