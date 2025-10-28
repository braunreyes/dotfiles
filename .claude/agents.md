---
description: Agent catalog and selection guide
---

# Agent Catalog

Quick reference for all available agents and when to use them.

## Core Engineering

### @agents/core-engineering.md

**Description**: Foundational engineering principles (SOLID, design patterns, best practices)

**Use when**:
- Making architectural decisions
- Choosing design patterns
- Establishing code quality standards
- General software engineering questions

**Expertise**: SOLID, DRY, KISS, design patterns, testing philosophy, security, operational excellence

---

## Language & Framework Specialists

### @agents/python-professional.md

**Description**: Modern Python development (3.9+), FastAPI, async patterns

**Use when**:
- Writing Python code
- Building FastAPI applications
- Working with async/await
- Using Pydantic for validation
- Need Python best practices
- Type hints and modern Python features

**Expertise**: Modern Python (3.11+), type hints, FastAPI, async patterns, PEP 8, dataclasses, Pydantic

---

### @agents/pytest-expert.md

**Description**: Python testing specialist

**Use when**:
- Writing tests
- Debugging test failures
- Designing fixtures
- Improving test coverage
- Test organization and structure
- Mocking and patching

**Expertise**: pytest, fixtures, mocking, test organization, coverage, parametrization, test-driven development

---

## Database Specialists

### @agents/postgres-operations.md

**Description**: PostgreSQL database operations and administration

**Use when**:
- Designing database schemas
- Writing migrations
- Database administration tasks
- PostgreSQL-specific features
- Connection pooling and management

**Expertise**: PostgreSQL, schema design, migrations, administration, replication, extensions

---

### @agents/sql-optimizer.md

**Description**: SQL query optimization and performance tuning

**Use when**:
- Slow queries need optimization
- Designing indexes
- Analyzing query plans
- Performance tuning
- Query complexity analysis

**Expertise**: Query optimization, EXPLAIN plans, indexing strategies, performance analysis

---

## Planning & Architecture

### @agents/software-planner.md

**Description**: Strategic software planning and architecture design

**Use when**:
- Planning new features or projects
- Making architectural decisions
- Designing system components
- Creating implementation roadmaps
- Analyzing quality attributes (performance, security, scalability)
- Risk identification and mitigation

**Expertise**: Requirements analysis, architecture patterns, Domain-Driven Design, quality attributes, ADRs, modern tech stack (2025)

---

## Documentation & Communication

### @agents/technical-writer.md

**Description**: Technical documentation specialist using proven frameworks

**Use when**:
- Writing README files
- Creating API documentation
- Writing tutorials or guides
- Improving documentation quality
- Need OpenAPI/Swagger specs
- Ensuring accessibility (WCAG 2.2)

**Expertise**: Diátaxis framework, SUCCESS framework, EPPO, OpenAPI 3.1, AsyncAPI, Markdown standards, accessibility, docs-as-code

---

### @agents/development-chronicler.md

**Description**: Document development process, decisions, and learnings

**Use when**:
- Made a significant technical decision
- Completed an iteration or refactoring
- Solved a complex problem
- Want to preserve context for future developers
- Need to generate CHANGELOG entries
- Conducting retrospectives

**Expertise**: Decision logs, iteration documentation, learning capture, problem-solution narratives, retrospectives, CHANGELOG generation

---

## Quality & Tooling

### @agents/code-reviewer.md

**Description**: Comprehensive code review specialist focusing on quality, security, and best practices

**Use when**:
- Reviewing code changes or pull requests
- Need systematic quality assessment
- Checking for security vulnerabilities
- Ensuring adherence to project standards
- Want structured, constructive feedback
- Teaching through code review

**Expertise**: Code review methodology, quality assessment (functionality, testing, security, performance), structured feedback, language-specific best practices (Python, FastAPI)

---

### @agents/tool-designer.md

