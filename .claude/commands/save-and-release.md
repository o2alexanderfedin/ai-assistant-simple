---
description: Commit, push, and release changes following gitflow conventions
argument-hint: [type] [description] (e.g., "feature add-user-auth" or "fix resolve-login-bug")
allowed-tools: Bash, Read, Glob
---

# Save and Release - Gitflow Automation

You will help commit, push, and release changes following gitflow conventions.

## Workflow Steps

### 1. Analyze Arguments and Repository State
Parse the provided arguments: `$ARGUMENTS`
- First word should be the change type: `feature`, `fix`, `hotfix`, `release`, or `chore`
- Remaining words form the description
- If no arguments provided:
  - Check if there are uncommitted changes to process
  - If working tree is clean, check for unreleased commits on main branch
  - If unreleased commits exist, automatically create a release

### 2. Determine Branch Strategy
Based on the type:
- **feature**: Create/use `feature/[description]` branch
- **fix**: Create/use `fix/[description]` branch  
- **hotfix**: Create/use `hotfix/[description]` branch
- **release**: Create/use `release/[version]` branch
- **chore**: Use current branch or `chore/[description]`

### 3. Pre-commit/Release Checks
Run in parallel:
- `git status` to see uncommitted changes
- `git diff` to review changes  
- Check current branch name
- Verify remote tracking
- Read VERSION file if it exists (or default to 0.0.0)
- Check latest tag with `git describe --tags --abbrev=0` (compare with VERSION file)
- Check for unreleased commits with `git log [latest-tag]..HEAD --oneline`

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

### 7. Release Actions (if release type or auto-release)
For release branches or when auto-releasing from main:
- Read current version from VERSION file (or use 0.0.0 if not exists)
- Determine next version number based on commit types:
  - `feat:` commits → minor version bump
  - `fix:` commits → patch version bump  
  - `BREAKING CHANGE:` or `!:` → major version bump
- Update VERSION file with new version number
- Commit VERSION file with message: `chore: bump version to [version]`
- Create GitHub release with `gh release create v[version] --generate-notes`
- Tag the version as v[version]
- Push the VERSION file update
- If on main branch with clean working tree and no arguments, auto-release unreleased commits

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
/save-and-release  # Auto-detect: commits changes or creates release
```

## Auto-Release Logic

When called without arguments on main branch with clean working tree:
1. Check VERSION file for current version (create if not exists)
2. Check for existing tags/releases
3. If unreleased commits exist since last tag:
   - Analyze commit messages to determine version bump type
   - Calculate new version number
   - Update VERSION file
   - Commit the VERSION file change
   - Create appropriate version tag and GitHub release
4. If no unreleased commits, report that everything is up to date

## VERSION File Format

The VERSION file should contain a single line with the semantic version:
```
1.2.3
```
(without 'v' prefix - the prefix is added when creating tags/releases)

Remember: Quality over speed. Better to catch issues before pushing than to fix them after.