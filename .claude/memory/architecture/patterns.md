# Design Patterns

## Pattern: Agent Specialization
- **Used in**: All agent definitions
- **Purpose**: Single responsibility for each agent
- **Implementation**: Each agent focuses on ONE domain (HR, SDET, etc.)

## Pattern: YAML Frontmatter Configuration
- **Used in**: Agent and command definitions
- **Purpose**: Declarative configuration separate from logic
- **Implementation**: Name, description, tools in frontmatter

## Pattern: Markdown-based DSL
- **Used in**: Agents, commands, memory files
- **Purpose**: Human-readable, version-controllable configuration
- **Implementation**: .md files with structured content