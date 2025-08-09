# Component Structure

## Core Components

### Agent System (.claude/agents/)
- **Responsibility**: Define specialized AI agents
- **Key Files**: agent-hr-manager.md, agent-software-engineer-in-test.md
- **Pattern**: YAML frontmatter + markdown prompt

### Command System (.claude/commands/)
- **Responsibility**: Custom slash commands
- **Key Files**: save-and-release.md, init-memory-bank.md
- **Pattern**: Argument parsing + workflow automation

### Memory System (.claude/memory/)
- **Responsibility**: Maintain project context
- **Structure**: Modular subdirectories with index aggregation
- **Pattern**: Hierarchical imports with @path syntax

### Version Control
- **VERSION file**: Semantic versioning tracker
- **Git integration**: Conventional commits, gitflow branches