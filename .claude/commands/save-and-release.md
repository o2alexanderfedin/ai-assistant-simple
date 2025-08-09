---
description: Commit, push, and release changes following gitflow conventions
argument-hint: [type] [description] (e.g., "feature add-user-auth" or "fix resolve-login-bug")
allowed-tools: Bash, Read, Glob
---

# Save and Release - Gitflow Automation

You will help commit, push, and release changes following gitflow conventions.

## Workflow Steps

### 1. Analyze Arguments
Parse the provided arguments: `$ARGUMENTS`
- First word should be the change type: `feature`, `fix`, `hotfix`, `release`, or `chore`
- Remaining words form the description
- If no arguments provided, analyze changes to determine type automatically

### 2. Determine Branch Strategy
Based on the type:
- **feature**: Create/use `feature/[description]` branch
- **fix**: Create/use `fix/[description]` branch  
- **hotfix**: Create/use `hotfix/[description]` branch
- **release**: Create/use `release/[version]` branch
- **chore**: Use current branch or `chore/[description]`

### 3. Pre-commit Checks
Run in parallel:
- `git status` to see uncommitted changes
- `git diff` to review changes
- Check current branch name
- Verify remote tracking

### 4. Stage and Commit
- Stage all changes with `git add .`
- Create semantic commit message:
  - **feature**: `feat: [description]`
  - **fix**: `fix: [description]`
  - **hotfix**: `hotfix: [description]`
  - **release**: `release: [version]`
  - **chore**: `chore: [description]`
- Include co-author attribution

### 5. Push to Remote
- If new branch, push with `-u origin [branch-name]`
- If existing branch, regular push
- Handle any merge conflicts if they arise

### 6. Create Pull Request (if applicable)
For feature/fix/hotfix branches:
- Use `gh pr create` with appropriate title and body
- Set base branch (main/master/develop as appropriate)
- Add labels if available

### 7. Release Actions (if release type)
For release branches:
- Create GitHub release with `gh release create`
- Generate release notes
- Tag the version

## Important Guidelines

- ALWAYS follow semantic versioning for releases
- NEVER force push unless explicitly requested
- Ensure commit messages are descriptive and follow conventional commits
- Check for pre-commit hooks and respect them
- If tests exist, mention they should be run before pushing

## Error Handling

If any step fails:
- Report the specific error
- Suggest resolution steps
- Do NOT proceed with subsequent steps

## Example Usage

```
/save-and-release feature user-authentication
/save-and-release fix login-validation-error
/save-and-release release v1.2.0
```

Remember: Quality over speed. Better to catch issues before pushing than to fix them after.