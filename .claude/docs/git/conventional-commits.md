# Conventional Commits Reference

Guidelines for semantic commit messages that enable automated versioning and changelog generation.

## Format

```
<type>[optional scope]: <description>

[optional body]

[optional footer(s)]
```

## Commit Types

| Type | Description | Version Bump | Example |
|------|-------------|--------------|---------|
| `feat` | New feature | Minor (0.x.0) | `feat: add user authentication` |
| `fix` | Bug fix | Patch (0.0.x) | `fix: resolve login validation error` |
| `docs` | Documentation only | None | `docs: update API documentation` |
| `style` | Code style (formatting, semicolons) | None | `style: fix eslint warnings` |
| `refactor` | Code refactoring | None | `refactor: extract validation logic` |
| `perf` | Performance improvement | Patch | `perf: optimize database queries` |
| `test` | Add/update tests | None | `test: add unit tests for auth` |
| `build` | Build system changes | None | `build: update webpack config` |
| `ci` | CI/CD changes | None | `ci: add GitHub Actions workflow` |
| `chore` | Maintenance tasks | None | `chore: update dependencies` |
| `revert` | Revert previous commit | Varies | `revert: revert feat: add auth` |

## Breaking Changes

Mark breaking changes with `BREAKING CHANGE:` in footer or `!` after type:

```bash
# Using footer
feat: change API response format

BREAKING CHANGE: API now returns data in 'results' field instead of 'data'

# Using ! notation
feat!: remove deprecated endpoints
```

Breaking changes trigger major version bump (x.0.0).

## Scope Examples

Optional scope provides context:

```bash
feat(auth): add OAuth2 support
fix(api): handle null responses
docs(readme): add installation guide
build(deps): upgrade to React 18
```

## Commit Message Examples

### Feature Addition
```bash
feat: implement shopping cart functionality

- Add cart state management
- Create cart UI components
- Integrate with payment API

Closes #123
```

### Bug Fix
```bash
fix: prevent race condition in data fetching

The previous implementation could cause duplicate API calls
when components mounted rapidly. Added debouncing and
request cancellation.

Fixes #456
```

### Breaking Change
```bash
feat!: migrate to new authentication system

BREAKING CHANGE: JWT tokens now use RS256 instead of HS256.
All clients must update their token validation logic.

Migration guide: docs/migration/v2.md
```

## Version Bumping Rules

Based on commits since last release:

1. **Major (x.0.0)**: Any `BREAKING CHANGE` or `!`
2. **Minor (0.x.0)**: Any `feat` commits
3. **Patch (0.0.x)**: Any `fix` or `perf` commits
4. **No bump**: Only `docs`, `style`, `refactor`, `test`, `build`, `ci`, `chore`

## Footers

Standard footers:
- `Fixes #<issue>`: Closes issue
- `Closes #<issue>`: Closes issue
- `Refs #<issue>`: References issue
- `BREAKING CHANGE: <description>`: Breaking change
- `Reviewed-by: <name>`: Reviewer
- `Co-authored-by: <name> <email>`: Co-author

## Git Aliases for Conventional Commits

Add to `.gitconfig`:

```bash
[alias]
    # Conventional commit shortcuts
    cfeat = "!f() { git commit -m \"feat: $1\" \"${@:2}\"; }; f"
    cfix = "!f() { git commit -m \"fix: $1\" \"${@:2}\"; }; f"
    cdocs = "!f() { git commit -m \"docs: $1\" \"${@:2}\"; }; f"
    cstyle = "!f() { git commit -m \"style: $1\" \"${@:2}\"; }; f"
    crefactor = "!f() { git commit -m \"refactor: $1\" \"${@:2}\"; }; f"
    cperf = "!f() { git commit -m \"perf: $1\" \"${@:2}\"; }; f"
    ctest = "!f() { git commit -m \"test: $1\" \"${@:2}\"; }; f"
    cbuild = "!f() { git commit -m \"build: $1\" \"${@:2}\"; }; f"
    cci = "!f() { git commit -m \"ci: $1\" \"${@:2}\"; }; f"
    cchore = "!f() { git commit -m \"chore: $1\" \"${@:2}\"; }; f"
```

Usage:
```bash
git cfeat "add user profile page"
git cfix "resolve memory leak in dashboard"
```

## Integration with Git Flow

| Git Flow Type | Conventional Commit Type | Example |
|--------------|---------------------------|---------|
| feature | `feat:` | `feat: implement OAuth login` |
| bugfix | `fix:` | `fix: resolve validation error` |
| hotfix | `fix:` or `hotfix:` | `hotfix: patch security vulnerability` |
| release | `chore:` | `chore: prepare release 1.2.0` |

## Validation Tools

### commitlint
```bash
npm install --save-dev @commitlint/cli @commitlint/config-conventional
echo "module.exports = {extends: ['@commitlint/config-conventional']}" > commitlint.config.js
```

### Git Hook (with commitlint)
```bash
#!/bin/sh
# .git/hooks/commit-msg
npx --no-install commitlint --edit "$1"
```

## Best Practices

1. **Keep subject line under 50 characters**
2. **Use imperative mood** ("add" not "added" or "adds")
3. **Don't end subject with period**
4. **Separate subject from body with blank line**
5. **Wrap body at 72 characters**
6. **Explain what and why, not how**
7. **Reference issues and PRs**
8. **Group related changes in one commit**
9. **Make atomic commits** (one logical change per commit)