# Skill: threat-modeling

**Type:** atomic

## Purpose

Identify the assets, trust boundaries, threat actors, and attack vectors relevant to a system. Produces a ranked threat list that drives the focus of subsequent security reviews and shapes design decisions before implementation begins.

## When to Invoke

- A new system or significant feature is being designed and security requirements need to be established.
- An existing system is being reviewed and a structured threat landscape is needed.
- A security audit needs a prioritised focus derived from threat analysis rather than intuition.

## Workflow

1. **Identify assets.** List what needs to be protected: user data, credentials, financial information, business logic, infrastructure, availability. For each asset, state the impact of its loss, exposure, or corruption.

2. **Map the system.** Produce or collect a data flow diagram showing:
   - External actors (users, third-party services, other systems)
   - System components (services, databases, queues, storage)
   - Trust boundaries — lines that data crosses where trust changes (e.g. internet → API, API → database, internal service → external service)
   - Data flows across boundaries, labelled with the type of data

3. **Identify threat actors.** For each external actor or entry point, characterise the realistic threat actors:
   - **External attacker** — anonymous, motivated by financial gain, disruption, or data theft
   - **Authenticated user** — legitimate account, abusing privileges or attempting privilege escalation
   - **Insider** — employee or contractor with legitimate access
   - **Compromised dependency** — supply chain attack via a trusted third-party component
   Rate each actor by motivation and capability.

4. **Apply STRIDE.** For each trust boundary and component, systematically consider each threat category:
   - **S**poofing — can an actor pretend to be another entity?
   - **T**ampering — can data be modified in transit or at rest?
   - **R**epudiation — can an actor deny an action they performed?
   - **I**nformation disclosure — can an actor access data they should not?
   - **D**enial of service — can an actor degrade or disable the system?
   - **E**levation of privilege — can an actor gain more access than authorised?

5. **Rate threats.** For each identified threat, assign:
   - **Likelihood** — how likely is this attack given the attacker profile and attack surface?
   - **Impact** — how severe is the damage if the attack succeeds?
   - **Priority** — Likelihood × Impact (Critical / High / Medium / Low)

6. **Identify existing mitigations.** For each threat, note controls already in place. Threats with no mitigation and high priority require immediate attention.

7. **Produce recommendations.** For each unmitigated Critical or High threat, recommend a specific control — not a general principle.

## Output

- **Asset inventory** — what is being protected and the impact of its compromise
- **Data flow diagram** — system components, trust boundaries, and data flows
- **Threat actor profiles** — who the realistic attackers are
- **STRIDE analysis** — threats per component and boundary
- **Ranked threat list** — prioritised by likelihood × impact
- **Mitigation gaps** — unmitigated threats with recommended controls
