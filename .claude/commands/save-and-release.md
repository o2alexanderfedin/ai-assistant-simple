---
description: Commit, push, and release changes using gitflow extension
argument-hint: [type] [name] (e.g., "feature user-auth" or "hotfix login-bug")
allowed-tools: Bash, Read, Glob
---

# Save and Release - Gitflow Automation

You will help commit, push, and release changes using the git-flow extension.

## Prerequisites
- Git Flow extension is installed (`git flow` commands available)
- Repository is initialized with `git flow init` (assume default branch names)

## Workflow Steps

### 1. Analyze Arguments and Repository State
Parse the provided arguments: `$ARGUMENTS`
- First word should be the flow type: `feature`, `bugfix`, `hotfix`, `release`, or `support`
- Remaining words form the name/version
- If no arguments provided:
  - Check if there are uncommitted changes to process
  - If working tree is clean, check for unreleased commits on develop
  - If unreleased commits exist, automatically create a release

### 2. Git Flow Branch Operations
Based on the type, use git flow commands:

**Feature**: Development of new features
```bash
git flow feature start [name]    # Start new feature from develop
git flow feature finish [name]   # Merge back to develop
git flow feature publish [name]  # Push feature to remote
```

**Bugfix**: Fix bugs in develop branch
```bash
git flow bugfix start [name]     # Start bugfix from develop
git flow bugfix finish [name]    # Merge back to develop
```

**Hotfix**: Emergency fixes to production
```bash
git flow hotfix start [version]  # Start from master/main
git flow hotfix finish [version] # Merge to both master and develop
```

**Release**: Prepare new production release
```bash
git flow release start [version]  # Start from develop
git flow release finish [version] # Merge to master and develop, create tag
```

**Support**: Long-term support branches
```bash
git flow support start [version] [base]  # Start support branch
```

### 3. Pre-operation Checks
Run these checks before any git flow operation:
- `git status` to see uncommitted changes
- `git flow config` to verify git flow is initialized
- Check current branch with `git branch --show-current`
- Verify no existing flow of same type with `git flow [type] list`
- Read VERSION file if it exists (for version determination)

### 4. Commit Workflow
For features/bugfixes with uncommitted changes:
1. Stage all changes with `git add .`
2. Create semantic commit message:
   - **feature**: `feat: [description]`
   - **bugfix**: `fix: [description]`
   - **hotfix**: `hotfix: [description]`
   - **release**: `chore: prepare release [version]`
3. Include co-author attribution

### 5. Git Flow Operations

**Starting a flow**:
1. Ensure working tree is clean (commit any changes first)
2. Use `git flow [type] start [name]`
3. Make commits as needed
4. Use `git flow [type] publish [name]` to push to remote

**Finishing a flow**:
1. Ensure all changes are committed
2. Use `git flow [type] finish [name]`
3. For releases/hotfixes: Enter tag message when prompted
4. Push all branches and tags: `git push --all && git push --tags`

### 6. Auto-Release Logic
When called without arguments and on develop branch:
1. Check for unreleased commits since last tag
2. Analyze commits to determine version bump:
   - `feat:` commits → minor version bump
   - `fix:` commits → patch version bump
   - `BREAKING CHANGE:` → major version bump
3. Start release with `git flow release start [version]`
4. Update VERSION file
5. Commit VERSION change
6. Finish release with `git flow release finish [version]`
7. Push all changes and tags

### 7. GitHub Release Creation
After finishing a release or hotfix:
1. The git flow finish creates a tag automatically
2. Push tags with `git push --tags`
3. Create GitHub release: `gh release create v[version] --generate-notes`

## Important Guidelines

- Git flow manages branch creation/deletion automatically
- NEVER manually create feature/release/hotfix branches
- Always use `git flow [type] finish` to properly merge and tag
- Features merge to develop, releases/hotfixes merge to both master and develop
- Version tags are created automatically by git flow release/hotfix finish

## Error Handling

If any step fails:
- Check if git flow is initialized: `git flow init`
- Verify you're not already in a flow: `git flow [type] list`
- Ensure working directory is clean before starting flows
- For merge conflicts during finish: Resolve and continue

## Example Usage

```bash
# Start and work on a feature
/save-and-release feature user-authentication

# Fix a bug in develop
/save-and-release bugfix validation-error

# Emergency fix to production
/save-and-release hotfix 1.2.1

# Create a release from develop
/save-and-release release 1.3.0

# Auto-detect and release
/save-and-release
```

## Git Flow Branch Model

```
master/main (production)
    ↑
    ├── hotfix branches (emergency fixes)
    ↑
develop (integration)
    ↑
    ├── feature branches (new features)
    ├── bugfix branches (bug fixes)
    └── release branches (release preparation)
```

Remember: Let git flow manage the complexity of branching and merging.