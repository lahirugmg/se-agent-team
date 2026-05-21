# Skill: infrastructure-as-code

**Type:** atomic

## Purpose

Write or review infrastructure definitions using an IaC tool (Terraform, CloudFormation, Pulumi, Bicep, or equivalent) such that all infrastructure is reproducible, version-controlled, and provably consistent with its declared state.

## When to Invoke

- New infrastructure needs to be provisioned for a service.
- Existing infrastructure needs to be modified, extended, or reviewed for correctness.
- Infrastructure has drifted from its declared state and needs to be reconciled.
- An IaC module or template needs to be reviewed before it is applied.

## Workflow

1. **Understand the infrastructure requirements.** Before writing any code:
   - What resources need to exist? (compute, networking, storage, secrets, queues, databases)
   - What are the environment differences? (production vs. staging resource sizes, replica counts, retention policies)
   - What are the compliance requirements? (encryption at rest, private networking, audit logging)

2. **Structure the code.** Organise IaC code for readability and reuse:
   - Separate modules for logical groupings (networking, compute, database)
   - Separate state files or stacks per environment
   - Variables for everything that differs between environments
   - No hardcoded values (account IDs, region names, AMI IDs) in the main code — parameterise or use data sources

3. **Apply security defaults.**
   - All data at rest encrypted
   - All network resources in private subnets unless public access is explicitly required
   - Security groups with minimum necessary ingress/egress rules
   - IAM roles with least-privilege policies
   - No credentials or secrets in IaC files

4. **Run plan/diff before apply.** Always review the planned changes before applying them:
   - Verify that no unexpected resources are being destroyed
   - Verify that resource replacements (vs. in-place updates) are intentional
   - For production changes, get a second review of the plan output

5. **Review for drift.** Before writing new IaC for existing infrastructure, check for drift between the declared state and actual state. Reconcile drift before adding new resources — applying new IaC to drifted infrastructure produces unpredictable results.

6. **Document non-obvious decisions.** Add comments for any resource configuration that is non-obvious: why a specific instance type was chosen, why a particular retention policy was set, why public access is enabled for a resource that is usually private.

7. **Verify after apply.** After applying IaC, confirm:
   - The target resources exist and are in the expected state
   - Health checks pass (for compute resources)
   - No plan/diff shows residual changes (state is clean)

## Output

- **IaC code** — committed to version control with modules, variables, and environment configurations
- **Plan output** — the reviewed and approved plan before application
- **Apply record** — confirmation of what was applied, when, and by whom
- **Post-apply verification** — confirmation that resources are healthy and state is clean
