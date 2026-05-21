# Skill: migration

**Type:** atomic
**Scope:** Plan and execute a migration — schema, data, API, or infrastructure — with rollback capability and verified correctness.

## When to Invoke

- A database schema must change in a way that affects existing data.
- Data must be moved from one shape, location, or system to another.
- An API is being versioned and old consumers must be migrated.
- Infrastructure or configuration is moving to a new format.

## Inputs

- What is being migrated: from what state, to what state.
- Scale: approximate record count, data volume, or number of affected consumers.
- Constraints: downtime budget, rollback requirements, consistency guarantees.

## Principles

- **Migrations are irreversible in practice.** Even with rollback scripts, rolled-back migrations that touched production data create cleanup work. Design to go forward, not back.
- **Prove correctness on a sample before running at scale.** A migration that fails at record 900,000 is worse than one that fails at record 10.
- **Zero-downtime migrations require multiple steps.** Adding a NOT NULL column to a live table cannot be done in one step. Plan the multi-phase approach.

## Procedure

### Phase 1: Design

1. Define the before state and after state precisely. Write it down. This becomes the acceptance criterion.
2. Identify every consumer of the thing being migrated (tables, APIs, config keys).
3. Write the rollback plan before writing the migration. If you can't articulate how to undo it, you don't understand the migration yet.
4. Estimate scope: rows, bytes, consumers, estimated duration at expected throughput.

### Phase 2: Write

1. Write the migration script. For schema migrations, use the project's migration tool (Alembic, Flyway, Rails migrations, etc.).
2. Write the rollback script. Test both together.
3. For large data migrations, write the script to be resumable: checkpoint progress, skip already-migrated records, log counts.
4. For API migrations, write the compatibility shim first — old callers must keep working until they're updated.

### Phase 3: Test

1. Run against a copy of production data (or a representative sample). Never first-run a migration directly on production.
2. Verify correctness on a sample: spot-check records before and after.
3. Measure actual duration on the sample. Extrapolate to estimate full runtime.
4. Run the rollback on the test environment. Confirm the system returns to the original state.

### Phase 4: Execute

1. Communicate the plan and timing to affected teams before running.
2. Take a backup if the migration is destructive and one isn't already scheduled.
3. Monitor progress. Have the rollback script ready to run, not just written.
4. Verify correctness after completion: row counts, spot checks, dependent system checks.

## Output

- Migration plan document: before/after state, affected systems, rollback plan, timing estimate.
- The migration script(s).
- The rollback script(s).
- Post-migration verification checklist.
- Actual outcome after execution: records migrated, duration, any anomalies.