**Description**: Expert in designing ergonomic tools for AI agents following Anthropic's best practices

**Use when**:
- Creating new slash commands or agents
- Reviewing existing tools for improvements
- Designing MCP integrations for external services
- Need to consolidate overlapping tools
- Optimizing tool token efficiency
- Applying Anthropic's tool design principles

**Expertise**: Tool design principles (quality over quantity, namespacing, meaningful context, token efficiency, purpose-driven), MCP specifications, tool evaluation, workflow optimization

---

## Decision Matrix

| Task Type | Primary Agent | Supporting Agents |
|-----------|--------------|-------------------|
| New Feature Planning | software-planner | python-professional, pytest-expert, technical-writer |
| Python Implementation | python-professional | pytest-expert, core-engineering |
| Bug Fix | python-professional | pytest-expert, development-chronicler |
| Refactoring | python-professional | pytest-expert, development-chronicler |
| API Design | software-planner | python-professional, technical-writer |
| Database Schema | postgres-operations | software-planner, sql-optimizer |
| Query Performance | sql-optimizer | postgres-operations, python-professional |
| Testing | pytest-expert | python-professional |
| Documentation | technical-writer | software-planner, python-professional |
| Architecture Design | software-planner | core-engineering |
| Process Documentation | development-chronicler | software-planner, technical-writer |
| Code Review | code-reviewer | python-professional, pytest-expert |
| Tool Design | tool-designer | software-planner, python-professional |

---

## Agent Selection by Complexity

### Simple Tasks

**Single file, clear requirements**:
- Use primary language agent (`python-professional`)
- No need for planning agents
- Quick, focused implementation

**Examples**:
- Add a utility function
- Fix a typo
- Update a docstring

### Medium Tasks

**Multiple files, some complexity**:
- Start with `software-planner` for quick design
- Use specialist agents for implementation
- Use `pytest-expert` for tests
- Use `development-chronicler` to document decisions

**Examples**:
- Add new API endpoint
- Refactor a module
- Implement new business logic

### Complex Tasks

**Architectural changes, multiple components**:
- **Must start** with `software-planner`
- Use multiple specialist agents in sequence
- Document decisions with `development-chronicler`
- Create comprehensive documentation with `technical-writer`

**Examples**:
- New feature with multiple endpoints
- Database schema changes
- Authentication/authorization system
- Performance optimization project

---

## Agent Selection by Phase

### Planning Phase

**Primary**: `@agents/software-planner.md`
- Requirements analysis
- Architecture design
- Implementation roadmap
- Risk assessment

**Supporting**:
- `@agents/core-engineering.md` - Design patterns
- `@agents/postgres-operations.md` - Database design
- `@agents/technical-writer.md` - API spec design

---

### Implementation Phase

**Primary**: `@agents/python-professional.md`
- Write production code
- Follow best practices
- Implement features

**Supporting**:
- `@agents/core-engineering.md` - SOLID principles
- `@agents/postgres-operations.md` - Database operations
- `@agents/development-chronicler.md` - Document iterations

---

### Testing Phase

**Primary**: `@agents/pytest-expert.md`
- Design test strategy
- Write comprehensive tests
- Debug test failures
- Improve coverage

**Supporting**:
- `@agents/python-professional.md` - Test code quality
- `@agents/development-chronicler.md` - Document test learnings

---

### Optimization Phase

**For Database**: `@agents/sql-optimizer.md`
- Query optimization
- Index design
- Performance analysis

**For Code**: `@agents/python-professional.md`
- Code optimization
- Async patterns
- Profiling analysis

---

### Documentation Phase

**User-Facing**: `@agents/technical-writer.md`
- README
- API documentation
- Tutorials
- User guides

**Development Process**: `@agents/development-chronicler.md`
- Decision logs
- Iteration documentation
- Retrospectives
- CHANGELOG

---

## Token Usage Optimization

Using specialized agents reduces token usage by **60-80%**:

