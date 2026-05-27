# Skill: idp-design

**Type:** atomic
**Trigger:** Design an internal developer platform — capabilities, self-service boundaries, and developer contract

## Purpose

Design the scope, developer-facing interface, and self-service boundaries of an internal developer platform capability before any infrastructure is built. The developer contract — what teams interact with versus what is internal — is the most important design decision a platform team makes. Getting it wrong after infrastructure exists is expensive.

## When to Invoke

- A new platform capability is being introduced (new environment type, new deployment mechanism, new shared service).
- An existing capability is being significantly redesigned.
- Teams are building the same thing independently and a platform capability could consolidate the approach.
- The platform team is being asked to support a new workload type.

**Do not invoke** to redesign a capability without first understanding why teams are currently routing around it — the root cause shapes the design.

## Workflow

1. **Understand the current state.** Before designing, identify what teams currently do to accomplish the task the new capability will address. Interview at least one representative team. Understand what is painful, what is working, and what teams would not want to lose. A design that ignores the current state will be ignored or worked around.
   **Gate:** Do not produce a design until you can describe what teams do today and what specific friction the new capability removes.

2. **Define the developer contract.** The contract has two sides:
   - **What teams interact with:** the self-service interface — APIs, CLI tools, portal UI, Helm values files, pipeline templates, golden path steps. This is what teams see and touch.
   - **What is internal to the platform:** the infrastructure, configuration, and machinery teams do not need to understand or operate.
   Document both sides explicitly. Anything undocumented will be assumed to be part of one side or the other — usually wrongly.

3. **Define the self-service boundary.** State clearly:
   - What teams can do without platform team involvement.
   - What requires platform team involvement and why.
   - What is explicitly out of scope for this capability.
   If a team needs to open a ticket for routine operations, the self-service boundary is in the wrong place.
   **Gate:** The self-service boundary must be reviewed by at least one team that will use the capability. Their reactions to what requires platform involvement reveal whether the boundary is in the right place.

4. **Identify what is on and off the golden path.** The capability will have an 80% case — the supported, opinionated path — and edge cases that the platform cannot fully support. Name them now:
   - What is on the golden path: standard configuration, supported workload types, documented integration patterns.
   - What is off the golden path: customisations the platform will not own, workload types that are out of scope, integrations teams must manage themselves.
   Off-path work is explicitly unsupported. Teams that go off-path own the consequences.

5. **Produce the design document.** One-pager format:
   ```
   ## Capability
   [Name and one-sentence purpose]

   ## Developer Contract
   Teams interact with: [interface elements]
   Internal to platform: [infrastructure and machinery]

   ## Self-Service Boundary
   Teams can do without platform team: [list]
   Requires platform team: [list — and why]
   Out of scope: [list]

   ## Golden Path
   On-path: [standard configuration and workload types]
   Off-path: [explicitly unsupported — teams own these]

   ## Open Questions
   [Decisions not yet made that could change the design]
   ```

## Output

- **IDP design document** — developer contract, self-service boundary, golden path, and open questions.
- Confirmed by at least one representative team before infrastructure work begins.

## Common Rationalizations

| Rationalization | Reality |
|---|---|
| "We'll figure out the interface as we build" | The interface is the hardest part to change after infrastructure exists. Design it first. |
| "Teams can just read the Terraform" | If teams need to read the Terraform to use the platform, the self-service boundary is in the wrong place. |
| "We'll support all use cases" | A platform that tries to support everything supports nothing well. Name what is off the golden path now. |
| "One team reviewed it, that's enough" | One team's perspective is a sample. Review with the team closest to the edge cases, not just the friendliest adopter. |

## Red Flags

- Design produced without interviewing any teams about their current workflow
- Developer contract that does not specify what is internal to the platform
- Self-service boundary defined without input from the teams it affects
- No "off the golden path" list — everything is claimed to be supported
- Open questions left unresolved when infrastructure work begins

## Verification

Before starting infrastructure work:

- [ ] Current team workflow documented — what teams do today and what friction the capability removes
- [ ] Developer contract documented — both what teams interact with and what is internal
- [ ] Self-service boundary reviewed by at least one representative team
- [ ] Golden path and off-path cases are named explicitly
- [ ] Open questions assigned to owners with resolution deadlines
- [ ] Design document approved before infrastructure code is written
