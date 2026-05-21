# Skill: dependency-update

**Type:** atomic
**Scope:** Update one or more project dependencies safely, with verification that nothing regressed.

## When to Invoke

- A dependency has a known security vulnerability.
- Routine maintenance update cycle.
- A new feature requires a newer version of an existing dependency.
- CI reports a failing security advisory scan.

## Inputs

- The dependency or dependencies to update (name + current version + target version).
- The reason for updating (security, feature, maintenance).
- The test suite to use for regression verification.

## Procedure

1. **Read the changelog.** For every version between current and target, read the release notes. Look for:
   - Breaking changes to APIs the project uses.
   - Behaviour changes that might silently affect existing code.
   - New dependencies introduced transitively.

2. **Update one dependency at a time** unless they are tightly coupled (e.g., peer dependencies that must move together). Batch updates make regressions hard to isolate.

3. **Check for transitive impact.** A major version update often changes transitive dependencies too. Review the lockfile diff, not just the direct dependency.

4. **Run the full test suite.** A passing test suite is necessary but not sufficient — also:
   - Start the application and exercise the paths that use the updated dependency.
   - Check for deprecation warnings that indicate future breakage.
   - Review type signature changes if the project uses types.

5. **Update internal usages if the API changed.** If the update deprecates or removes an API, update all call sites now — don't leave deprecated usage for later.

6. **Security updates ship fast.** For CVE-driven updates, prioritise speed over perfect test coverage. Merge the update, then improve test coverage for the affected path.

## Output

- A summary of changes: dependency name, old version, new version, why updated.
- Changelog highlights relevant to this project.
- Confirmation that tests pass.
- Any deprecated API usages updated or flagged for follow-up.
- Any breaking changes encountered and how they were resolved.

## What Not to Do

- Don't update a dependency to its latest version "just to stay current" without reading the changelog.
- Don't batch all dependencies into one PR — it makes rollback painful.
- Don't skip testing because "it's just a patch version" — patch versions can still change behaviour.
