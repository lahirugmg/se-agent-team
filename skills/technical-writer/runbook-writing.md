# Skill: runbook-writing

**Type:** atomic

## Purpose

Write a runbook for a recurring operational procedure from a documentation perspective — producing a document that is accurate, structured, and usable by an operator who did not write it. This skill focuses on the writing and documentation standards; the operational design of the procedure itself belongs to the SRE agent.

## When to Invoke

- An operational procedure exists informally (in someone's head or in a Slack thread) and needs to be documented.
- An existing runbook is outdated, unclear, or failed during an incident.
- A post-mortem has identified a documentation gap that a runbook would close.

## Workflow

1. **Interview the procedure owner.** Before writing, gather the information from the person who currently performs the procedure:
   - When is this procedure performed? (Trigger or schedule)
   - What is needed to perform it? (Access, tools, information)
   - What are the steps, in order?
   - What does success look like after each step?
   - What can go wrong, and what should the operator do?
   - Who to call if the procedure doesn't work?
   Record the interview. Do not write from memory.

2. **Write the trigger.** The first thing in the runbook is when to use it. If an operator cannot determine within 10 seconds whether this runbook applies to their situation, it will not be used:
   - "Use this runbook when alert `database-connection-pool-exhausted` fires"
   - "Use this runbook to perform the monthly certificate rotation"

3. **Write prerequisites.** Every access requirement, tool, and piece of information needed before starting the first step. Formatted as a checklist the operator can tick off.

4. **Write the procedure.** Numbered steps. Each step:
   - States a single, specific action
   - Uses imperative voice ("Run", "Navigate to", "Enter")
   - Includes the exact command or UI path where applicable
   - States the expected output or confirmation after commands with observable results
   - Warns before any step that is irreversible or has a significant blast radius

5. **Write verification steps.** After significant actions, describe how to confirm the step succeeded before proceeding.

6. **Write the escalation path.** If the procedure does not produce the expected result, where does the operator go? Be specific: team name, channel, how to page.

7. **Review with the procedure owner.** Have the person who performs the procedure review the draft for accuracy. Then have someone who does not perform it follow it cold. Both reviews are necessary.

## Output

- **Runbook document** with: trigger, prerequisites (checklist format), numbered procedure with verification steps, escalation path, and review date
- **Review record** — confirmation from the procedure owner and a cold-run tester
