# Claude Code Configuration for Database Reliability Engineering

This directory contains custom commands, agents, and prompts for Claude Code, tailored for Database Reliability Engineering workflows with PostgreSQL.

## Structure

```
.claude/
├── commands/          # Slash commands for specific tasks
├── agents/           # Specialized agent personas
├── prompts/          # Programming paradigm references
├── config.yaml       # Configuration and preferences
└── README.md         # This file
```

## The Build Command - Your Starting Point

**`/build`** is your multi-purpose development orchestrator. Use it to start any new project, feature, or refactoring work.

### What it does:
1. Assesses what you want to build
2. Activates the **project-orchestrator** agent
3. Guides you through a complete TDD workflow
4. Delegates to specialized agents/commands at the right time
5. Teaches you which tools to use (builds muscle memory)

### Workflow Modes:
- **Strict Mode**: TDD enforced, all quality gates required (best for production)
- **Flexible Mode**: Guided recommendations, can skip steps (best for prototyping)

### Example Usage:
```bash
/build a PostgreSQL connection pooling library

# The orchestrator will:
# 1. Model domain with @ddd-designer
# 2. Set up project structure
# 3. Guide through TDD cycle with @python-tdd-coach
# 4. Review code with @clean-code-reviewer
# 5. Optimize if needed with @sql-optimizer
```

## Commands

Invoke commands with `/command-name` in Claude Code.

### Workflow Orchestration
- `/build` - **START HERE** - Multi-purpose orchestrator for projects/features

### Database Operations
- `/pg-replication` - Setup PostgreSQL logical replication with TDD approach
- `/pg-extensions` - Manage PostgreSQL extensions (pgvector, pg_cron, etc.)
- `/pg-users` - User and role management with security-first approach
- `/pg-cron` - Manage pg_cron jobs with monitoring
- `/pg-metrics` - Extract PostgreSQL metrics for observability
- `/pg-cdc-pipeline` - Build CDC pipelines from PostgreSQL to S3
- `/ai-agent-workflow` - Create AI-assisted database workflows

### Code Quality
- `/review-code` - Comprehensive code review focusing on DRE patterns
- `/refactor-code` - Refactor code applying SOLID and Clean Code principles

## Agents

Agents are specialized personas that provide domain expertise. The **project-orchestrator** automatically delegates to these agents at the right time, teaching you when to use each one.

### Orchestration
- **project-orchestrator** - Autonomous workflow manager (activated by `/build`)

### Domain Experts
- **dre-architect** - Database architecture and system design
- **python-tdd-coach** - Test-Driven Development guidance
- **sql-optimizer** - PostgreSQL query optimization
- **clean-code-reviewer** - Clean Code and SOLID principles review
- **ddd-designer** - Domain-Driven Design modeling

## Prompts

Reference documents for programming paradigms and best practices:

- **zen-of-python** - PEP 20 principles and Pythonic code
- **solid-principles** - SOLID design principles with examples
- **design-patterns** - Gang of Four patterns for database engineering
- **pythonic-idioms** - Python idioms and best practices
- **dry-principle** - Don't Repeat Yourself with refactoring techniques

## Configuration

Edit `.claude/config.yaml` to customize your workflow:

```yaml
default_mode: strict  # or flexible

testing:
  framework: pytest
  coverage_threshold: 80

quality:
  enforce_type_hints: true
  enforce_docstrings: true

orchestrator:
  ask_before_major_decisions: true
  build_muscle_memory: true  # Ask you to identify correct agent
```

See `config.yaml` for all available options including project templates, PostgreSQL defaults, and custom workflows.

## Usage Examples

### Starting a New Project (Recommended)
```bash
/build a user authentication service

# Orchestrator will guide you through:
# - Domain modeling
# - Project structure setup
# - TDD cycle (tests → implementation → refactor)
# - Code review and quality checks
# - Each step teaches you which agent/command to use
```

