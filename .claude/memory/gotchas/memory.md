# Memory System Gotchas

## Issue: Import recursion limit
- **Symptom**: Memory not loading completely
- **Cause**: More than 5 levels of imports
- **Solution**: Flatten import hierarchy

## Issue: Large memory files
- **Symptom**: Slow context loading
- **Cause**: Files over 100 lines
- **Solution**: Split into smaller modules

## Issue: Stale memories
- **Symptom**: Outdated instructions being followed
- **Cause**: Not updating memory with changes
- **Solution**: Regular memory audits