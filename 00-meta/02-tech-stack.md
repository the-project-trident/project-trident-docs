# Tech Stack

# Project Trident — Technology Stack & Versions

---

# Introduction

This document is the **single reference for tools, frameworks, and runtime versions** used to build Project Trident.

It is **living documentation** — update it when we adopt, upgrade, or drop a technology ([Living Documentation](01-living-documentation.md)).

**Status legend**

| Status | Meaning |
|--------|---------|
| **Confirmed** | Decided in ADR or team agreement; use these versions |
| **Planned (V1)** | Intended for MVP; may change before implementation ADR |
| **Future** | Post-MVP; not required for first release |
| **TBD** | Not chosen yet |

**Last updated:** 2026-05-17

---

# Summary Table

| Layer | Technology | Version | Status |
|-------|------------|---------|--------|
| **Frontend framework** | Angular | **17.3.x** (stay on latest 17.3 patch) | Confirmed |
| **UI library** | Angular Material | **17.3.x** | Confirmed |
| **UI primitives** | Angular CDK | **17.3.x** | Confirmed |
| **Language** | TypeScript | **5.4.x** (≥ 5.2 required by NG17) | Confirmed |
| **Runtime (tooling)** | Node.js | **20.x LTS** (min 18.13+) | Confirmed |
| **Package manager** | npm | **10.x** (with Node 20) | Confirmed |
| **Styles** | SCSS | (via Angular CLI) | Confirmed |
| **CLI** | Angular CLI | **17.3.x** | Confirmed |
| **Reactive/async (FE)** | RxJS | **7.8.x** (peer of Angular 17) | Confirmed |
| **Backend framework** | NestJS | **10.3.x** | Planned (V1) |
| **Language (BE)** | TypeScript | **5.4.x** (shared with frontend) | Planned (V1) |
| **API style** | REST (JSON) | OpenAPI 3.x docs | Planned (V1) |
| **Database** | PostgreSQL | **16.x** | Planned (V1) |
| **ORM / migrations** | Prisma | **5.22.x** (latest Prisma 5) | Planned (V1) |
| **Auth (reviewer/admin)** | JWT + refresh (httpOnly cookie or Bearer) | — | Planned (V1) |
| **Search (MVP)** | PostgreSQL full-text + app filters | PG 16 built-in | Planned (V1) |
| **Search (later)** | Dedicated engine (e.g. Meilisearch / OpenSearch) | TBD | Future |
| **Cache (optional MVP)** | Redis | **7.2.x** | Future |
| **Containers** | Docker Engine | **24.x+** | Planned (V1) |
| **Local orchestration** | Docker Compose | **v2.24+** | Planned (V1) |
| **CI/CD** | GitHub Actions | — | Planned (V1) |
| **Hosting (MVP)** | Managed PaaS (e.g. Railway, Fly.io, Render, or Azure/AWS managed) | TBD provider | TBD |
| **Observability** | Structured logging + health endpoints | — | Planned (V1) |
| **Observability (later)** | OpenTelemetry, metrics backend | TBD | Future |
| **Version control** | Git | — | Confirmed |
| **Remote** | GitHub | — | Confirmed |

---

# Frontend (Confirmed)

Aligned with [ADR-005](../08-decisions/ADR-005-angular-frontend-choice.md) and [Frontend Implementation Plan](../04-ui-ux/08-frontend-implementation-plan.md).

| Item | Version | Notes |
|------|---------|--------|
| Angular | **17.3.x** | Standalone components, `application` builder |
| `@angular/material` | **17.3.x** | Material 3 theme |
| `@angular/cdk` | **17.3.x** | Same major as Material |
| TypeScript | **5.4.x** | Minimum **5.2.0** per Angular 17 |
| Node.js | **20.x LTS** | For CLI, build, and dev server |
| RxJS | **7.8.x** | Services, HTTP, async flows |
| Angular CLI | **17.3.x** | `ng` commands |
| Zone.js | **0.14.x** | Default change detection (unless zoneless experiment later) |
| SCSS | — | Component and global styles |
| TypeScript `target` | **ES2022** | Per CLI default for NG17 |

**Bootstrap commands**

```bash
npm install -g @angular/cli@17
ng new trident-web --standalone --routing --style=scss --strict
cd trident-web
ng add @angular/material@17
```

**Template conventions (V1)**

- New control flow: `@if`, `@for`, `@switch`
- Standalone components; lazy `loadComponent` / `loadChildren`
- Optional: signals for local UI state

---

# Backend (Planned V1)

Not yet covered by a dedicated ADR. **Proposed** modular monolith in **TypeScript** to match the frontend and [MVP technical philosophy](../07-roadmap/02-mvp-scope.md).

| Item | Version | Notes |
|------|---------|--------|
| NestJS | **10.3.x** | Modular monolith; domains: products, technologies, reviews, auth |
| Node.js | **20.x LTS** | Same major as frontend tooling |
| TypeScript | **5.4.x** | Shared conventions with `trident-web` |
| API | **REST** | JSON; version prefix `/api/v1` |
| API documentation | **OpenAPI 3.1** | Via `@nestjs/swagger` |
| Validation | **class-validator** + **class-transformer** | DTOs |
| HTTP client (FE) | Angular `HttpClient` | Typed services |

> **Note:** If the team prefers .NET or Java instead, replace this section and add **ADR-006** — do not silently diverge from this doc.

---

