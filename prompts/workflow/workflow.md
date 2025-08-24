# Default Development Workflow

> Consolidated verbatim content of the 8 modular step prompt files (01–08). Use this when a single-file workflow reference is preferred.

---

## 01 – Requirements

### 1. Purpose
Capture and lock a **small, fully testable iteration slice** of a feature/module: value delivered, success conditions, and measurable acceptance criteria. Scope ONLY this iteration (Iteration iNN).

### 2. Inputs to Collect (one question at a time)
1. Feature/module name (slug)
2. Iteration goal (single concise user-facing outcome)
3. Primary user persona / actor
4. Problem / pain addressed
5. Single user story (As a <persona> I want <action> so that <outcome>)
6. Functional capabilities (bullet list, testable now)
7. Explicit exclusions / out-of-scope
8. Preconditions / external dependencies
9. Data touched (read/write; abstract)
10. Acceptance test scenarios (Given / When / Then list)
11. Risks / edge cases
12. Definition of Done confirmation (user must ACCEPT)

### 3. Constraints / Rules
- Exactly ONE user story per iteration.
- Must be deployable independently.
- At least one automated and one manual test will result.
- No tech/implementation detail—stack handles later.
- Reference existing naming, commit & version conventions (don't restate).

### 4. Assistant Behavior
- Ask exactly one question; wait for answer.
- After each answer show updated structured draft (with TBD placeholders).
- Clarify ambiguity with a micro-question (consumes next slot).
- On completion: show full summary & request ACCEPT or CHANGES.
- On CHANGES: modify only requested fields; redisplay; reconfirm.

### 5. Step Actions
1. Q/A loop to gather inputs.
2. Build Acceptance Test list (each capability → ≥1 test id AT-001...).
3. Derive atomic task list (to populate tasks.md later / update existing).
4. On ACCEPT: freeze scope; record start timestamp.
5. Update README requirements section & user-test planned tests.

### 6. Required Artifacts / Files
- modules/{feature}/README.md → Section: "## Iteration iNN – Requirements".
- modules/{feature}/tasks.md → Unchecked tasks referencing test IDs.
- modules/{feature}/user-test.md → "## Iteration iNN – Planned Manual Tests".

### 7. Completion Criteria
- All 12 inputs answered & ACCEPTED.
- Each capability maps to ≥1 acceptance test.
- Tasks list present & traceable.
- User explicitly typed ACCEPT / CONFIRM.

### 8. Handoff Question
"Proceed to Planning for Iteration iNN? (yes/adjust/cancel)"

### 9. Failure / Retry
- Overscoped: propose 2–3 smaller slices.
- Missing dependency data: propose assumptions for approval.
- Cancel: offer to save draft summary.

### 10. Metrics
- Capability count
- Acceptance test count
- Risk count
- Complexity (Low/Med/High)
- Start timestamp

---

## 02 – Planning

### 1. Purpose
Convert accepted requirements into a lean internal design & implementation map for Iteration iNN (stack-agnostic structure).

### 2. Inputs to Collect (one question at a time)
1. Requirements recap confirmation (changes? Y/N)
2. Components / screens / views list
3. User actions per component
4. State elements (name, purpose) this iteration
5. External services / data sources (abstract)
6. Error & edge case handling list
7. Navigation / flow steps (ordered)
8. Non-UI elements (validators, schedulers, background jobs)
9. Performance / latency sensitivities
10. Security / permission considerations
11. Acceptance test → component/state mapping confirmation
12. Planning completeness ACCEPT

### 3. Constraints / Rules
- No new capabilities beyond Requirements.
- All state maps to at least one acceptance test.
- Avoid deep coupling; prefer clear boundaries.

### 4. Assistant Behavior
- After each answer show evolving plan structure (Components, Actions, State, Flow, Errors, Security, TestMapping).
- If user attempts scope expansion warn & offer to re-open Requirements.
- Provide up to 3 option suggestions when user unsure.

### 5. Step Actions
1. Show recap; confirm.
2. Gather planning inputs sequentially.
3. Build mapping table (Acceptance Test → Responsible Component).
4. Refine tasks (split if necessary) maintaining traceability IDs.
5. Update README Planning section.

### 6. Required Artifacts / Files
- modules/{feature}/README.md → Append "### Iteration iNN – Planning".
- modules/{feature}/tasks.md → Update / refine tasks.

### 7. Completion Criteria
- All inputs answered & ACCEPTED.
- Full mapping coverage of acceptance tests.
- No scope drift.

### 8. Handoff Question
"Proceed to Scaffolding for Iteration iNN? (yes/adjust/cancel)"

### 9. Failure / Retry
- Missing clarity: propose template pattern examples.
- Overdesign: recommend minimal viable subset.

### 10. Metrics
- Component count
- State item count
- Mapping completeness %

---

## 03 – Scaffolding

### 1. Purpose
Create/update minimal file & folder skeleton for Iteration iNN per active stack rules (no premature implementation).

### 2. Inputs to Collect (one question at a time)
1. Confirm module slug & base path
2. Does module folder exist? (Y/N)
3. Required subdirectories for this iteration (stack-derived)
4. Mandatory placeholder files (README, tasks, user-test presence) confirm
5. Interface / contract stubs (models/services/controllers) needed? (list)
6. Test placeholder files (names & locations) confirm

### 3. Constraints / Rules
- All structure must derive from stack file; no invention.
- Only stubs / headers; minimal comments linking acceptance test IDs.
- Re-runs are idempotent; no duplication.

### 4. Assistant Behavior
- Present proposed structure diff; ask for approval.
- Provide one-line rationale for each directory.
- On approval output final scaffold summary.

### 5. Step Actions
1. Derive canonical structure.
2. Compute delta vs existing.
3. List files to add with rationale.
4. Provide stub content outlines.
5. Update tasks referencing stubs.

### 6. Required Artifacts / Files
- Created directories/files per stack & iteration needs.
- Updated README referencing new stubs if needed.

### 7. Completion Criteria
- User approves structure.
- All required placeholders enumerated.
- Tasks updated with stub references.

### 8. Handoff Question
"Proceed to Implementation for Iteration iNN? (yes/adjust/cancel)"

### 9. Failure / Retry
- File conflict: propose merge vs rename vs skip.
- Uncertain directory: mark deferred & ensure no dependent task.

### 10. Metrics
- New dirs count
- New files count
- % acceptance tests with placeholder linkage

---

## 04 – Implementation

### 1. Purpose
Deliver iteration slice via micro-iterations: implement smallest testable unit → test → (optional manual confirm) → commit.

### 2. Inputs to Collect (loop per micro-iteration; one question at a time)
1. Select next target task (show remaining tasks list)
2. Expected behavior (link acceptance test IDs)
3. Need mocks/stubs? (Y/N details)
4. Edge case to include? (if none skip)
5. Proceed to implementation? (confirm)

### 3. Constraints / Rules
- Each micro-iteration ≤ small atomic change with matching test.
- Add/update automated test before commit.
- Add `data-ref` to new UI (temporary).
- No unrelated refactors (create separate backlog task instead).

### 4. Assistant Behavior
- Provide concise pseudo-outline first.
- Ask for approval before presenting full code & test.
- After tests: request pass/fail status (one failing test at a time).
- Track remaining tasks & display progress percentage.

### 5. Step Actions
1. Present remaining tasks.
2. Outline & propose code + test for chosen task.
3. Guide running tests; handle failures sequentially.
4. On green tests: prepare commit message draft (Conventional Commit + [iNN]).
5. Repeat until all iteration tasks complete.

### 6. Required Artifacts / Files
- Implemented code & tests.
- Optional README "Implementation Notes" subsection.

### 7. Completion Criteria
- All iteration tasks done.
- All related tests green.
- No open critical defects.
- User approves status.

### 8. Handoff Question
"Proceed to Testing consolidation for Iteration iNN? (yes/adjust)"

### 9. Failure / Retry
- Persistent failing test: propose isolation or splitting task.
- Scope creep: move new ideas to backlog.

### 10. Metrics
- Micro-iterations count
- Tests added
- Failures resolved

---

## 05 – Testing

### 1. Purpose
Ensure comprehensive automated test coverage & readiness for manual validation.

### 2. Inputs to Collect (one question at a time)
1. Confirm acceptance test list (show enumerated)
2. For each unmapped acceptance test: select test type (unit/ui/integration/e2e/manual-only)
3. Coverage threshold? (Y/N value)
4. Any flaky areas needing retries? (Y/N)
5. Confirm readiness to execute full suite (ACCEPT)

### 3. Constraints / Rules
- Each acceptance test must be automated or explicitly manual-only (annotate reason).
- Prefer targeted unit tests over broad integration where feasible.
- Test names include acceptance test ID suffix.

### 4. Assistant Behavior
- Display gaps; propose skeleton tests.
- Provide concise failure diagnosis suggestions.
- Ask before recommending structural refactors.

### 5. Step Actions
1. Map acceptance tests → automation plan.
2. Generate missing test skeletons.
3. Execute (guide) full suite; list pass/fail.
4. Iterate fixes until green.
5. Summarize matrix & coverage.
6. Update user-test with automated summary & remaining manual tests.

### 6. Required Artifacts / Files
- Implemented test files.
- user-test.md → "Automated Test Summary – Iteration iNN".
- (Optional) README coverage note.

### 7. Completion Criteria
- All planned automated tests pass.
- All acceptance tests mapped.
- User confirms readiness for manual validation.

### 8. Handoff Question
"Proceed to Manual Validation for Iteration iNN? (yes/adjust)"

### 9. Failure / Retry
- Persistent failing test: isolate minimal repro instructions.
- Coverage below threshold: list top uncovered logical branches.

### 10. Metrics
- Automated tests added
- Pass rate
- Coverage % (if available)

---

## 06 – Validation

### 1. Purpose
Perform manual validation (one test at a time) confirming iteration readiness for deployment.

### 2. Inputs to Collect (one question at a time)
1. Confirm environment (simulator/device/staging)
2. For each manual test: result? (Pass/Fail/Blocked) + notes
3. For any failure: fix now or defer? (loop if fix)
4. Final validation approval (ACCEPT)

### 3. Constraints / Rules
- Single test presentation at a time.
- A fail requires explicit note & linked acceptance test ID.
- Deferred = must create follow-up task before deployment.

### 4. Assistant Behavior
- Format per test: Purpose → Precondition → Action → Expected → Result?.
- On fail: propose triage path (quick fix vs defer) + update table.
- Keep running validation summary visible.

### 5. Step Actions
1. Load manual tests from user-test.md.
2. Iterate sequentially, recording outcomes.
3. Handle failures (fix or create task & mark deferred).
4. Generate Validation Summary & timestamp.
5. Update docs accordingly.

### 6. Required Artifacts / Files
- user-test.md → "Manual Validation Results – Iteration iNN".
- tasks.md → Added follow-up tasks for deferrals.

### 7. Completion Criteria
- All tests pass or are deferred with tasks.
- User ACCEPTS deployment readiness.

### 8. Handoff Question
"Proceed to Deployment for Iteration iNN? (yes/adjust)"

### 9. Failure / Retry
- >30% failures: recommend partial rollback or extra micro-iteration.

### 10. Metrics
- Pass count / total
- Deferred count
- Validation duration

---

## 07 – Deploy

### 1. Purpose
Produce production-ready artifacts & version tagging for iteration slice with traceability.

### 2. Inputs to Collect (one question at a time)
1. Confirm validation pass (Y/N)
2. Version bump type (auto-suggest) accept? (Y/N override?)
3. Tag metadata (feature-slug + iNN) confirm
4. Artifact targets (Docker / iOS / Android) confirm
5. Release notes bullet list confirm
6. Commit & tag approval (ACCEPT)

### 3. Constraints / Rules
- Must have green tests & validation ACCEPT.
- Conventional Commit + [iNN] marker.
- Tag: vX.Y.Z+feature-slug.iNN.
- Artifacts reproducible via documented commands.

### 4. Assistant Behavior
- Suggest semantic bump based on change types.
- Draft commit message & tag; request approval.
- Provide artifact build commands abstractly (stack-specific executed externally).
- Summarize release outputs.

### 5. Step Actions
1. Verify prior criteria.
2. Determine version bump & tag.
3. Present commit + tag drafts.
4. Outline artifact build process.
5. Update CHANGELOG & README iteration summary.
6. Capture iteration duration.

### 6. Required Artifacts / Files
- CHANGELOG.md updated.
- tasks.md iteration tasks checked.
- README.md iteration summary appended.
- RELEASES.md / artifact manifest (optional).

### 7. Completion Criteria
- Commit approved & created.
- Tag defined & queued for push.
- Artifact build steps acknowledged.
- Docs updated.

### 8. Handoff Question
"Start Iteration Review? (yes/finish)"

### 9. Failure / Retry
- Build failure: capture error summary & propose fixes.

### 10. Metrics
- Iteration duration
- Tests count
- Artifacts produced

---

## 08 – Iteration

### 1. Purpose
Decide next action after deployment: extend feature, start new feature, update other module, refactor, or end session.

### 2. Inputs to Collect (one question at a time)
1. Satisfaction rating (1–5 or short text)
2. Immediate follow-up improvements? (list / none)
3. Choose next action: [extend / new feature / update module / refactor / end]
4. If extend: next capability statement → confirm start new iteration?
5. If new feature: name → proceed to Requirements.
6. If update other module: target module → proceed to update-feature prompt.
7. If refactor: target + rationale → create backlog tasks → proceed? (Y/N)
8. If end: confirm closure summary.

### 3. Constraints / Rules
- Single path per cycle.
- New desires not chosen logged as backlog.
- Extension/new/update triggers fresh Requirements step.

### 4. Assistant Behavior
- Present concise iteration summary (value delivered, version, tests, duration) first.
- Offer backlog display on request.
- Encourage small next slice.

### 5. Step Actions
1. Show summary.
2. Collect decision inputs.
3. Log backlog items not selected.
4. Route accordingly or finalize.

### 6. Required Artifacts / Files
- README.md → Append iteration summary line.
- BACKLOG.md (optional) → updated.

### 7. Completion Criteria
- Next action clearly chosen.
- Backlog updated.
- User confirms transition or closure.

### 8. Handoff Question
Contextual: e.g., "Begin Requirements for Iteration i(N+1)?" or closure message.

### 9. Failure / Retry
- Indecision: propose top 3 high-value small slices with effort estimates.

### 10. Metrics
- Satisfaction rating
- Backlog additions count

---

© 2025 Unified Workflow (Full Content r1)