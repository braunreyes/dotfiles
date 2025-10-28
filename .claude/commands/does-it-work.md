---
description: Quick diagnostic to verify code works
---

Run comprehensive checks to validate the code is working correctly.

## 1. Syntax Check

Verify Python syntax is valid:

```bash
python -m py_compile src/**/*.py 2>&1 | head -20
```

**What this checks**:
- No syntax errors
- Files can be parsed
- Basic Python validity

**If errors**: Fix syntax errors before proceeding

---

## 2. Import Check

Try importing main modules:

```bash
python -c "import sys; sys.path.insert(0, 'src'); import $(basename $PWD)"
```

**What this checks**:
- Modules can be imported
- No missing dependencies
- Import structure is correct

**Common issues**:
- Missing `__init__.py` files
- Circular imports
- Missing dependencies in venv

**If errors**: Fix import issues or install missing dependencies

---

## 3. Linting

Check code quality:

```bash
ruff check --fix .
```

**What this checks**:
- PEP 8 compliance
- Common code issues
- Unused imports/variables
- Potential bugs

**Note**: `--fix` will auto-fix many issues

---

## 4. Formatting

Ensure consistent code style:

```bash
ruff format .
```

**What this does**:
- Formats all Python files
- Ensures consistent style
- Makes code more readable

---

## 5. Type Checking

Validate type hints:

```bash
mypy src/
```

**What this checks**:
- Type hint correctness
- Type mismatches
- Missing type annotations (if configured)

**Common issues**:
- Missing return types
- Incompatible types
- Untyped function calls

**If errors**: Add/fix type hints

---

## 6. Run Tests

Execute test suite:

```bash
pytest -v
```

**What this checks**:
- All tests passing
- No regressions
- Expected behavior intact

**For more details**:
```bash
pytest -vv --tb=short
```

**Check coverage**:
```bash
pytest --cov=src --cov-report=term-missing
```

---

## 7. Quick Smoke Test

If applicable, try running the application:

### For FastAPI Applications

```bash
# Start server in background
uvicorn main:app --host 127.0.0.1 --port 8000 &
SERVER_PID=$!

# Give it time to start
sleep 2

# Test health endpoint
curl -s http://localhost:8000/health || curl -s http://localhost:8000/ || echo "No response"

# Cleanup
kill $SERVER_PID 2>/dev/null
```

### For CLI Applications

```bash
python -m src.main --help
```

### For Libraries

```bash
python -c "from src import main_module; print(main_module.__version__)"
```

---

## Report Format

Present results in this structure:

```markdown
# Diagnostics Report

## Summary

- **Status**: ✅ All Clear | ⚠️ Warnings | ❌ Errors
- **Date**: [timestamp]
- **Branch**: [git branch]

---

## Results

### ✅ Syntax Check
All files parse successfully

### ✅ Import Check
All modules import correctly

### ⚠️ Linting (12 issues)
**Auto-fixed**:
- Removed 8 unused imports
- Fixed 3 line length issues

**Remaining**:
- src/api/routes.py:45 - Complexity too high (consider refactoring)

### ✅ Formatting
Code formatted successfully

### ❌ Type Checking (3 errors)
**Errors**:
1. src/services/user.py:23 - Missing return type annotation
   ```python
   def get_user(id: int):  # Add -> Optional[User]
   ```

2. src/api/routes.py:67 - Incompatible types
   ```python
   user_id: int = request.query_params.get("id")  # Returns str, not int
   ```

3. src/models/user.py:12 - Untyped function call

### ✅ Tests (23/23 passing)
**Coverage**: 87% (threshold: 80%)

**Uncovered lines**:
- src/utils/helper.py:45-48 (error handling branch)
- src/services/notification.py:89 (edge case)

### ⚠️ Smoke Test
**API Started**: ✅
**Health Check**: ❌ (404 - endpoint may not exist)

---

## Next Steps

### Critical (Fix Now)
1. Fix type errors in user.py and routes.py
2. Add type annotation to models/user.py

### Important (Fix Soon)
3. Refactor complex function in routes.py:45
4. Consider adding health endpoint

### Optional (Nice to Have)
5. Improve test coverage for edge cases
6. Add tests for error handling branches

---

## Quick Fixes

### Fix Type Errors

**File**: src/services/user.py:23
```python
# Before
def get_user(id: int):
    return db.query(User).filter(User.id == id).first()

