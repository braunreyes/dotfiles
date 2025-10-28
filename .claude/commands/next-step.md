---
description: Suggest the next logical step in your current work
---

Analyze the current context and suggest the next logical step in the workflow.

## 1. Analyze Current State

### Check Working Directory Status

```bash
git status
```

**Look for**:
- Untracked files
- Modified files
- Staged files

### Review Recent Changes

```bash
git diff
```

**Identify**:
- What's been changed
- Incomplete implementations
- Comments like TODO, FIXME, NOTE

### Check for Incomplete Work

**In modified files**:
- Functions without implementations
- Missing error handling
- Incomplete docstrings
- TODO comments

---

## 2. Determine Workflow Stage

### Planning Stage

**Indicators**:
- No code changes yet
- Only documentation changes
- Architecture docs being written

**Next Step**:
→ Begin implementation or write detailed plan

---

### Implementation Stage

**Indicators**:
- Code files modified
- New functions/classes added
- Business logic being written

**Check**:
- Are tests written? → If NO, write tests next
- Is code documented? → If NO, add docstrings
- Are edge cases handled? → If NO, add error handling

**Next Step**:
→ Write tests (TDD) or complete implementation

---

### Testing Stage

**Indicators**:
- Test files modified
- Tests being written
- Coverage being checked

**Check**:
```bash
pytest -v
```

- Are tests passing? → If NO, fix failing tests
- Is coverage sufficient? → If NO, add more tests
- Are edge cases tested? → If NO, add edge case tests

**Next Step**:
→ Fix failing tests or improve coverage

---

### Documentation Stage

**Indicators**:
- README or docs being updated
- API documentation changes
- Comments being added

**Check**:
- Is code documented? → Docstrings, type hints
- Is API documented? → OpenAPI specs, examples
- Are changes documented? → CHANGELOG, decision logs

**Next Step**:
→ Complete documentation or create examples

---

### Quality Stage

**Indicators**:
- Refactoring in progress
- Performance optimization
- Code review feedback addressed

**Check**:
```bash
ruff check --fix .
ruff format .
mypy src/
```

**Next Step**:
→ Address quality issues or prepare for commit

---

## 3. Check Quality Gates

Run through this checklist:

### Code Quality

- [ ] **Linting**: `ruff check --fix .` → All issues resolved?
- [ ] **Formatting**: `ruff format .` → Code formatted?
- [ ] **Type Checking**: `mypy src/` → Type errors fixed?

### Testing

- [ ] **Tests Exist**: Do tests cover new/changed code?
- [ ] **Tests Pass**: `pytest -v` → All passing?
- [ ] **Coverage**: `pytest --cov` → Meets threshold (80%)?

### Documentation

- [ ] **Docstrings**: Functions/classes documented?
- [ ] **Type Hints**: All functions have type annotations?
- [ ] **README**: Updated if behavior changed?

### Git

- [ ] **Commits**: Changes committed with clear messages?
- [ ] **Branch**: Working on correct branch?
- [ ] **Up to date**: Pulled latest changes?

---

## 4. Consider Dependencies

### What Blocks Progress?

**Missing Requirements?**
- Need clarification from user?
- Waiting on external dependency?
- Need to install library?

**Technical Blockers?**
- Database schema not ready?
- API not implemented yet?
- Infrastructure not set up?

**Knowledge Gaps?**
- Need to research approach?
- Unfamiliar with library/pattern?
- Need to consult documentation?

---

## 5. Suggest Next Action

Based on the analysis, provide a clear, actionable next step:

### Format

```markdown
## Next Step: [Action]

**Why**: [Reasoning based on current state]

**What to Do**:
1. [Specific action 1]
2. [Specific action 2]
3. [Specific action 3]

**Estimated Time**: [X] minutes/hours

**Prerequisites** (if any):
- [Prerequisite 1]
- [Prerequisite 2]

**Expected Outcome**:
[What should be accomplished]

**Then What**:
[What comes after this step]
```

---

## Example Outputs

### Example 1: Need Tests

```markdown
## Next Step: Write Unit Tests for UserService

**Why**: You've implemented UserService.create_user() and UserService.update_user() but there are no tests yet. Following TDD principles and your config's `require_tests_before_commit: true`, tests should be written before marking this work complete.

**What to Do**:
1. Create `tests/unit/test_user_service.py`
2. Write tests for `create_user()`:
   - Happy path (valid input)
   - Validation errors (invalid email, missing fields)
   - Edge cases (duplicate user, empty strings)
3. Write tests for `update_user()`:
   - Update existing user
   - User not found error
   - Partial updates

**Estimated Time**: 45-60 minutes

**Prerequisites**:
- UserService implementation is complete
- Test fixtures for user data (can create alongside tests)

**Expected Outcome**:
- Comprehensive test coverage for UserService
- All tests passing
- Edge cases documented through tests

**Then What**:
- Check test coverage with `pytest --cov`
- If coverage ≥80%, proceed to documentation
- If < 80%, add more tests for uncovered branches
```

