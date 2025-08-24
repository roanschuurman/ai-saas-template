# SaaS Development Prompt Index

| Category | Path | Purpose |
|----------|------|---------|
| Workflow | prompts/workflow/workflow.md | Unified 8-step SaaS development workflow |
| Action | prompts/actions/start-project.prompt.md | Initialize SaaS project + load Next.js stack |
| Action | prompts/actions/create-feature.prompt.md | Orchestrate new SaaS feature lifecycle |
| Action | prompts/actions/update-feature.prompt.md | Orchestrate SaaS feature update |
| Stack | prompts/stacks/stack-saas.md | Next.js SaaS stack definition |
| Instructions | prompts/stacks/instructions_saas.md | Complete Next.js development standards |
| Quality | docs/quality-gates.md | Measurable quality criteria for SaaS development |
| Documentation | docs/CHANGELOG.md | SaaS release documentation template |
| Documentation | docs/BACKLOG.md | SaaS feature backlog management |
| Documentation | docs/ARCHITECTURE.md | SaaS system architecture documentation |
| CI/CD | .github/workflows/saas-ci.yml | Next.js automated testing pipeline |
| Deployment | Dockerfile | Next.js production container configuration |

## Cross References

| Artifact | Generated/Updated By | Notes |
|----------|----------------------|-------|
| README.md (feature/module) | 01,02,07,08 | SaaS feature iteration sections appended |
| tasks.md | 01,02,03,04,06,07 | Trace each SaaS task to acceptance test IDs |
| user-test.md | 01,05,06 | SaaS testing: planned vs automated vs manual results |
| CHANGELOG.md | 07 | SaaS semantic version entry |
| BACKLOG.md | 08 | Deferred SaaS improvements |
| quality-gates.md | All steps | SaaS quality criteria validation at each gate |
| instructions_saas.md | 01,02,03 | Next.js technical standards and setup requirements |
| saas-ci.yml | 05,07 | Next.js automated testing and deployment validation |
| Dockerfile | 07 | Container deployment configuration |

## SaaS-Specific Metrics Tracked
- Next.js application performance (Web Vitals)
- Supabase query performance and RLS compliance
- End-to-end test coverage for user journeys
- API route test coverage and performance
- Security scan results (dependencies, OWASP)
- TypeScript type coverage percentage
- Accessibility compliance scores (WCAG 2.1 AA)
- Cloud deployment success rates

## Next.js SaaS Quality Gates
- **Unit Testing**: >85% code coverage for components and utilities
- **Integration Testing**: API routes and database interactions tested
- **E2E Testing**: Critical user flows tested with Playwright
- **Performance**: Web Vitals compliance (CLS ≤ 0.1, LCP ≤ 2.5s, FID ≤ 100ms)
- **Accessibility**: WCAG 2.1 AA compliance
- **Security**: RLS enabled, CSRF protection, input validation
- **Type Safety**: Strict TypeScript + Zod runtime validation
- **SEO**: Server-side rendering optimization and meta tags
