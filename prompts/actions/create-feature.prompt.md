# ✨ Create Feature Prompt
<!-- standardized revision marker r1 -->

This prompt guides the AI assistant in building a **new feature/module** for an existing project.

---

## 🧭 Prerequisites
Before using this prompt:
- Project must be initialized using `start-project.prompt.md`
- A stack file must be selected (`stack-mobile.md` or `stack-saas.md`)
- All shared workflow modules must be available

---

## 🧩 Workflow Sequence
Run the following modular prompt sequence to implement the feature:

01. `prompts/workflow/01-requirements.prompt.md` — Gather user/feature goals  
02. `prompts/workflow/02-planning.prompt.md` — Define screens, states, actions  
03. `prompts/workflow/03-scaffolding.prompt.md` — Create folder/file structure  
04. `prompts/workflow/04-implementation.prompt.md` — Build UI, logic, and tests iteratively  
05. `prompts/workflow/05-testing.prompt.md` — Write and run automated tests  
06. `prompts/workflow/06-validation.prompt.md` — Guide the user through a manual test  
07. `prompts/workflow/07-deploy.prompt.md` — Commit and package the feature  
08. `prompts/workflow/08-iteration.prompt.md` — Repeat steps until feature is fully built

---

## 🚦 Rules
- Follow the rules from the selected stack’s `instructions_*.md` file
- Use mock data when possible
- Add `data-ref` tags to all visible UI elements for traceability (remove before release)
- Confirm every part with the user before proceeding

---

## ✅ First Question
**“What is the name and purpose of the new feature/module you want to create?”**
