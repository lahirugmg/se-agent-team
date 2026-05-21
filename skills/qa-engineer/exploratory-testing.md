# Skill: exploratory-testing

**Type:** atomic

## Purpose

Run structured exploratory testing to find defects and risks that planned tests do not cover. Exploratory testing is not random clicking — it is disciplined investigation driven by a charter, constrained by a time-box, and documented in real time.

## When to Invoke

- Planned tests are passing but confidence in the release is not high.
- A feature has complex user interactions that are difficult to fully specify upfront.
- A risk area has been identified but the failure modes are unknown.
- A short investigation is needed to assess quality before committing to a full test plan.

## Workflow

1. **Write a charter.** A charter defines what you are exploring, how you will explore it, and what you are looking for. Format:
   ```
   Explore <area of the system>
   With <tools, techniques, or data>
   To discover <what risks or defects you are looking for>
   ```
   One session, one charter. Broad charters produce unfocused sessions.

2. **Set the time-box.** A session is typically 60–90 minutes. Longer sessions lose focus. If more is needed, run multiple sessions with separate charters.

3. **Take notes in real time.** During the session, record:
   - What you tried
   - What you observed (including things that worked correctly — note those too)
   - Any anomalies, unexpected behaviour, or questions that arose
   Do not rely on memory. Notes taken after the session are reconstructions, not records.

4. **Vary your approach.** Within the charter, use multiple techniques:
   - Follow user flows end to end
   - Use boundary values and unexpected inputs
   - Try to break implied assumptions (what if the user has no data? Has too much? Acts out of sequence?)
   - Observe behaviour under slow connections or with data from edge-case users

5. **Capture defects immediately.** When something looks wrong, document it with enough detail to reproduce it before moving on. Use the bug-report skill for any defect that warrants a formal report.

6. **Debrief.** After the session, summarise:
   - What was covered
   - What was found (defects, risks, questions)
   - What was NOT covered and why
   - Whether a follow-up session is needed

## Output

- **Charter** — what was explored, how, and what was being looked for
- **Session notes** — real-time log of what was tried and observed
- **Defects found** — list of issues, with bug reports for any that need formal tracking
- **Coverage summary** — what was and was not covered, with rationale
- **Debrief summary** — overall assessment and recommended follow-up
