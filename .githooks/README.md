# Git Hooks

This directory contains git hooks for enforcing gitflow conventions.

## Installation

To install these hooks locally, run:

```bash
# Set git to use this directory for hooks
git config core.hooksPath .githooks

# Or copy individual hooks to .git/hooks/
cp .githooks/pre-commit .git/hooks/pre-commit
chmod +x .git/hooks/pre-commit
```

## Hooks

### pre-commit

Prevents direct commits to protected branches (main/master/develop) and enforces gitflow usage.

**Features:**
- Blocks commits to main, master, and develop branches
- Provides clear gitflow command reminders
- Acts as prompt injection for Claude to enforce gitflow
- Allows emergency bypass with `--no-verify` flag

**Protected branches:**
- main
- master  
- develop

**Allowed branches:**
- feature/*
- bugfix/*
- hotfix/*
- release/*
- Any other custom branches

## Gitflow Reminder

When a commit is blocked, the hook displays:

```
**GITFLOW SCOPE MUST BE USED**

You MUST use git flow commands instead of direct commits:
- git flow feature start/finish
- git flow bugfix start/finish
- git flow hotfix start/finish
- git flow release start/finish
```

This message serves as a prompt injection for Claude, ensuring AI assistants follow gitflow conventions.