### Starting a New Feature in Existing Project
```bash
/build password reset functionality

# Orchestrator adapts to existing project:
# - Skips initialization
# - Goes straight to TDD cycle
# - Uses existing patterns and structure
```

### Database-Specific Task
```bash
/pg-replication

# Directly invoke specialized command
# For tasks that don't need full workflow
```

### Quick Code Review (Without Full Workflow)
```bash
/review-code

# Direct review without TDD cycle
# Useful for reviewing existing code
```

### Getting Architecture Guidance
```bash
# Either through /build or directly:
Ask the dre-architect agent:

I need to design a high-availability PostgreSQL setup for
a multi-region deployment. What architecture would you recommend?
```

### Learning Mode
```bash
# Orchestrator in "build muscle memory" mode will ask:
"Which agent would help with writing tests?"
> You: python-tdd-coach
"Correct! Let me consult them..."

# This builds your intuition for which tools handle what
```

## Programming Principles

All code should follow these principles:

1. **Test-Driven Development (TDD)** - Write tests first
2. **Zen of Python** - Beautiful, explicit, simple, readable code
3. **Clean Code** - Small functions, meaningful names, proper abstractions
4. **DRY** - Don't Repeat Yourself
5. **SOLID** - Single Responsibility, Open/Closed, Liskov Substitution, Interface Segregation, Dependency Inversion
6. **Gang of Four Patterns** - Use appropriate design patterns
7. **Domain-Driven Design** - Model the domain accurately

## Customization

Feel free to:
- Add new commands for your specific workflows
- Create additional agents for specialized domains
- Extend prompts with your team's conventions
- Modify existing files to match your preferences

## Workflow Overview

```
┌─────────────────────────────────────────────────────────┐
│                      /build command                      │
│           (Entry point - gathers context)                │
└─────────────────────┬───────────────────────────────────┘
                      │
                      ▼
┌─────────────────────────────────────────────────────────┐
│              project-orchestrator agent                  │
│         (Autonomous workflow management)                 │
└─────────────────────┬───────────────────────────────────┘
                      │
        ┌─────────────┼─────────────┐
        ▼             ▼             ▼
   ┌────────┐   ┌──────────┐   ┌──────────┐
   │Domain  │   │   TDD    │   │  Code    │
   │Modeling│   │  Cycle   │   │ Review   │
   └────┬───┘   └────┬─────┘   └────┬─────┘
        │            │              │
        │            │              │
        ▼            ▼              ▼
  ddd-designer  python-tdd-    clean-code-
                  coach          reviewer

  Other specialists:
  • dre-architect (architecture)
  • sql-optimizer (queries)
  • Specific /pg-* commands
```

## Best Practices

### Getting Started
1. **Use `/build` for projects and features** - It guides you through the complete workflow
2. **Choose your mode** - Strict for production, flexible for prototyping
3. **Let orchestrator teach you** - Pay attention to which agents handle what
4. **Trust the TDD cycle** - Tests first really works!

### During Development
1. Write tests before implementation (orchestrator enforces in strict mode)
2. Apply SOLID principles from the start
3. Use type hints and comprehensive docstrings
4. Implement proper error handling and logging
5. Make operations idempotent when possible
6. Document architectural decisions
7. Keep security in mind (credentials, SQL injection, etc.)

### Tool Selection
- **New work** → `/build` (full workflow)
- **DB-specific tasks** → `/pg-*` commands (specialized)
- **Quick review** → `/review-code` (no TDD cycle)
- **Architecture questions** → `@dre-architect` (direct consultation)
- **Query help** → `@sql-optimizer` (direct consultation)

## Contributing

As you discover new patterns or workflows:
1. Document them in the appropriate command/agent/prompt
2. Share with your team
3. Keep examples practical and based on real use cases

---

For more information about Claude Code configuration, visit:
https://docs.claude.com/en/docs/claude-code