---

### Example 2: Fix Failing Tests

```markdown
## Next Step: Fix Failing Tests in test_api.py

**Why**: Running `pytest` shows 3 failing tests in tests/test_api.py. Tests must pass before proceeding to ensure no regressions.

**What to Do**:
1. Run failing tests with verbose output:
   ```bash
   pytest tests/test_api.py::test_create_user -vv
   ```
2. Analyze failure messages and stack traces
3. Fix the underlying issues (likely in src/api/routes.py)
4. Re-run tests to verify fixes
5. Run full test suite to ensure no new failures

**Estimated Time**: 30-45 minutes

**Expected Outcome**:
- All tests in test_api.py passing
- No regressions in other tests
- Understanding of what caused failures

**Then What**:
- If all tests pass, proceed to code quality checks
- Document any tricky bugs in development log
```

---

### Example 3: Complete Implementation

```markdown
## Next Step: Implement Authentication Middleware

**Why**: The API endpoints are ready, but authentication middleware is marked as TODO in src/middleware/auth.py:15. This is a blocker for testing the full authentication flow.

**What to Do**:
1. Open `src/middleware/auth.py`
2. Implement JWT token validation logic:
   - Extract token from Authorization header
   - Validate token signature
   - Check token expiry
   - Extract user info from claims
3. Handle errors gracefully:
   - Missing token → 401
   - Invalid token → 401
   - Expired token → 401
4. Add user context to request object

**Estimated Time**: 1-2 hours

**Prerequisites**:
- JWT library installed (`pip install pyjwt`)
- Secret key configured in environment

**Expected Outcome**:
- Functional authentication middleware
- Proper error responses
- User context available in endpoints

**Then What**:
- Write integration tests for authentication flow
- Test all protected endpoints
- Document authentication in API docs
```

---

### Example 4: Ready to Commit

```markdown
## Next Step: Commit Your Changes

**Why**: All quality gates are passing:
- ✅ Tests passing (23/23)
- ✅ Coverage at 87% (threshold: 80%)
- ✅ Linting clean
- ✅ Types checked
- ✅ Code formatted
- ✅ Documentation updated

**What to Do**:
1. Review your changes one more time:
   ```bash
   git diff --cached
   ```
2. Ensure commit message is clear and follows convention
3. Commit with co-author attribution:
   ```bash
   git commit -m "feat: add user authentication middleware

   Implement JWT-based authentication with token validation
   and refresh token support.

   🤖 Generated with Claude Code

   Co-Authored-By: Claude <noreply@anthropic.com>"
   ```

**Estimated Time**: 5-10 minutes

**Expected Outcome**:
- Clean commit with descriptive message
- Changes documented in git history

**Then What**:
- Push to remote branch
- Create pull request
- Or continue with next feature
```

---

### Example 5: Need Clarification

```markdown
## Next Step: Get Requirements Clarification

**Why**: The implementation in src/services/notification.py has a TODO comment: "Determine notification priority logic". This is ambiguous and could be implemented multiple ways.

**What to Do**:
1. Review the business requirements document (if exists)
2. Ask the user for clarification:
   - Should priority be user-configurable?
   - Should it be based on notification type?
   - Should it be time-sensitive?
3. Document the decision in development log
4. Update the TODO with specific implementation approach

**Estimated Time**: 15-30 minutes (including wait time)

**Blocked By**: Need business logic clarification

**Expected Outcome**:
- Clear understanding of priority logic
- Decision documented
- Ready to implement

**Then What**:
- Implement the clarified priority logic
- Add tests for various priority scenarios
```

---

## Integration with Other Tools

### After Suggesting Next Step

**If next step is write tests**:
```
@agents/pytest-expert.md, help me write tests for [component]
```

**If next step is implementation**:
```
@agents/python-professional.md, implement [feature]
```

**If next step is documentation**:
```
@agents/technical-writer.md, document [feature/API]
```

**If next step is refactoring**:
```
/find-refactor-candidates
```

### Use with Other Commands

**Before next-step**:
```
/does-it-work
```
(Validate current state)

**After completing next-step**:
```
/next-step
```
(Get next action)

---

## Tips

**For Long Tasks**:
- Break down "next step" into smaller chunks
- Aim for steps that take 1-2 hours max
- Create todos for multi-step work

**When Stuck**:
- Check for blockers
- Consider if you need help/clarification
- Look at what's preventing progress

**Maintain Momentum**:
- Always have a clear next action
- Don't let perfect be enemy of done
- Ship incremental progress

**Follow Your Workflow**:
- Respect quality gates (tests, linting, etc.)
- Don't skip steps to move faster
- Technical debt accumulates quickly