**Example**:
- **General Claude**: ~50,000 tokens loaded per request
- **Specialized agent**: ~10,000-15,000 tokens loaded
- **Savings**: 76%

### Best Practices

1. **Always use the most specific agent** that can handle the task
2. **Chain agents** for complex work (plan → implement → test → document)
3. **Don't use multiple agents** when one will suffice
4. **Invoke explicitly** with `@agents/[name].md` syntax

### Common Mistakes

❌ **Don't**:
- Use general Claude for tasks a specialist can handle
- Invoke agents you don't need
- Ask one agent to do another agent's job

✅ **Do**:
- Choose the most specific agent
- Use supporting agents when appropriate
- Trust agents to delegate when needed

---

## Quick Selection Guide

### "I need to..."

**"...plan a new feature"**
→ `@agents/software-planner.md` (previously `/plan-feature` command)

**"...write Python code"**
→ `@agents/python-professional.md`

**"...write tests"**
→ `@agents/pytest-expert.md`

**"...design a database schema"**
→ `@agents/postgres-operations.md`

**"...optimize a slow query"**
→ `@agents/sql-optimizer.md`

**"...write documentation"**
→ `@agents/technical-writer.md`

**"...document a decision"**
→ `@agents/development-chronicler.md`

**"...understand design patterns"**
→ `@agents/core-engineering.md`

**"...review code quality"**
→ `@agents/code-reviewer.md` (previously `/review-code` command)

**"...design new tools or improve existing ones"**
→ `@agents/tool-designer.md`

**"...work with PostgreSQL"**
→ `@agents/postgres-operations.md` (previously `/pg-*` commands)

**"...refactor code"**
→ `@agents/python-professional.md` + `@agents/code-reviewer.md` (previously `/refactor-code` command)

---

## Commands vs. Agents

We maintain a **lean set of 4 commands** for specific workflows. For everything else, use agents directly.

### The 4 Essential Commands

1. **`/analyze-tools`** - Health check of your tooling setup
   - Scans commands and agents
   - Evaluates against best practices
   - Provides structured recommendations

2. **`/does-it-work`** - Quick validation workflow
   - Syntax check, imports, linting, formatting
   - Type checking, tests, smoke tests
   - Structured diagnostic report

3. **`/find-refactor-candidates`** - Metric-based code analysis
   - Complexity metrics (file size, function count, cyclomatic complexity)
   - Git history (change frequency, hot spots)
   - Code smells (long lines, duplication, nesting)

4. **`/next-step`** - Workflow guidance
   - Analyzes current state (git, files, tests)
   - Suggests next logical action
   - Context-aware recommendations

### When to Use Commands

Commands are for **repeatable workflows** that combine multiple tool calls or produce structured output. For everything else, invoke agents directly.

**Command**: Multi-step process with defined output
**Agent**: Deep expertise, flexible consultation

### Migrating from Deleted Commands

| Old Command | New Approach |
|-------------|--------------|
| `/review-code` | `@agents/code-reviewer.md, review [code/PR]` |
| `/refactor-code` | `@agents/python-professional.md, refactor [component]` |
| `/plan-feature` | `@agents/software-planner.md, plan [feature description]` |
| `/pg-users` | `@agents/postgres-operations.md, help with user management` |
| `/pg-extensions` | `@agents/postgres-operations.md, manage extensions` |
| `/pg-replication` | `@agents/postgres-operations.md, setup replication` |
| `/pg-cron` | `@agents/postgres-operations.md, manage pg_cron jobs` |
| `/pg-metrics` | `@agents/postgres-operations.md, extract metrics` |
| `/pg-cdc-pipeline` | `@agents/postgres-operations.md, setup CDC pipeline` |

**Why this change?** Following Anthropic's "Quality over Quantity" principle - fewer, more powerful tools are better than many redundant ones. Agents provide more flexibility and deeper expertise.

---

## Creating New Agents

