# AI-Assisted SaaS Development Template

Opinionated prompt architecture for Next.js SaaS applications, enabling small, fully testable iterations with strict separation between PROCESS (workflow) and SOLUTION (SaaS technology stack).

## SaaS Stack Focus

This template is specifically designed for **Next.js SaaS applications** with:
- Next.js/TypeScript framework
- Supabase backend integration
- Modern web development tooling
- Cloud deployment strategies

## Structure

```
prompts/
  workflow/         # Unified 8-step workflow (consolidated)
  actions/          # Entry orchestration prompts (create/update feature, start project)
  stacks/           # SaaS/Next.js specific stack descriptors
docs/               # Global docs (changelog, architecture, backlog)
.github/workflows/  # SaaS CI/CD pipeline
Dockerfile          # Container configuration for deployment
```

## Core Principles
- One question at a time
- Each iteration = deployable slice (requirements → deploy cycle complete)
- Automated + manual test coverage every slice
- Workflow agnostic of stack; SaaS stack injects Next.js structure & tooling
- Traceability: acceptance tests ↔ tasks ↔ code stubs ↔ commits

## Usage Flow
1. Run `start-project` action prompt → loads Next.js SaaS stack.
2. Use `create-feature` (or `update-feature`).
3. Step through 01–08 prompts; each iteration loops until value delivered.

## SaaS-Specific Features
- Next.js server-side rendering and API routes
- Supabase integration for database and authentication
- Stripe payment integration capabilities
- Cloud deployment with Docker containers
- Modern web performance optimization

## Versioning & Commits
- Conventional Commits + iteration marker `[iNN]`
- Tag: `vMAJOR.MINOR.PATCH+feature-slug.iNN`

## SaaS Stack Configuration
The included stack configuration (`prompts/stacks/stack-saas.md`) provides:
- Next.js/TypeScript tech stack details
- SaaS application folder structure
- Testing strategy for web applications
- Cloud deployment targets

## Prompt Index
See `PROMPTS_INDEX.md` for detailed cross-reference of SaaS-specific prompts.

## Backlog
Maintain optional `docs/BACKLOG.md` for deferred SaaS features surfaced during Iteration prompt.

## Extensibility
New SaaS-specific steps may be added (e.g., Payment Integration, Analytics Setup) without modifying the core workflow.

---
© 2025 SaaS Development Template
