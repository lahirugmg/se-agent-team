# Skill: api-docs

**Type:** atomic

## Purpose

Write or update reference documentation for an API such that a developer can integrate with it without reading the source code or asking the implementer for clarification. API docs are a contract — they must be accurate, complete, and testable.

## When to Invoke

- A new API or endpoint has been implemented and needs reference documentation.
- An existing API has changed and the documentation no longer matches the implementation.
- An API is being consumed by external developers and its documentation needs to meet a higher standard of completeness.

## Workflow

1. **Read the implementation, not the old docs.** Docs written from memory or from old documentation accumulate errors. Read the source code, the OpenAPI spec (if one exists), and any integration tests to understand the actual behaviour.

2. **Document each endpoint.** For every endpoint:
   - **Method and path** — `POST /v1/orders`
   - **Description** — one sentence stating what this endpoint does and when to use it
   - **Authentication** — required auth scheme (Bearer token, API key, etc.)
   - **Request parameters** — path params, query params, and request body fields with: name, type, required/optional, constraints, and description
   - **Response** — status codes returned, and for each: the response body shape with all fields, types, and example values
   - **Error responses** — each error code, what triggers it, and what the response body contains
   - **Rate limits** — if applicable

3. **Provide examples.** For each endpoint, provide a complete request/response example in a format the reader can copy and run (curl, HTTP, or SDK example). An example without a response is half an example.

4. **Document authentication separately.** Authentication is used by every endpoint but documented nowhere visible if it's only mentioned inline. Give it its own section:
   - How to obtain credentials
   - How to include them in requests
   - Token lifetime and refresh process
   - What happens when authentication fails

5. **Document error codes as a reference.** A table of all error codes the API can return, with: code, HTTP status, description, and what the caller should do.

6. **Verify accuracy.** For every documented request/response, execute it against a running instance and confirm the documentation matches. Documentation that cannot be verified against reality is not done.

7. **Mark deprecated elements.** Any deprecated endpoint, parameter, or field must be clearly labelled with: what it is replaced by and when it will be removed.

## Output

- **Endpoint reference** — each endpoint documented with method, path, auth, parameters, responses, and examples
- **Authentication guide** — how to obtain, use, and rotate credentials
- **Error code reference** — all error codes with descriptions and remediation guidance
- **Changelog** — what changed in this version of the docs
