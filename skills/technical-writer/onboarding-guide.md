# Skill: onboarding-guide

**Type:** atomic

## Purpose

Create onboarding documentation that enables a new engineer, user, or operator to become effective in a system or codebase without requiring hand-holding from the existing team. An onboarding guide measures success by the questions it pre-empts.

## When to Invoke

- A new team member is joining and there is no structured onboarding documentation.
- Existing onboarding documentation is outdated or known to be incomplete.
- A product or system is being opened to a new category of user who needs a structured path to getting started.

## Workflow

1. **Define the audience and success criteria.** Who is being onboarded, and what does "successfully onboarded" look like?
   - For an engineer: can set up a local development environment, run tests, and make a first contribution
   - For an operator: can deploy the service, monitor it, and respond to a basic alert
   - For an end user: can complete their primary task without external help
   The guide is done when a representative reader reaches the success criteria without asking for help.

2. **Map the journey.** Document the full onboarding path from "nothing" to "effective". Identify the blockers at each stage — the things that stop new joiners and cause them to ask for help. These become the guide's key content areas.

3. **Write the system overview.** Before any instructions, give the reader enough context to form a mental model:
   - What does this system do?
   - What are its main components?
   - How does it fit into the broader product or infrastructure?
   Two to three paragraphs. Not a history; not a feature list. Context for the instructions that follow.

4. **Write the setup section.** Step-by-step instructions to get from a blank machine (or account) to a running environment:
   - Prerequisites (what must be installed or configured before starting)
   - Installation and configuration steps — exact commands, not descriptions
   - Verification — how to confirm setup succeeded
   Test this section on a blank machine. If it requires any steps not listed, it is incomplete.

5. **Write the first tasks section.** Guide the reader through their first meaningful actions in the system:
   - For engineers: make a trivial code change, run the test suite, open a PR
   - For operators: deploy to a non-production environment, view a dashboard, simulate an alert
   - For users: complete the primary use case
   First tasks build confidence and surface any remaining gaps in setup.

6. **Write the "where to find things" section.** A reference for the most common questions:
   - Where is the code? Where are the docs? Where are the runbooks?
   - Where do I ask questions? (Slack channel, team alias, on-call rotation)
   - Where do I report a problem? (Issue tracker, incident process)
   - Who owns what? (Key contacts by area)

7. **Validate the guide.** Have a real new joiner follow it. Record every question they ask or every place they get stuck. Fix those gaps before publishing.

## Output

- **System overview** — what the system is and where it fits
- **Setup guide** — exact steps from zero to working environment, verified on a blank machine
- **First tasks walkthrough** — the first two to three meaningful actions
- **Reference section** — where to find things, who to contact
- **Validation record** — who tested it and what was found and fixed