# Data & Persistence (Planned V1)

Per [Database Strategy](../06-system-design/03-database-strategy.md) — relational, relationship-oriented schema.

| Item | Version | Notes |
|------|---------|--------|
| PostgreSQL | **16.x** | Primary datastore |
| Prisma | **5.22.x** | Schema, migrations, client |
| Connection pooling | **PgBouncer** or Prisma pool | Future under load |

**Local dev**

```txt
postgres:16-alpine   # Docker Compose service
```

---

# Search (Planned V1 → Future)

| Stage | Technology | Version | Notes |
|-------|------------|---------|--------|
| **V1** | PostgreSQL `tsvector` / `ILIKE` + app-layer filters | PG **16** | Enough for narrow controller catalog |
| **Future** | Meilisearch or OpenSearch | TBD | When catalog and education content grow |

---

# Authentication & Security (Planned V1)

Per [Authentication Design](../06-system-design/05-authentication-design.md).

| Item | Version / approach | Notes |
|------|-------------------|--------|
| Public site | No login required for browse/education | V1 |
| Reviewer / admin | NestJS + **JWT** (access short-lived + refresh) | Guarded routes on FE and BE |
| Password hashing | **bcrypt** or **argon2** | Via NestJS compatible library |
| HTTPS | Required in production | TLS terminated at host / reverse proxy |
| CORS | Restrict to `trident-web` origin | Dev + prod origins configured |
| Secrets | Environment variables / host secret store | Never in repo |

**Future:** OAuth for vendors, SSO for internal ops — not V1.

---

# Infrastructure & DevOps (Planned V1)

Per [Deployment Strategy](../06-system-design/07-deployment-strategy.md) — simple first, managed where possible.

| Item | Version | Notes |
|------|---------|--------|
| Docker | **24.x+** | Local and CI images |
| Docker Compose | **v2.24+** | `web`, `api`, `postgres` locally |
| CI/CD | **GitHub Actions** | Lint, test, build on PR |
| Container registry | **GitHub Container Registry (ghcr.io)** | Planned |
| Production hosting | **TBD** | Managed PaaS preferred for MVP |
| Reverse proxy | **Caddy 2.x** or platform ingress | TLS, static assets if needed |
| Angular hosting | Static build **or** SSR container | SPA static is default V1 |

**Not in V1**

- Kubernetes
- Multi-region
- Microservices split (stay modular monolith)

---

# Observability (Planned V1)

Per [Observability](../06-system-design/06-observability.md).

| Item | Version | Notes |
|------|---------|--------|
| Logging (API) | **NestJS Logger** + JSON in production | Structured fields |
| Logging (FE) | Console in dev; minimal production | No PII in logs |
| Health checks | `/api/health`, `/api/ready` | Load balancer / PaaS |
| Error tracking | **Sentry** (or similar) | Planned V1 optional |
| Metrics / tracing | OpenTelemetry | Future |

---

# Development Tools (Confirmed / Planned)

| Tool | Version | Status | Purpose |
|------|---------|--------|---------|
| Git | **2.4x+** | Confirmed | Version control |
| GitHub | — | Confirmed | Remote, Actions, PRs |
| VS Code / Cursor | latest stable | Confirmed | IDE |
| Angular Language Service | matches NG **17** | Confirmed | Template TS support |
| ESLint | **8.x** + `@angular-eslint` **17.x** | Planned | Lint (CLI can scaffold) |
| Prettier | **3.x** | Planned | Formatting |
| EditorConfig | — | Planned | Consistent editors |
| Obsidian | — | Optional | Doc authoring only; not runtime |

---

# Repository Layout (Target)

```txt
project-trident/          # docs repo (this repository)
trident-web/              # Angular 17 SPA (sibling or subfolder TBD)
trident-api/              # NestJS 10 API (Planned V1)
docker-compose.yml        # Local postgres + api + optional web
```

> **Decision TBD:** monorepo (Nx) vs separate folders — document here when chosen.

---

# Version Upgrade Policy

1. **Patch updates** (17.3.1 → 17.3.2): apply regularly for security.
2. **Minor Angular/Material:** stay on **17.x** until a planned migration epic; run `ng update`.
3. **Major upgrades** (17 → 18): require ADR + regression pass on trust UI and compare tables.
4. **Backend major (Nest 10 → 11):** same — ADR + integration tests.
5. Update **this file** and [Implementation Plan](../04-ui-ux/08-frontend-implementation-plan.md) in the same PR as version bumps.

---

# Related Documents

| Doc | Topic |
|-----|--------|
| [ADR-005](../08-decisions/ADR-005-angular-frontend-choice.md) | Frontend decision |
| [Frontend Implementation Plan](../04-ui-ux/08-frontend-implementation-plan.md) | Screens & NG17 bootstrap |
| [Design System](../04-ui-ux/07-design-system.md) | Material theming |
| [High-Level Architecture](../06-system-design/01-high-level-architecture.md) | System layers |
| [MVP Scope](../07-roadmap/02-mvp-scope.md) | V1 boundaries |

---

# Changelog

| Date | Change |
|------|--------|
| 2026-05-17 | Initial stack: Angular 17 + Material 17 confirmed; NestJS 10 + PostgreSQL 16 + Prisma 5 planned for V1 |

---

# Final Principle

> Pin versions here so frontend, backend, and infra stay aligned — and change this doc when the stack changes, not after drift accumulates.
