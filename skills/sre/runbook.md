# Skill: runbook

**Type:** atomic

## Purpose

Write or update an operational runbook for a recurring procedure — a documented, tested set of steps that any on-call operator can follow to perform the procedure safely, without requiring the author's presence.

## When to Invoke

- A new operational procedure is being established (deployment, rollback, database failover, cache flush).
- An existing runbook is out of date, known to be wrong, or was found to be inadequate during an incident.
- A post-mortem has identified a gap in operational documentation.

## Workflow

1. **Define the trigger.** A runbook is invoked in a specific situation. Document exactly what causes an operator to open this runbook:
   - "This runbook is used when alert X fires"
   - "This runbook is used during scheduled maintenance for Y"
   - "This runbook is used when a customer reports Z"
   A runbook without a clear trigger will not be found when needed.

2. **State the prerequisites.** Before the operator executes any step, what must be true?
   - Required access (AWS role, database credentials, Kubernetes context)
   - Required tools (CLI versions, local dependencies)
   - Required information (service name, region, incident ID)
   An operator who reaches step 4 and discovers they don't have the required access has lost valuable time.

3. **Write the procedure.** Numbered steps. Each step is a single, specific action:
   - Include the exact command to run, not just a description of what to run
   - Include the expected output after each command that has one
   - For commands that are destructive or irreversible, add a warning before the step
   - For commands with mandatory parameters, show the complete syntax with placeholders: `kubectl rollout undo deployment/<SERVICE_NAME> -n <NAMESPACE>`

4. **Include verification steps.** After each significant action, include a step to verify the action succeeded before proceeding:
   - "Run `kubectl get pods -n <NAMESPACE>` and confirm all pods are in Running state before continuing."

5. **Define the escalation path.** If the procedure does not resolve the situation, where does the operator go?
   - Which team or individual to contact
   - How to escalate (page, channel, direct message)
   - What information to include in the escalation

6. **Test the runbook.** A runbook that has never been executed is a draft. Test it:
   - Run through it in a non-production environment
   - Have someone who did not write it follow it cold
   - Update based on gaps found during the test
   Record the test date and environment in the runbook.

7. **Set a review date.** Runbooks go stale as systems change. Set a review date (typically 6 months) and assign an owner responsible for keeping it current.

## Output

A runbook document containing:
- **Trigger** — when to use this runbook
- **Prerequisites** — required access, tools, and information
- **Procedure** — numbered steps with exact commands, expected outputs, and warnings
- **Verification steps** — confirmation checks between significant actions
- **Escalation path** — what to do if the procedure doesn't work
- **Tested on** — date and environment of last test
- **Review date** — next scheduled review
