# Skill: user-guide

**Type:** atomic

## Purpose

Produce a task-oriented guide that enables a specific audience to accomplish a specific set of tasks using the product or system. A user guide teaches how to do things; it is not a feature catalogue or a specification.

## When to Invoke

- A feature or product has been shipped and users need guidance to adopt it effectively.
- Users are struggling with a specific task and there is no documentation that addresses it directly.
- Onboarding for a new user type needs to be documented.

## Workflow

1. **Define the audience.** A user guide for a system administrator is different from one for an end user. Identify:
   - Who will read this guide?
   - What do they already know? (Assume this, do not explain it)
   - What do they need to be able to do after reading it?
   Write to one primary audience. If multiple audiences need the same system documented, write separate guides.

2. **Define the scope.** List the tasks the guide will cover. A guide that tries to cover everything covers nothing well. Tasks should be: specific, completable, and meaningful to the reader.

3. **Structure around tasks, not features.** Organise the guide by what the reader is trying to do, not by what the product can do:
   - Good: "Add a payment method", "Set up two-factor authentication", "Export your data"
   - Bad: "Payment settings", "Security settings", "Account settings"

4. **Write prerequisites.** Before the first step of any task, state what the reader must have or know:
   - Required access or permissions
   - Required setup that must be done first
   - Required knowledge or context
   A reader who reaches step 3 and discovers they need admin access has had a bad experience.

5. **Write steps as actions.** Each step is a single action the reader performs, written in imperative form:
   - "Click **Add payment method**."
   - "Enter your card number in the **Card number** field."
   - "Click **Save**. A confirmation message appears."
   Include the expected result after any step where the system responds visibly.

6. **Add context sparingly.** Explain the why only when it is not obvious and when the reader will make a better decision knowing it. Do not explain how the system works internally — explain what the reader needs to know to complete the task.

7. **Test the guide.** Follow the guide yourself from scratch. Have someone unfamiliar with the feature follow it cold. A guide that cannot be followed without additional help is not done.

## Output

- **Audience and scope definition** — who this guide is for and what tasks it covers
- **Task-oriented guide** — each task as a titled section with prerequisites, numbered steps, and expected results
- **Tested** — confirmation that the guide was followed end-to-end without gaps
