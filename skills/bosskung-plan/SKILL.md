---
name: bosskung-plan
description: 'Plan and deliver features with cost efficiency: use Opus-level reasoning for architecture and plan quality, then delegate bounded implementation and verification tasks to Haiku-class models. Use when you need a clear feature plan, controlled scope, lower token cost, and an interview-first workflow that clarifies requirements one question at a time before planning.'
argument-hint: 'Feature goal, constraints, deadlines, and cost targets'
user-invocable: true
disable-model-invocation: false
---

# Bosskung Plan

## What This Skill Produces
- A complete feature plan with scope, assumptions, risks, and acceptance criteria.
- A task breakdown that separates high-leverage reasoning (Opus) from execution-heavy work (Haiku).
- A delegation map with explicit handoff packets and review gates.
- A step-by-step clarification flow that asks one focused question at a time and suggests a solution as soon as enough information is available.

## When to Use
- You need strong up-front planning quality, but want lower implementation cost.
- The feature can be split into independent or loosely coupled tasks.
- You want predictable quality gates before merge or release.

## Inputs to Collect First
- Feature objective and user value.
- Hard constraints: timeline, compatibility, performance, security, compliance.
- Cost target: where to spend premium reasoning and where to optimize.
- Definition of done: tests, docs, rollout requirements.

## Clarification Loop
1. Ask one question at a time.
- Keep each question focused on the single highest-uncertainty requirement.
- Prefer questions that unlock multiple downstream decisions.
- Avoid multi-part questions unless the answer truly depends on them.

2. After each answer, decide whether enough is known.
- If the requirement is still ambiguous, ask the next most important question.
- If the requirement is sufficiently clear, stop asking and propose a solution.

3. When a solution is suggested, include alternatives only if they materially change cost, risk, or scope.
- Prefer one recommended path.
- Call out tradeoffs briefly.
- Keep the suggestion concrete enough to implement.

## Workflow
1. Define mission and boundaries (Opus)
- Restate the feature outcome in one paragraph.
- List in-scope and out-of-scope items.
- Capture assumptions and unknowns.
- If requirements are incomplete, ask the next best question before moving on.

2. Build the implementation strategy (Opus)
- Identify impacted areas (API, data, UI, infra, tests, docs).
- Propose 1-2 viable approaches and choose one with tradeoffs.
- Record key risks and mitigations.
- If the solution path is clear, present the recommended solution immediately instead of waiting for more context.

3. Design the execution graph (Opus)
- Break work into tasks sized for fast delegated execution.
- Mark dependencies and parallelizable tasks.
- Add acceptance criteria per task.

4. Delegate bounded tasks (Haiku)
- Send Haiku tasks with strict packets:
	- Objective
	- Files/scope
	- Constraints
	- Acceptance tests
	- Output format (patch, summary, test evidence)
- Delegate best to Haiku:
	- Mechanical refactors
	- Test writing from clear specs
	- Boilerplate implementation
	- File-by-file updates with explicit requirements

5. Keep critical decisions centralized (Opus)
- Do not delegate these without review:
	- Architecture pivots
	- Security-sensitive logic
	- Data migrations and backward compatibility choices
	- Ambiguous requirements resolution

6. Review and integrate (Opus)
- Validate each delegated result against acceptance criteria.
- Run quality checks (tests, lint, build, behavior).
- Reject or revise work that passes syntax but misses intent.

7. Finalization (Opus)
- Produce final change summary: what changed, why, risks, rollout/rollback.
- Confirm definition of done is met.

## Delegation Decision Rules
- Use Opus when task uncertainty is high or tradeoffs are non-trivial.
- Use Haiku when complexity is low to medium, requirements are explicit, and verification is objective.
- If a delegated task returns unclear rationale, escalate back to Opus.
- If three failed delegation attempts occur on the same task, keep it with Opus.

## Default Output Style
- Deliver planning output as a checklist plus task table.
- Include, in order:
	- Executive summary (3-5 lines)
	- Scope checklist
	- Task table with owner model (Opus or Haiku), dependencies, and acceptance criteria
	- Risk table with mitigation and fallback
	- Final go/no-go checklist

## Suggested Response Pattern
When requirements are incomplete, respond in this order:
1. One clarifying question.
2. One short note explaining why that question matters.
3. A tentative solution direction if the current information already supports one.

When requirements are clear enough, respond in this order:
1. Recommended solution.
2. Checklist plus task table.
3. Any remaining edge cases or risks.

