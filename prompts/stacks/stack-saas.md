# 🌐 SaaS Stack

## 🧱 Project Type

**Software-as-a-Service (SaaS) Web Application** built with a modern, modular Next.js stack. This stack emphasizes type-safety, testability, security (RLS), and iterative delivery.

---

## 🧰 Technology Choices & Rationale

### Core Stack
* **Framework:** Next.js 14.0.4 (TypeScript) — Server-side rendering, type safety, ecosystem maturity
* **Data Platform:** Supabase 2.38.4 — PostgreSQL + RLS, Auth, Storage, Edge Functions (reduces backend complexity)
* **Styling:** Tailwind CSS 3.4.1 + shadcn/ui — Utility-first CSS with accessible components
* **State/Forms:** React Hook Form 7.48.2 + Zod 3.22.4 — Type-safe form handling and validation

### Supporting Technologies
* **Auth:** Supabase Auth (OAuth, magic links, email/password)
* **Testing:** Vitest 1.1.0 + Playwright 1.40.1 (unit + E2E coverage)
* **Deployment:** Vercel or Docker containers
* **Optional Services:** Stripe (payments), Resend/Postmark (email), PostHog/Mixpanel (analytics)

### Architecture Decisions
* **Server-First:** Prefer server components, server actions, RLS-protected queries
* **Modular Design:** Feature-based organization with isolated modules
* **Type Safety:** Strict TypeScript + Zod runtime validation for external data

---

## 📋 Quality Framework Summary

* **Testing Standards:** >85% code coverage, comprehensive E2E testing
* **Performance Targets:** Web Vitals compliance (CLS ≤ 0.1, LCP ≤ 2.5s, FID ≤ 100ms)
* **Security Requirements:** RLS enabled, CSRF protection, input validation
* **Accessibility Standards:** WCAG 2.1 AA compliance
* **CI/CD Pipeline:** Automated testing, security scanning, deployment gates

> **Complete Quality Gates:** See `docs/quality-gates.md` for detailed measurable criteria

---

## 📁 Architecture Pattern

### Folder Structure Philosophy
```
app/                    # Next.js app router
├── modules/            # Feature-based organization
│   └── {feature}/      # Isolated feature modules
│       ├── components/ # UI components for feature
│       ├── services/   # Data + business logic
│       ├── hooks/      # Custom React hooks
│       └── tests/      # Feature tests
├── lib/                # Shared utilities
└── public/             # Static assets
```

### Design Principles
* **Modularity:** Each feature is self-contained with its own components, services, and tests
* **Server-First:** Leverage Next.js server components and server actions
* **Type Safety:** Strict TypeScript with Zod validation for external data
* **Security:** Row Level Security (RLS) policies protect all data access

---

## 🔄 Integration with Workflow

This stack definition is consumed by:
* `start-project.prompt.md` — Project initialization and stack selection
* `create-feature.prompt.md` — Feature development orchestration
* `update-feature.prompt.md` — Feature modification workflows
* Generic 8-step development flow — Technology-specific implementations

### Implementation Details
> **Complete Setup Guide:** See `prompts/stacks/instructions_saas.md` for:
> - Detailed installation and configuration steps
> - Coding standards and best practices
> - Testing strategies and examples
> - Security implementation guidelines
> - Performance optimization techniques

### Quality Assurance
> **Quality Framework:** See `docs/quality-gates.md` for measurable success criteria at each workflow step

### Automation
> **CI/CD Pipeline:** See `.github/workflows/saas-ci.yml` for automated testing and deployment configuration
