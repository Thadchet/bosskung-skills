---
name: bosskung-plan
description: 'Plan and deliver software features with cost-efficient model routing: use Opus-level reasoning for architecture and risk decisions, then delegate bounded implementation tasks to Haiku-class models. Use for feature planning, controlled scope, and interview-first clarification with explicit answer choices.'
argument-hint: 'Feature goal, constraints, timeline, and cost target'
user-invocable: true
disable-model-invocation: false
---

# Bosskung Plan

## What This Skill Produces
- A complete feature plan with scope, assumptions, risks, and acceptance criteria.
- A task graph that separates high-leverage reasoning (Opus) from execution-heavy tasks (Haiku).
- A delegation map with explicit handoff packets and quality gates.
- A clarification log that records each question, options presented, the recommended option, and the selected answer.

## When to Use
- You need strong up-front planning quality with lower implementation cost.
- The work can be split into independent or loosely coupled tasks.
- You want explicit decision tracking before implementation and release.

## Inputs to Collect First
- Feature objective and user value.
- Hard constraints: timeline, compatibility, performance, security, compliance.
- Cost target: where to spend premium reasoning and where to optimize.
- Definition of done: tests, docs, rollout and rollback requirements.

## Mandatory Clarification Rule
For every clarification question, always provide at least 3 selectable solution choices and explicitly mark one recommended choice.

Required format for each question:

```markdown
Question: <single highest-impact uncertainty>
Choices:
- A. <solution option 1>
- B. <solution option 2>
- C. <solution option 3>
Recommended: <A|B|C> - <one sentence why this is best under current constraints>
Please choose: Reply with A, B, C, or provide a custom answer.
```

Rules:
- Ask one question at a time.
- Each question must be focused on one decision.
- Each question must include 3 or more options.
- Include one recommended option based on current known constraints.
- If user gives a custom answer, map it to the nearest option or add a new branch and continue.

## Clarification Loop
1. Ask one focused question using the mandatory format.
2. Capture the selected choice and reason in the clarification log.
3. Decide if enough is known:
- If still ambiguous, ask the next highest-impact question with 3+ options and a recommendation.
- If sufficiently clear, stop asking and present the recommended solution.

## Workflow
1. Define mission and boundaries (Opus)
- Restate the feature outcome in one paragraph.
- List in-scope and out-of-scope items.
- Capture assumptions and unknowns.
- If requirements are incomplete, start the clarification loop.

2. Build implementation strategy (Opus)
- Identify impacted areas (API, data, UI, infra, tests, docs).
- Propose 2-3 viable approaches and select one.
- Record major tradeoffs and mitigations.

3. Design execution graph (Opus)
- Break work into bounded tasks for delegation.
- Mark dependencies and parallelizable work.
- Add measurable acceptance criteria per task.

4. Delegate bounded tasks (Haiku)
- Delegate tasks with strict handoff packets:
  - Objective
  - Files and scope
  - Constraints
  - Acceptance tests
  - Output format (patch summary, changed files, test evidence, open questions)
- Best delegation targets:
  - Mechanical refactors
  - Test writing from clear specs
  - Boilerplate implementation
  - File-by-file updates with explicit requirements

5. Keep critical decisions centralized (Opus)
- Do not delegate without review:
  - Architecture pivots
  - Security-sensitive logic
  - Data migrations and backward compatibility choices
  - Ambiguous requirements resolution

6. Review and integrate (Opus)
- Validate delegated work against acceptance criteria.
- Run tests, lint, build, and behavior checks.
- Reject or revise output that passes syntax but misses intent.

7. Finalization (Opus)
- Produce final summary: what changed, why, risks, rollout and rollback.
- Confirm definition of done.

## Delegation Decision Rules
- Use Opus when uncertainty is high or tradeoffs are non-trivial.
- Use Haiku when complexity is low to medium and verification is objective.
- Escalate back to Opus when delegated rationale is weak.
- After 3 failed delegation attempts on one task, keep it with Opus.

## Output Format
Deliver output in this order:
1. Recommended solution.
2. Executive summary (3-5 lines).
3. Scope checklist.
4. Task table (owner model, dependencies, acceptance criteria).
5. Risk table (mitigation and fallback).
6. Clarification log.
7. Go or no-go checklist.

## Clarification Log Template

```markdown
| # | Question | Options | Recommended | User Choice | Notes |
|---|----------|---------|-------------|-------------|-------|
| 1 | ... | A/B/C | B | B | ... |
```

## Handoff Packet Template (Opus -> Haiku)

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
- Planning gate: scope, assumptions, and acceptance criteria are explicit.
- Clarification gate: each open requirement has a logged question with 3+ options and a recommendation.
- Delegation gate: each delegated task is bounded and verifiable.
- Integration gate: checks pass and behavior matches feature intent.
- Release gate: risk, rollout, and rollback notes are documented.

## Completion Checklist
- Feature objective is achieved and measurable.
- All acceptance criteria are met.
- Tests cover main path and key edge cases.
- Cost target is respected.
- Final summary includes risks and follow-ups.

## Example Prompts
- /bosskung-plan Plan a billing alert feature with backward compatibility and minimal cost.
- /bosskung-plan Plan a profile settings rewrite and delegate implementation tasks efficiently.
- /bosskung-plan Plan API pagination improvements with strict acceptance tests and explicit risk controls.
