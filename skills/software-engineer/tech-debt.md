# Skill: tech-debt

**Type:** atomic
**Scope:** Identify, assess, and create an actionable plan for technical debt in a codebase or subsystem.

## When to Invoke

- Asked to assess the health of a codebase or module.
- Before a major refactor or feature build in an unfamiliar area.
- During a quarterly or sprint planning cycle.
- After a production incident caused by brittleness in existing code.

## Inputs

- The codebase, module, or area to assess.
- Any known pain points or incidents to prioritise.
- Context on upcoming work that the debt may affect.

## Debt Categories

| Category | Examples |
|---|---|
| **Code quality** | Functions too long, poor naming, missing abstractions, duplicated logic |
| **Test coverage** | Critical paths untested, tests that don't verify intent, flaky tests |
| **Architecture** | Wrong layer handling logic, circular dependencies, missing separation of concerns |
| **Dependencies** | Outdated packages, deprecated APIs, abandoned libraries |
| **Documentation** | Missing runbooks, out-of-date READMEs, undocumented invariants |
| **Security** | Known vulnerabilities, hardcoded secrets, unvalidated inputs that have survived |
| **Performance** | Known bottlenecks that are tolerated but not addressed |

## Procedure

1. **Survey the area.** Read the code, look at recent git history, check issue trackers, ask maintainers. Debt that isn't visible in the code shows up in commit messages and bug history.

2. **List concrete items.** Vague entries like "the auth module is messy" are not actionable. Concrete entries name the file, describe the specific problem, and explain the cost.

3. **Assess each item on two dimensions:**
   - **Cost to fix:** effort in hours or days.
   - **Cost of NOT fixing:** risk of incidents, velocity drag, difficulty of upcoming features.

4. **Prioritise.** Debt that intersects upcoming work rises to the top. Debt that has never caused a problem and won't affect planned work can wait.

5. **Propose disposition for each item:**
   - Fix now (blocking)
   - Fix this sprint (high cost of delay)
   - Schedule (known, tracked, backlogged)
   - Accept (cost of fixing exceeds benefit)

6. **Create tickets.** Debt that lives only in a document gets forgotten. Convert prioritised items into tracked work items.

## Output

A structured debt register with:

```
Item: [name]
Location: [file:line or module]
Problem: [what's wrong]
Cost to fix: [hours/days]
Cost of not fixing: [risk or velocity impact]
Disposition: fix-now / schedule / accept
```

Followed by a prioritised list of the top 3–5 items to address next and a recommendation on whether to block upcoming feature work on any of them.
