# Skill: system-design

**Type:** atomic

## Purpose

Design the architecture for a new system or major component: define what parts exist, how they interact, what data flows where, and what technology choices are made and why. Produces a design that can be reviewed, decided on, and handed to implementers.

## When to Invoke

- A new system or major component needs to be designed before implementation begins.
- An existing system is being significantly restructured.
- Multiple technical approaches are possible and a design review is needed to choose one.

## Workflow

1. **Read the requirements.** Start with the PRD, user stories, and any existing architectural context. Extract: functional requirements (what the system must do), non-functional requirements (latency, throughput, availability, data retention), and constraints (existing systems it must integrate with, technology mandates, budget, team skills).

2. **Identify components.** Break the system into logical parts. For each component, define:
   - Its single responsibility
   - Its boundaries (what it owns vs. what it delegates)
   - Its primary consumers and producers

3. **Define interactions.** Map how components communicate: synchronous vs. asynchronous, request/response vs. event-driven, push vs. pull. For each interaction, specify the protocol, the data shape, and the failure behaviour.

4. **Map data flows.** Trace the lifecycle of the system's primary data entities: where they originate, how they are transformed, where they are stored, and where they are consumed or expired. Identify which component owns each entity.

5. **Address non-functional requirements explicitly.** For each NFR, show how the design satisfies it:
   - Availability → redundancy, failover, health checks
   - Latency → caching, async offloading, read replicas
   - Security → trust boundaries, encryption in transit and at rest, authentication points
   - Scalability → where the bottlenecks are and how they scale

6. **Generate alternatives.** Produce at least two design options for any significant architectural decision. Document the tradeoffs. The final design must reference which alternative was chosen and why.

7. **Identify risks.** List design decisions that are hard to reverse, introduce new failure modes, or depend on unproven technology. Each risk has a mitigation or an explicit acceptance decision.

## Output

- **Component diagram** — the logical parts of the system and their relationships
- **Data flow diagram** — how primary entities move through the system
- **Technology choices** — each significant choice with rationale and alternatives considered
- **NFR analysis** — how each non-functional requirement is satisfied
- **Risk register** — hard-to-reverse decisions and high-impact unknowns
