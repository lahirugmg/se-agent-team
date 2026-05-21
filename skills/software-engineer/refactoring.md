# Skill: refactoring

**Type:** atomic
**Scope:** Improve the internal structure of existing code without changing its observable behaviour.

## When to Invoke

- Code is correct but hard to read, test, or extend.
- Duplication exists that makes a future change require touching multiple places.
- Explicitly asked to refactor a specific area.

## Inputs

- The code to refactor.
- The stated motivation (readability, testability, reducing duplication, etc.).
- The test suite that must pass before and after.

## Constraints

- **Behaviour is frozen.** If the refactor changes what the code does, it's not a refactor — it's a change that also happens to move things around. Separate them.
- **No features during refactoring.** If you notice a missing feature, note it. Don't add it.
- **No standard changes.** Don't update dependencies, rename config keys, or touch unrelated files as part of a refactor.

## Procedure

1. **Confirm tests pass before starting.** Run the full relevant test suite. If tests are red before you touch anything, stop — you can't verify your refactor didn't break something.

2. **Define the goal.** State what structural problem you're solving: "this module has three callers that each duplicate the same null-check" or "this function is 200 lines and does three unrelated things."

3. **Refactor in small, verifiable steps.**
   - Extract one thing at a time.
   - Run tests after each step.
   - Commit at each green state. Small commits make it easy to revert a step without losing the whole refactor.

4. **Common moves:**
   - Extract function/method — pull repeated or complex logic into a named unit.
   - Inline — remove a function that adds indirection without clarity.
   - Rename — improve a name when its current form is misleading or too generic.
   - Move — relocate code to where it belongs by responsibility.
   - Reduce parameters — introduce a parameter object when a function takes many arguments.

5. **Confirm tests pass after every step.** If a step breaks a test, that step changed behaviour — investigate before proceeding.

6. **Clean up YOUR orphans.** Remove variables, imports, and functions made unused by your refactor. Don't remove pre-existing dead code unless that's the explicit goal.

## Output

- The refactored code.
- A brief statement of what changed structurally and why.
- Confirmation that all tests pass before and after.
- Any unrelated issues noticed but not addressed (list, don't fix).
