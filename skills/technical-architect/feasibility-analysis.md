# Skill: feasibility-analysis

**Type:** atomic

## Purpose

Assess whether a proposed technical approach is achievable within the given constraints of time, team, technology, and budget. Produces a clear recommendation — proceed, proceed with conditions, or do not proceed — with the reasoning and evidence behind it.

## When to Invoke

- A proposed approach involves technology the team has not used before.
- A stakeholder is proposing something and there is uncertainty about whether it can be built.
- A timeline or cost estimate seems inconsistent with the scope and the team needs an independent assessment.
- A proof of concept is needed to resolve a feasibility question before committing to a design.

## Workflow

1. **Define the proposal.** State clearly what is being assessed: what would be built, how, and to what standard. If the proposal is vague, clarify it before assessing — assessing a vague proposal produces a vague answer.

2. **Identify constraints.** List the fixed constraints the proposal must fit within:
   - Timeline: when must it be done?
   - Team: who is available, and what are their skills?
   - Budget: what is the cost ceiling?
   - Technology: are there mandated platforms, languages, or vendor relationships?
   - Compliance: are there regulatory requirements the solution must meet?

3. **Assess technical complexity.** For each major component of the proposal:
   - Is this well-understood technology or novel?
   - Has the team done this before?
   - Are there known unknowns (things we know we don't know)?
   - Are there unknown unknowns (areas where we don't know what we don't know)?
   Rate each component: Low / Medium / High / Unknown complexity.

4. **Identify dependencies.** List external systems, teams, APIs, or data that the proposal depends on. For each dependency:
   - Is it available and stable?
   - Who controls it?
   - What is the risk if it changes or is unavailable?

5. **Assess risks.** Identify the top three to five risks that could prevent successful delivery. For each:
   - Likelihood (Low / Medium / High)
   - Impact if it materialises
   - Possible mitigation

6. **Produce a recommendation.** One of:
   - **Feasible** — the proposal can be delivered within constraints; proceed.
   - **Feasible with conditions** — feasible if specific conditions are met (list them).
   - **Requires spike** — too many unknowns to assess; recommend a time-boxed investigation.
   - **Not feasible** — cannot be delivered within the stated constraints; explain why and suggest alternatives.

## Output

- **Proposal summary** — what was assessed
- **Constraint inventory** — the fixed constraints
- **Complexity assessment** — component-by-component complexity rating
- **Dependency map** — external dependencies and their risk level
- **Risk register** — top risks with likelihood, impact, and mitigation
- **Recommendation** — Feasible / Feasible with conditions / Requires spike / Not feasible, with rationale
