# Skill: technical-spec

**Type:** atomic

## Purpose

Write a technical specification that tells an engineering team exactly what to build and how — at the level of interfaces, data models, and behaviour — without leaving implementation decisions that require architectural input. The spec is the contract between the architect and the implementer.

## When to Invoke

- A design has been decided (including ADRs for significant choices) and implementation is about to begin.
- An engineering team needs a written agreement on what they are building before they start.
- A feature involves multiple components or teams and interface contracts must be agreed upfront.

## Workflow

1. **State the purpose.** In two to three sentences: what this spec describes, what it does NOT describe, and who the intended reader is. A spec for a backend engineer looks different from one for a platform team.

2. **Define the interfaces.** For each component or service boundary in scope:
   - API endpoints or function signatures
   - Request and response shapes (include field names, types, and nullability)
   - Error codes and error response shapes
   - Authentication requirements
   Interface definitions must be specific enough to generate client code from without further clarification.

3. **Define the data model.** For each entity stored or processed:
   - Field names, types, constraints, and defaults
   - Relationships to other entities
   - Indexing requirements
   - Data lifecycle (when is it created, modified, deleted, or expired?)

4. **Define the behaviour.** Describe what the system does in response to valid inputs, invalid inputs, and error conditions. Use GIVEN/WHEN/THEN format for clarity:
   ```
   GIVEN a user with role X
   WHEN they call endpoint Y with parameter Z
   THEN the system responds with HTTP 200 and body { ... }
   ```

5. **Define sequencing.** For multi-step operations, provide a sequence diagram or numbered steps showing the order of calls, state transitions, and side effects.

6. **Define error handling.** For each error condition:
   - What HTTP status or error code is returned
   - What the error response body contains
   - What state the system is left in (no side effects? partially applied? rolled back?)

7. **List implementation decisions.** Items the spec explicitly defers to the implementer, so they are not guessing what is in scope. Example: "The caching strategy for this endpoint is left to the implementing team."

8. **List open questions.** Items that require resolution before or during implementation, with owners.

## Output

- **Interface definitions** — API contracts with request/response shapes
- **Data model** — entities, fields, relationships, and lifecycle
- **Behaviour specification** — GIVEN/WHEN/THEN cases covering happy path and key error paths
- **Sequence diagrams** — for multi-step or multi-service operations
- **Implementation decisions** — explicit list of what is deferred to the team
- **Open questions** — with owners and deadlines
