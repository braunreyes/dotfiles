---
description: Analyze current tooling setup and suggest improvements based on best practices
---

Evaluate all slash commands and agents in this Claude Code setup against Anthropic's tool design principles, and provide actionable recommendations.

## Step 1: Inventory Current Tools

**List all slash commands**:
```bash
ls -la ~/.claude/commands/ | grep -v "^\." | awk '{print $NF}' | grep "\.md$"
```

**List all agents**:
```bash
ls -la ~/.claude/agents/ | grep -v "^\." | awk '{print $NF}' | grep "\.md$"
```

Group them by category:
- **Planning**: Commands/agents for feature planning and architecture
- **Code Quality**: Tools for linting, testing, refactoring
- **Database**: PostgreSQL-specific tools
- **Documentation**: Writing and maintaining docs
- **Workflow**: Process guidance and automation
- **Utilities**: General-purpose helpers

## Step 2: Evaluate Against Five Principles

For each tool, assess against Anthropic's principles:

### 1. Quality over Quantity
- Are there redundant or overlapping tools?
- Could multiple tools be consolidated?
- Is each tool serving a distinct, valuable purpose?

### 2. Namespacing
- Do related tools have consistent naming?
- Is grouping clear (e.g., `pg-*` for PostgreSQL)?
- Easy to distinguish similar tools?

### 3. Meaningful Context
- Commands: Do they guide agents to produce high-signal output?
- Agents: Do they focus on relevant, actionable information?
- Clear what each tool does from its name and description?

### 4. Token Efficiency
- Do commands encourage focused, targeted outputs?
- Are agents specialized enough to avoid loading unnecessary context?
- Any tools that might dump excessive information?

### 5. Purpose-Driven Design
- Do tools solve tasks like humans would?
- Are workflows natural and intuitive?
- Tools designed around tasks, not just technical operations?

## Step 3: Identify Issues and Opportunities

### Redundancies
Look for:
- Multiple tools doing similar things
- Commands that duplicate agent capabilities
- Overlapping PostgreSQL tools

### Gaps
Identify missing capabilities:
- Common workflows without dedicated tools?
- Frequently repeated tasks that could be automated?
- Integration opportunities (GitHub, CI/CD, etc.)?

### Low Quality
Find tools that violate principles:
- Poor naming or unclear purpose
- Overly broad or unfocused
- Missing important context
- Token inefficient

### Quick Wins
Low-effort, high-impact improvements:
- Simple renaming for clarity
- Adding descriptions to existing tools
- Consolidating obvious duplicates
- Better command namespacing

## Step 4: Provide Structured Report

Present findings in this format:

```markdown
# Tool Analysis Report

**Date**: [Current date]
**Total Commands**: [N]
**Total Agents**: [N]

---

## Executive Summary

[2-3 sentence overview of current state and key findings]

**Overall Health Score**: [1-5 ⭐]

---

## Current Tooling Inventory

### Slash Commands (by Category)

**Planning** ([N] tools):
- /plan-feature - [Brief assessment]
- ...

**Code Quality** ([N] tools):
- /does-it-work - [Brief assessment]
- ...

**Database** ([N] tools):
- /pg-users - [Brief assessment]
- ...

**[Other categories]** ...

### Agents (by Category)

**Development** ([N] agents):
- python-professional.md - [Brief assessment]
- ...

**Architecture** ([N] agents):
- software-planner.md - [Brief assessment]
- ...

**[Other categories]** ...

---

## Principle Evaluation

### 1. Quality over Quantity: [Score 1-5]

**Findings**:
- [Observations about tool count and overlap]

**Issues**:
- [Specific redundancies or overlaps identified]

**Recommendations**:
- [Consolidation opportunities]

### 2. Namespacing: [Score 1-5]

**Findings**:
- [Observations about naming consistency]

**Good Patterns**:
- [Examples of good namespacing]

**Issues**:
- [Inconsistencies or unclear naming]

**Recommendations**:
- [Naming improvements]

### 3. Meaningful Context: [Score 1-5]

**Findings**:
- [Assessment of how tools guide output quality]

**Strengths**:
- [Well-designed tools]

**Issues**:
- [Tools that could be clearer]

**Recommendations**:
- [Improvements to descriptions or guidance]

### 4. Token Efficiency: [Score 1-5]

**Findings**:
- [Assessment of agent specialization and output focus]

**Strengths**:
- [Efficient tools]

**Issues**:
- [Overly broad or verbose tools]

**Recommendations**:
- [Optimization opportunities]

### 5. Purpose-Driven Design: [Score 1-5]

**Findings**:
- [Assessment of task-oriented vs. technical-oriented design]

**Strengths**:
- [Well-designed workflows]

**Issues**:
- [Tools that feel like raw API wrappers]

**Recommendations**:
- [Redesign suggestions]

---

## Specific Issues Found

### 🔴 High Priority (Fix Now)

**Issue 1**: [Description]
- **Impact**: [Why this matters]
- **Recommendation**: [Specific fix]
- **Effort**: [Low/Medium/High]

### 🟡 Medium Priority (Fix Soon)

**Issue 1**: [Description]
- **Impact**: [Why this matters]
- **Recommendation**: [Specific fix]
- **Effort**: [Low/Medium/High]

### 🔵 Low Priority (Nice to Have)

**Issue 1**: [Description]
- **Impact**: [Small improvement]
- **Recommendation**: [Optional enhancement]
- **Effort**: [Low/Medium/High]

---

## Identified Gaps

Missing capabilities that would be valuable:

1. **[Gap Name]**
   - **Need**: [What's missing]
   - **Use Case**: [When you'd use it]
   - **Recommendation**: [Command or agent to create]
   - **Priority**: [High/Medium/Low]

2. **[Next gap]** ...

---

## Quick Wins

Easy improvements with immediate impact:

1. **[Quick Win 1]**
   - **Change**: [What to do]
   - **Benefit**: [Why it helps]
   - **Effort**: 5-30 minutes

2. **[Quick Win 2]** ...

---

## Consolidation Opportunities

Tools that could be combined:

### Consolidation 1: [Name]

**Current State**:
- [Tool 1] - Does X
- [Tool 2] - Does Y
- [Tool 3] - Does Z

**Proposed**:
- [New unified tool] - Does X, Y, Z with clear parameters

**Benefits**:
- Fewer tools to remember
- More powerful combined functionality
- Reduced context overhead

**Trade-offs**:
- Slightly more complex interface
- Need to update existing workflows

**Recommendation**: [Do it / Consider it / Skip it]

---

## Agent Specialization Review

Are agents appropriately specialized?

**Well-Specialized** ✅:
- [Agent name]: [Why it's good]

**Too Broad** ⚠️:
- [Agent name]: [How to narrow]

**Too Narrow** ⚠️:
- [Agent name]: [Could expand or consolidate]

---

## Recommended Actions

### Immediate (This Week)

1. **[Action 1]** - [Brief description]
   - Priority: High
   - Effort: [Time estimate]
   - Impact: [Expected benefit]

2. **[Action 2]** ...

### Short Term (This Month)

1. **[Action 1]** - [Brief description]
   - Priority: Medium
   - Effort: [Time estimate]
   - Impact: [Expected benefit]

### Long Term (When Needed)

1. **[Action 1]** - [Brief description]
   - Priority: Low
   - Effort: [Time estimate]
   - Impact: [Expected benefit]

---

## Integration Suggestions

Tools that should reference each other:

- **[Tool A]** → Should mention **[Tool B]** for [reason]
- **[Agent X]** → Should delegate to **[Agent Y]** when [situation]

---

## Documentation Needs

Tools that need better documentation:

1. **[Tool name]**: Missing [what documentation]
2. **[Tool name]**: Unclear [what to clarify]

Suggested updates to `~/.claude/agents.md` or `~/.claude/docs/`:
- [Specific documentation to add]

---

## Conclusion

**Overall Assessment**: [Summary of current state]

**Strengths**: [What's working well]

**Areas for Improvement**: [Key themes]

**Next Step**: [Single most important action to take]

---

## Follow-Up

For detailed tool design work, consult:
```
@agents/tool-designer.md, [specific design request]
```

For implementation:
```
@agents/python-professional.md, implement [tool changes]
```

For documentation updates:
```
@agents/technical-writer.md, update [documentation]
```
```

---

## Integration

This command provides a starting point. For deeper analysis or custom tool design:

```
@agents/tool-designer.md, I ran /analyze-tools and here are the findings: [paste report]

Please help me:
1. Design [specific new tool]
2. Refactor [problematic tool]
3. Create MCP integration for [service]
```

---

**Note**: This command performs a health check. It doesn't make changes—it provides actionable intelligence so you can decide what to improve.