### When to Create a New Agent

Create a new specialized agent when:
- **Domain expertise** needed repeatedly
- **Token usage** is high for common tasks
- **Consistent methodology** required
- **Specific framework** or technology focus

### Don't Create When

- Task is one-time or rare
- Existing agent can handle it
- Domain is too broad
- Better as a slash command

### Use `/create-new-agent` Command

```
/create-new-agent
```

This will guide you through creating a properly structured agent.

---

## Agent Inheritance

Many agents inherit from `@agents/core-engineering.md`:

```
core-engineering.md (base principles)
    ↓
    ├── python-professional.md
    ├── software-planner.md
    ├── technical-writer.md
    ├── development-chronicler.md
    ├── code-reviewer.md
    └── tool-designer.md
```

**What inheritance means**:
- Inheriting agents follow core-engineering principles
- No need to repeat SOLID, DRY, etc.
- Focus on specialized expertise
- Consistent quality standards

---

## Integration Patterns

### Sequential (Pipeline)

Use agents in sequence for end-to-end workflows:

```
1. @agents/software-planner.md (plan)
   ↓
2. @agents/python-professional.md (implement)
   ↓
3. @agents/pytest-expert.md (test)
   ↓
4. @agents/technical-writer.md (document)
   ↓
5. @agents/development-chronicler.md (retrospective)
```

---

### Parallel (Multiple Specialists)

Use multiple agents for different aspects:

```
@agents/python-professional.md (application code)
    +
@agents/postgres-operations.md (database code)
    =
Complete feature
```

---

### Consultation

One agent consults another:

```
@agents/technical-writer.md
    ↓ (consults for accuracy)
@agents/python-professional.md
```

---

## Maintenance

### Keep This Catalog Updated

When you add a new agent:
1. Add entry to appropriate section
2. Update decision matrix
3. Update quick selection guide
4. Add to integration patterns if relevant

### Review Quarterly

- Are agents still relevant?
- Do descriptions match current behavior?
- Are there new agents needed?
- Can any agents be merged?

---

## Examples

### Example 1: Building a New API Feature

```
Step 1: Plan
@agents/software-planner.md, plan an API for user notifications

Step 2: Implement
@agents/python-professional.md, implement the notification API based on the plan

Step 3: Database
@agents/postgres-operations.md, create the database schema for notifications

Step 4: Test
@agents/pytest-expert.md, create comprehensive tests for the notification API

Step 5: Document
@agents/technical-writer.md, write API documentation for the notification endpoints

Step 6: Chronicle
@agents/development-chronicler.md, document the key decisions we made
```

---

### Example 2: Performance Optimization

```
Step 1: Identify Issues
/find-refactor-candidates

Step 2: Analyze Queries
@agents/sql-optimizer.md, analyze these slow queries and suggest optimizations

Step 3: Implement Optimizations
@agents/python-professional.md, implement the query optimizations

Step 4: Verify
@agents/pytest-expert.md, add performance tests to ensure improvements

Step 5: Document
@agents/development-chronicler.md, document the performance improvements and metrics
```

---

### Example 3: Bug Fix

```
Step 1: Diagnose
@agents/python-professional.md, help me debug this issue

Step 2: Test
@agents/pytest-expert.md, create a regression test for this bug

Step 3: Document
@agents/development-chronicler.md, document this problem-solution narrative
```

---

## Tips for Success

1. **Start with planning agents** for non-trivial work
2. **Use specialist agents** for their domains
3. **Document as you go** with development-chronicler
4. **Chain agents** for complex workflows
5. **Trust agent delegation** - they know when to defer to others
6. **Keep token usage in mind** - more specific = fewer tokens
7. **Update this catalog** when you add agents

---

**Remember**: The right agent at the right time maximizes efficiency and quality. When in doubt, start with `@agents/software-planner.md` for complex tasks or `@agents/python-professional.md` for straightforward Python work.
