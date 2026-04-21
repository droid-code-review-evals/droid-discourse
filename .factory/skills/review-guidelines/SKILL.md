# Review Guidelines - File-by-File Deep Analysis

## IMPORTANT: Review each file TWICE

For every modified file in the diff:

### Pass 1 - Line-by-line read
Read every changed line and understand what it does. Do not skim. For each line ask:
- What value does this variable hold at this point?
- What type is this expression?
- What happens if this is null/None/undefined?

### Pass 2 - Cross-reference
For each function/method changed:
- Find ALL callers in the diff. Do they pass correct arguments?
- Find ALL implementations of interfaces/abstract methods. Do they match?
- Check if any imports/exports changed that affect other files in the diff.

### Key patterns to hunt for
- Class/module-level expressions evaluated at import time (datetime.now(), [], {})
- Feature flags that are always true or always false due to logic errors
- Wrong variable referenced when two similar names exist in scope
- Return value from a function that was changed but callers not updated
- Test assertions that don't actually test the intended behavior
