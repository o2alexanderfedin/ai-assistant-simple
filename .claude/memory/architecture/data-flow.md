# Data Flow

## Agent Creation Flow
1. User requests specialized agent via HR manager
2. HR manager analyzes task requirements
3. Searches existing agents in .claude/agents/
4. Creates new agent if <60% match
5. Returns agent configuration path

## Command Execution Flow
1. User invokes slash command with arguments
2. Command parses $ARGUMENTS
3. Executes workflow steps
4. Reports results to user

## Memory Loading Flow
1. Claude Code starts session
2. Loads CLAUDE.md from project root
3. Recursively imports @referenced files
4. Builds context from memory hierarchy
5. Max recursion depth: 5 levels