# After
def get_user(id: int) -> Optional[User]:
    return db.query(User).filter(User.id == id).first()
```

**File**: src/api/routes.py:67
```python
# Before
user_id: int = request.query_params.get("id")

# After
user_id_str = request.query_params.get("id")
if user_id_str is None:
    raise HTTPException(status_code=400, detail="Missing id parameter")
user_id: int = int(user_id_str)
```
```

---

## Examples of Different Scenarios

### Example 1: Everything Works

```markdown
# Diagnostics Report

## Summary
✅ **All Clear** - Everything is working!

## Results
- ✅ Syntax: Valid
- ✅ Imports: Working
- ✅ Linting: Clean (0 issues)
- ✅ Formatting: Formatted
- ✅ Types: No errors
- ✅ Tests: 45/45 passing (94% coverage)
- ✅ Smoke Test: API responding correctly

## Next Steps
None! Ready to commit or deploy.
```

---

### Example 2: Tests Failing

```markdown
# Diagnostics Report

## Summary
❌ **Errors Found** - Tests failing

## Results
- ✅ Syntax: Valid
- ✅ Imports: Working
- ✅ Linting: Clean
- ✅ Formatting: Formatted
- ✅ Types: No errors
- ❌ Tests: 42/45 passing (3 failures)

## Failing Tests

### test_user_service.py::test_create_user_duplicate
```
AssertionError: Expected IntegrityError, got None
```
**Issue**: Duplicate user detection not working

**Location**: src/services/user.py:34
**Fix**: Add unique constraint check before insert

### test_api.py::test_authentication_invalid_token
```
HTTPException not raised
```
**Issue**: Invalid tokens are not being rejected

**Location**: src/middleware/auth.py:18
**Fix**: Add token validation logic

### test_utils.py::test_email_validation
```
AssertionError: False != True
```
**Issue**: Email validation regex not matching valid emails

**Location**: src/utils/validators.py:12
**Fix**: Update regex pattern

## Next Steps
1. Fix duplicate user detection (HIGH PRIORITY)
2. Add token validation (HIGH PRIORITY)
3. Fix email regex (MEDIUM PRIORITY)
4. Re-run tests after fixes
```

---

### Example 3: Import Errors

```markdown
# Diagnostics Report

## Summary
❌ **Critical Errors** - Cannot import modules

## Results
- ✅ Syntax: Valid
- ❌ Imports: Failed

## Import Errors

```
ModuleNotFoundError: No module named 'fastapi'
```

**Cause**: Dependencies not installed

**Fix**:
```bash
pip install -r requirements.txt
```

**Or if using poetry**:
```bash
poetry install
```

## Next Steps
1. Install dependencies (BLOCKING)
2. Re-run diagnostics after install
```

---

## Integration with Other Commands

### Before Committing

```
/does-it-work
```
(Verify everything works)

```
git add .
git commit -m "..."
```

### After Making Changes

```
/does-it-work
```
(Quick validation)

### As Part of Workflow

```
/next-step
```
(Suggests: Fix failing tests)

```
/does-it-work
```
(Verify fix worked)

---

## Configuration

Customize for your project structure:

**For different source directory**:
```bash
python -m py_compile project_name/**/*.py
mypy project_name/
pytest tests/
```

**For monorepo**:
```bash
ruff check --fix packages/*/src/
pytest packages/*/tests/
```

**For specific test suite**:
```bash
pytest tests/integration/ -v
```

---

## Tips

**Run frequently**: After any significant changes

**Fix issues early**: Don't let errors accumulate

**Automate**: Add to pre-commit hooks

**Understand failures**: Don't just fix, understand why

**Keep fast**: Should run in < 30 seconds for quick feedback
