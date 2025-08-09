# Release Workflow

## Automated via /save-and-release
1. Check for uncommitted changes
2. Determine change type (feat/fix/chore)
3. Stage and commit changes
4. Check for unreleased commits
5. Calculate version bump:
   - feat → minor
   - fix → patch
   - BREAKING CHANGE → major
6. Update VERSION file
7. Create GitHub release
8. Push tags and changes

## Manual Release
1. Update VERSION file
2. Commit with "chore: bump version"
3. Create tag: `git tag v[version]`
4. Push tag: `git push --tags`
5. Create GitHub release via gh CLI