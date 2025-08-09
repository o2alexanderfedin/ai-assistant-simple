# Agent Creation Workflow

## Via HR Manager
1. Invoke agent-hr-manager with task description
2. HR manager analyzes requirements
3. Searches existing agents
4. Creates new if <60% match

## Manual Creation
1. Create .md file in .claude/agents/
2. Add YAML frontmatter (name, description, model, tools)
3. Include mandatory sections:
   - Core Engineering Principles
   - Handling Uncertainties
   - Granular Update Philosophy
4. Write focused system prompt
5. Test agent functionality

## Quality Checks
- Single responsibility?
- Minimal tool selection?
- Clear documentation?
- Follows patterns?