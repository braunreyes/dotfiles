---
description: Identify files that are good candidates for refactoring using various metrics
---

Analyze the codebase for refactoring candidates using these metrics:

## 1. Code Complexity

**Large Files**:
- Find files over 300 lines
- Files over 500 lines are high priority

**Functions Per File**:
- Count functions per file
- More than 10 functions suggests splitting needed

**Cyclomatic Complexity**:
- Identify functions with high complexity
- Use tools like radon (Python) if available

## 2. Change Frequency (Git History)

**Most Frequently Modified**:
```bash
git log --format=format: --name-only | grep -E '\.(py|js|ts)$' | sort | uniq -c | sort -rn | head -20
```

**Files with Multiple Contributors**:
- Files modified by 5+ people may have consistency issues
- Potential merge conflict hotspots

**Recent "Hot Spots"**:
- Files changed in last 30 days
- High churn indicates potential issues

## 3. Code Smells

**Long Lines**:
- Lines over 100 characters (Python PEP 8 suggests 79-88)
- Indicates complex expressions or deep nesting

**Duplicate Code**:
- Look for similar code blocks
- Use tools or manual inspection
- High duplication = refactoring opportunity

**TODO/FIXME Comments**:
```bash
grep -r "TODO\|FIXME\|HACK\|XXX" --include="*.py" .
```

**Deeply Nested Conditionals**:
- More than 3 levels of nesting
- Indicates complex logic that needs extraction

## 4. Static Analysis

**Linting**:
```bash
ruff check --fix .
```

**Formatting**:
```bash
ruff format .
```

**Type Checking**:
```bash
mypy src/
```

**Common Issues**:
- Unused imports
- Unused variables
- Missing type hints
- Complex expressions

## 5. Test Coverage

**Low Coverage Files**:
- Files with <80% coverage
- Critical business logic with no tests

**Files with No Tests**:
- Production code without corresponding test file
- High risk for regressions

## Output Format

Present findings in this structure:

```markdown
# Refactoring Candidates Analysis

## Executive Summary
- Total files analyzed: X
- High priority candidates: Y
- Medium priority candidates: Z

## High Priority (Refactor Soon)

### File: path/to/file.py
**Issues**:
- Lines: 650 (threshold: 300)
- Functions: 23 (threshold: 10)
- Changed: 45 times (top 5%)
- Contributors: 8 people
- Coverage: 45% (threshold: 80%)
- Code smells: 12 TODO comments, deep nesting

**Recommendation**: Split into multiple modules by responsibility

**Estimated effort**: 4-6 hours

---

### File: path/to/another.py
**Issues**:
- Cyclomatic complexity: Very High
- No tests
- Changed 30 times in last month

**Recommendation**: Add comprehensive tests first, then refactor

**Estimated effort**: 6-8 hours

## Medium Priority (Plan for Later)

[Similar format for medium priority files]

## Low Priority (Monitor)

[Files with minor issues]

## Quick Wins

These can be fixed quickly (< 1 hour each):
- Fix TODO comments in file1.py
- Add type hints to file2.py
- Extract duplicate code in file3.py and file4.py

## Recommendations

1. **Start with**: [highest priority file]
2. **Add tests to**: [files without tests]
3. **Monitor**: [files with medium issues]
4. **Technical debt items**: [Create issues for tracking]
```

## Analysis Tips

**For Python Projects**:
- Use `radon cc src/` for complexity metrics
- Use `radon mi src/` for maintainability index
- Check `pytest --cov` output for coverage gaps

**Prioritization Factors**:
1. **High churn + Low tests** = Highest priority (risky)
2. **Large + Complex** = High priority (hard to maintain)
3. **Many contributors** = Medium priority (inconsistency)
4. **Code smells only** = Low priority (cosmetic)

**Before Refactoring**:
- Ensure tests exist (or write them first)
- Create refactoring plan
- Get code review for major changes
- Refactor incrementally, not all at once

## Integration with Other Agents

After analysis:
- Use `@agents/refactoring-specialist.md` to plan refactoring approach
- Use `@agents/pytest-expert.md` to add missing tests first
- Use `@agents/code-reviewer.md` to review refactoring changes
- Use `@agents/development-chronicler.md` to document refactoring iterations