## Handoff Packet Template (Opus -> Haiku)
Use this exact structure when delegating:

```markdown
Task: <one sentence>
Goal: <expected outcome>
Scope: <files/modules allowed>
Constraints: <style, compatibility, performance, security>
Acceptance Criteria:
- <criterion 1>
- <criterion 2>
Verification:
- <tests/commands to run>
Return:
- Patch summary
- Files changed
- Test evidence
- Open questions
```

## Quality Gates
- Planning gate: clear scope, assumptions, and acceptance criteria exist.
- Delegation gate: every task has bounded scope and verifiable output.
- Integration gate: tests and checks pass; behavior matches feature intent.
- Release gate: risk and rollback notes are documented.

## Completion Checklist
- Feature objective is achieved and measurable.
- All acceptance criteria are met.
- Tests cover main path and key edge cases.
- Cost target is respected (high-cost reasoning used only where necessary).
- Final summary includes risks, follow-ups, and rollout notes.

## Example Prompts
- /bosskung-plan Plan a new billing alert feature with backward compatibility and minimal cost.
- /bosskung-plan Create a migration plan for profile settings rewrite, delegating coding tasks to Haiku.
- /bosskung-plan Plan and execute API pagination improvements with strict acceptance tests.
4. Delegate bounded tasks (Haiku)
- Send Haiku tasks with strict packets:
	- Objective
	- Files/scope
When requirements are incomplete, respond in this order:
1. One clarifying question.
2. One short note explaining why that question matters.
3. A tentative solution direction if the current information already supports one.
	- Constraints
When requirements are clear enough, respond in this order:
1. Recommended solution.
2. Checklist plus task table.
3. Any remaining edge cases or risks.
	- Acceptance tests
	- Output format (patch, summary, test evidence)
- Delegate best to Haiku:
	- Mechanical refactors
	- Test writing from clear specs
	- Boilerplate implementation
	- File-by-file updates with explicit requirements

5. Keep critical decisions centralized (Opus)
- Do not delegate these without review:
	- Architecture pivots
	- Security-sensitive logic
	- Data migrations and backward compatibility choices
	- Ambiguous requirements resolution

6. Review and integrate (Opus)
- Validate each delegated result against acceptance criteria.
- Run quality checks (tests, lint, build, behavior).
- Reject or revise work that passes syntax but misses intent.

7. Finalization (Opus)
- Produce final change summary: what changed, why, risks, rollout/rollback.
- Confirm definition of done is met.

## Delegation Decision Rules
- Use Opus when task uncertainty is high or tradeoffs are non-trivial.
- Use Haiku when complexity is low to medium, requirements are explicit, and verification is objective.
- If a delegated task returns unclear rationale, escalate back to Opus.
- If three failed delegation attempts occur on the same task, keep it with Opus.

## Default Output Style
- Deliver planning output as a checklist plus task table.
- Include, in order:
	- Executive summary (3-5 lines)
	- Scope checklist
	- Task table with owner model (Opus or Haiku), dependencies, and acceptance criteria
	- Risk table with mitigation and fallback
	- Final go/no-go checklist

## Handoff Packet Template (Opus -> Haiku)
Use this exact structure when delegating:

```markdown
Task: <one sentence>
Goal: <expected outcome>
Scope: <files/modules allowed>
Constraints: <style, compatibility, performance, security>
Acceptance Criteria:
- <criterion 1>
- <criterion 2>
Verification:
- <tests/commands to run>
Return:
- Patch summary
- Files changed
- Test evidence
- Open questions
```

## Quality Gates
- Planning gate: clear scope, assumptions, and acceptance criteria exist.
- Delegation gate: every task has bounded scope and verifiable output.
- Integration gate: tests and checks pass; behavior matches feature intent.
- Release gate: risk and rollback notes are documented.

## Completion Checklist
- Feature objective is achieved and measurable.
- All acceptance criteria are met.
- Tests cover main path and key edge cases.
- Cost target is respected (high-cost reasoning used only where necessary).
- Final summary includes risks, follow-ups, and rollout notes.

## Example Prompts
- /bosskung-plan Plan a new billing alert feature with backward compatibility and minimal cost.
- /bosskung-plan Create a migration plan for profile settings rewrite, delegating coding tasks to Haiku.
- /bosskung-plan Plan and execute API pagination improvements with strict acceptance tests.
