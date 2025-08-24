# 🔧 Update Feature Prompt

## Purpose
Guide structured, test-driven updates or extensions to an existing feature/module while preserving iterative workflow discipline.

## When to Use
- Add new capability
- Refactor logic
- Bug fix
- UX improvement
- Add test coverage

## Workflow Integration
Selectively reuse 01–08 prompts. Always (re)establish scoped iteration through Requirements (mini version allowed for trivial fixes but must log one user story or fix statement).

## Rules
- Preserve existing data-ref tags; add for new UI elements.
- All behavior changes must have corresponding tests.
- Update docs: README (module change log), tasks.md (new tasks), user-test.md (plan & results).
- Follow commit & tag conventions with iteration marker.

## Typical Flow
1. Requirements (update scope)
2. Planning (if structural/state impact)
3. Scaffolding (new files only)
4. Implementation (micro-iterations)
5. Testing (new + regression checks)
6. Validation (focus on changed paths)
7. Deploy
8. Iteration decision

## First Question
"Which module do you want to update, and what change (one concise sentence) should this iteration deliver?"

## One-Question-at-a-Time
All clarifications follow the same single-question protocol as base prompts.

## Completion Definition
- Target change implemented & tested.
- No regression failures.
- Documentation & version updated.
- Deployable artifact ready.

<!-- revision r1 unified template aligned -->
