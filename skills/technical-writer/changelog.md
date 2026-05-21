# Skill: changelog

**Type:** atomic

## Purpose

Write a structured changelog entry for a release or significant change that tells readers what changed, why it matters to them, and what they need to do — in terms they understand. A changelog is for readers, not for developers reviewing commits.

## When to Invoke

- A version is being released and the changelog needs to be updated before announcement.
- A significant breaking change needs to be communicated with migration guidance.
- A security fix has been shipped and the changelog entry needs to meet a disclosure standard.

## Workflow

1. **Gather inputs.** Collect:
   - The git log or PR list since the last release
   - The release notes or PR descriptions
   - Any breaking changes or deprecations
   - Any security fixes with CVE identifiers (if applicable)
   Do not write from memory. Write from the diff.

2. **Filter for significance.** Not every commit belongs in a changelog. Include:
   - New features or capabilities
   - Changed behaviour that affects existing users
   - Bug fixes that affected users
   - Security fixes
   - Deprecated features (with removal timeline)
   - Removed features (with migration path)
   Exclude: internal refactors, test improvements, documentation updates (unless they fix known misinformation), dependency updates with no user-visible impact.

3. **Group by type.** Use the Keep a Changelog convention:
   - **Added** — new features
   - **Changed** — changes to existing functionality
   - **Deprecated** — features that will be removed in a future release
   - **Removed** — features removed in this release
   - **Fixed** — bug fixes
   - **Security** — fixes for vulnerabilities

4. **Write each entry for the reader.** Each entry describes the impact on the user, not the implementation:
   - Good: "The export button now generates a CSV file instead of a JSON file, matching the format expected by the reporting tool."
   - Bad: "Changed ExportController to emit CSV instead of JSON."

5. **Write breaking change entries with full context.** For any breaking change:
   - What changed
   - Who is affected (which users or integrations)
   - What the user must do to migrate (specific steps, not "update your configuration")
   - When the old behaviour was or will be removed

6. **Write security entries carefully.** For security fixes:
   - Include the CVE identifier if one has been assigned
   - Describe the vulnerability class (e.g. "authenticated users could access other users' data") without providing a detailed exploit
   - State which versions are affected and which version contains the fix
   Follow the project's responsible disclosure policy.

7. **Date and version the entry.** Every changelog entry must have a version number and a release date. Unreleased changes belong in an "Unreleased" section that is renamed on release.

## Output

- **Changelog entry** — versioned, dated, grouped by type, written for the reader
- **Breaking change guidance** — migration steps for each breaking change
- **Security disclosure section** — following the project's disclosure policy, with CVE identifiers where applicable
