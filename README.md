# AI-Assisted SaaS Development Template

[![GitHub stars](https://img.shields.io/github/stars/roanschuurman/saas-template?style=for-the-badge)](https://github.com/roanschuurman/saas-template/stargazers)
[![GitHub license](https://img.shields.io/github/license/roanschuurman/saas-template?style=for-the-badge)](https://github.com/roanschuurman/saas-template/blob/main/LICENSE)
[![CI/CD Pipeline](https://img.shields.io/github/actions/workflow/status/roanschuurman/saas-template/saas-ci.yml?style=for-the-badge&label=CI%2FCD)](https://github.com/roanschuurman/saas-template/actions)

Opinionated prompt architecture for Next.js SaaS applications, enabling small, fully testable iterations with strict separation between PROCESS (workflow) and SOLUTION (SaaS technology stack).

## SaaS Stack Focus

This template is specifically designed for **Next.js SaaS applications** with:
- Next.js/TypeScript framework
- Supabase backend integration
- Modern web development tooling
- Cloud deployment strategies

## 🚀 Quick Start

1. **Clone this template:**
   ```bash
   git clone https://github.com/roanschuurman/saas-template.git my-saas-app
   cd my-saas-app
   ```

2. **Use with AI Assistant:**
   - Load `prompts/actions/start-project.prompt.md` in your AI assistant
   - Follow the 8-step workflow for feature development
   - Reference `prompts/stacks/instructions_saas.md` for technical standards

3. **Start Development:**
   ```bash
   npm install
   npm run dev
   ```

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
