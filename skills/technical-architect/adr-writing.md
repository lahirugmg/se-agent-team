# Skill: adr-writing

**Type:** atomic

## Purpose

Document an architectural decision in a structured, permanent record that captures context, alternatives, the chosen option, and the reasoning. An ADR is a decision record, not a design document — it records that a decision was made, why, and what was rejected.

## When to Invoke

- A significant architectural decision has been made or is about to be made.
- A decision is hard to reverse, affects multiple components, or will be questioned later.
- An existing ADR needs to be superseded because circumstances have changed.

## Workflow

1. **Name the decision.** Give the ADR a short, specific title that names the decision being made. "Use PostgreSQL for the primary data store" not "Database decision."

2. **Record the status.** One of: Proposed, Accepted, Deprecated, Superseded. If superseded, link to the ADR that replaces it.

3. **Write the context.** Describe the situation that required a decision. Include:
   - What problem needed to be solved
   - The constraints that applied (technical, organisational, timeline)
   - What would happen if no decision was made
   Do not include the decision itself here — context is purely about the situation.

4. **Document the options.** List every serious option that was considered. For each:
   - A brief description of the approach
   - Its key advantages in this context
   - Its key disadvantages or risks in this context
   At least two options must be documented. If only one option was ever considered, the decision was not an architectural decision — it was an assumption.

5. **State the decision.** One clear sentence: "We will use X." No hedging, no "we decided to consider." If the decision is conditional or phased, state the conditions explicitly.

6. **Explain the rationale.** Connect the decision back to the context. Why does this option serve the stated constraints better than the alternatives? Reference specific tradeoffs.

7. **Document the consequences.** What does this decision enable? What does it foreclose? What technical debt does it create? What follow-on decisions does it require? Both positive and negative consequences belong here.

## Output

A single ADR document with these sections:
- **Title** and unique ID (e.g. ADR-0012)
- **Status** (Proposed / Accepted / Deprecated / Superseded)
- **Context** — the situation that required a decision
- **Options** — each alternative with pros and cons
- **Decision** — the chosen option in one sentence
- **Rationale** — why this option over the alternatives
- **Consequences** — what this enables, forecloses, and requires
