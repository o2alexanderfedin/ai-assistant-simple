# Common Pitfalls

## Issue: Agents recreating entire files
- **Symptom**: Agent rewrites whole test suite for one test fix
- **Cause**: Not following granular update philosophy
- **Solution**: Enforce Edit/MultiEdit for targeted changes

## Issue: Tool bloat in agents
- **Symptom**: Agent has many unused tools
- **Cause**: Not analyzing actual tool needs
- **Solution**: HR manager must justify each tool

## Issue: Monolithic memory files
- **Symptom**: Single file with all conventions
- **Cause**: Not following SOLID principles
- **Solution**: Split into focused subdirectories