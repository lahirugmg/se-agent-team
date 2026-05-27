# Skill: developer-experience

**Type:** atomic
**Trigger:** Measure and improve developer productivity and satisfaction with the platform

## Purpose

Measure and improve the productivity and satisfaction of the engineering teams using the platform. Developer experience (DX) is the lagging indicator of platform success: teams that are faster, less frustrated, and less reliant on the platform team are the evidence that the platform is working. Without measurement, DX improvements are anecdotal.

## When to Invoke

- After a platform capability has been in production for a sufficient period to collect meaningful signal.
- Teams are reporting that the platform is slowing them down, even if SLOs are green.
- A platform capability is being redesigned and baseline DX data is needed to measure improvement.
- Quarterly or semi-annual platform health review.

**Do not invoke** to collect DX data for the first time on a capability that has been live for less than two weeks — the signal is too sparse to be meaningful.

## Workflow

1. **Define what you are measuring.** Developer experience is not a single number. Measure across four dimensions:
   - **Speed:** How long do platform-assisted tasks take compared to doing them manually or before the platform existed? (time-to-first-deploy, time to provision an environment, CI cycle time)
   - **Reliability:** How often do teams have to retry or escalate because the platform failed? (platform error rate, escalation rate to platform team)
   - **Cognitive load:** How much does the team need to know or remember to use the platform? (measured through observation, not survey)
   - **Satisfaction:** Do teams feel the platform helps or hinders them? (survey, but calibrate against the other three)

2. **Collect data from multiple sources.** No single source tells the full story:
   - **Quantitative:** Pipeline metrics, deployment frequency, platform error rates, time-to-X measurements from platform-observability.
   - **Qualitative:** Direct conversations with teams, support ticket themes, off-path work observed (teams doing something manually that the platform should handle).
   - **Passive:** Adoption rate of golden paths, volume of platform team escalations, frequency of "how do I...?" questions.

3. **Identify the highest-friction points.** Rank friction sources by: frequency (how often teams hit it), severity (how much time it costs), and whether it is on or off the golden path. On-path friction is the platform team's responsibility. Off-path friction may signal that the golden path scope is too narrow.
   **Gate:** Before proposing changes, confirm with the teams that the identified friction points match what they actually experience. Friction identified without consumer input is a guess.

4. **Propose targeted improvements.** Each improvement should address a specific friction point with a measurable expected outcome:
   ```
   Friction: Environment provisioning takes 25 minutes on average — teams report this
             blocks their workflow during development.
   Root cause: The network policy application step takes 18 minutes due to a
               sequential apply that could be parallelised.
   Proposed fix: Parallelise network policy application.
   Expected outcome: Provisioning time drops below 10 minutes.
   Measure: Time-to-provision metric in platform-observability dashboard.
   ```

5. **Measure after the improvement.** The DX improvement is not complete until the metric shows change. If the metric did not improve, the root cause analysis was wrong. Re-investigate before trying another fix.

## Output

- **DX report** — measurements across speed, reliability, cognitive load, and satisfaction for the measured capabilities.
- **Friction ranking** — top friction points by frequency and severity, confirmed with consumer teams.
- **Improvement proposals** — each with a specific friction point, root cause, proposed fix, expected outcome, and how it will be measured.
- **Post-improvement measurement** — before/after comparison for completed improvements.

## Common Rationalizations

| Rationalization | Reality |
|---|---|
| "Teams would tell us if DX was bad" | Teams adapt to friction. They build habits around the friction rather than reporting it. The absence of complaints is not evidence of good DX. |
| "Our SLOs are green, so DX must be fine" | SLOs measure platform reliability, not whether the platform makes teams faster. Green SLOs and poor DX coexist regularly. |
| "We do a survey once a year" | Annual surveys are too infrequent to drive improvements. By the time the next survey runs, the problems from the previous one may still not be fixed. |
| "Improving DX is nice to have" | A platform that makes teams slower is consuming engineering budget without producing leverage. Improving DX is the platform team's primary job. |

## Red Flags

- DX measured only through satisfaction surveys with no quantitative data
- Friction identified without confirming it with consumer teams
- Improvements proposed without a measurable expected outcome
- No before/after measurement for completed improvements
- Platform team defines DX targets without consumer team input
- Cognitive load not measured — teams know more than they should need to

## Verification

Before publishing a DX report or declaring an improvement complete:

- [ ] Speed, reliability, cognitive load, and satisfaction are all measured (not just one)
- [ ] Data collected from quantitative, qualitative, and passive sources
- [ ] Top friction points confirmed with consumer teams before improvement proposals are written
- [ ] Each improvement proposal has: friction point, root cause, proposed fix, expected outcome, and measurement plan
- [ ] Post-improvement measurement confirms the metric moved in the expected direction
- [ ] DX review schedule set for next period
