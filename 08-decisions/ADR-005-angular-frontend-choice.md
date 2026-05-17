# ADR-005 — Angular Frontend Architecture Choice

# Status

Accepted

---

# Date

2026-05-17

---

# Supersedes

[ADR-004 — React Frontend Architecture Choice](ADR-004-react-choice.md) (status: Superseded)

---

# Context

Project Trident requires a frontend architecture capable of supporting:

- technology-first discovery,
- educational experiences,
- comparison systems,
- trust-oriented UX,
- structured reviewer operations,
- and long-term platform scalability.

The team has chosen to standardize on **Angular** for implementation velocity, structural consistency, and integrated tooling.

The public experience must remain **calm, editorial, and trust-first** — not marketplace- or enterprise-default styling. UI library choice and theming are therefore part of this decision.

---

# Decision

Project Trident will adopt:

- **Angular** (current LTS) with **TypeScript**
- **Angular Material** and **Angular CDK** for UI components
- **Angular Router** for public and internal route shells
- **Standalone components** as the default component model

Optional as needed for MVP and beyond:

- **Angular SSR** (or hybrid rendering) for SEO on education and trust pages
- **RxJS** for async flows (used idiomatically with Angular services)

The architecture will prioritize:

- modularity,
- maintainability,
- scalability,
- structured feature boundaries,
- and explainable UI behavior.

---

# UI & Design System

**Angular Material** is the default component library.

Material must be **themed** for Project Trident’s calm editorial identity. See:

[Design System — Angular Material](../04-ui-ux/07-design-system.md)

Core rules:

- neutral palette, restrained accent,
- low elevation on public surfaces,
- trust layers visually separated (vendor / user / platform),
- no marketplace-style conversion patterns in global chrome.

---

# Reasons for Decision

Angular was selected because:

- strong integrated tooling (CLI, routing, forms, testing),
- opinionated structure suitable for growing domain complexity,
- excellent fit for **comparison tables**, **reviewer workflows**, and **form-heavy** verification UI,
- first-class **TypeScript** support,
- team preference and implementation speed for this project.

Angular Material provides:

- accessible primitives (`MatTable`, `MatTab`, `MatExpansion`, forms, toolbar, sidenav),
- consistent patterns for internal operational screens,
- a customizable Material 3 theme when tuned for editorial calmness.

---

# Architectural Philosophy

The frontend architecture should prioritize:

- clarity,
- maintainability,
- feature-based folder structure,
- and explainable UI behavior.

The platform should avoid:

- unnecessarily complex state management in V1,
- excessive abstraction,
- trend-driven UI engineering,
- default Material styling without a Trident theme.

The frontend should evolve:

- gradually,
- and intentionally.

---

# Suggested MVP Structure

```txt
src/app/
├── core/              # shell, nav, interceptors, guards
├── shared/            # trust badges, pipes, shared Material wrappers
├── features/
│   ├── home/
│   ├── technologies/
│   ├── products/
│   ├── compare/
│   ├── transparency/
│   └── reviewer/      # authenticated internal area
└── styles/            # Material theme, tokens
```

Public routes align with [Navigation Flow — V1 Global Header](../04-ui-ux/02-navigation-flow.md#v1-global-header-navbar).

---

# Implications

This decision influences:

- frontend repository layout,
- Angular Material theme and design tokens,
- component and module boundaries,
- SSR/SEO strategy for education pages,
- reviewer app routing and auth guards,
- API client patterns (services + typed models).

---

# TypeScript Direction

TypeScript is **required** for application code.

Use typed models for:

- products,
- technologies,
- verification states,
- trust layers,
- and comparison data.

---

# Performance Philosophy

Frontend performance should prioritize:

- responsiveness,
- readability,
- and smooth educational exploration.

Avoid premature optimization. Prefer:

- lazy-loaded feature routes,
- lean bundles per area,
- server rendering only where SEO or first paint clearly benefit.

---

# Alternatives Considered

## React + component libraries (previous ADR-004)

Previously accepted. Superseded because:

- the team will implement faster and more consistently in Angular,
- Angular Material maps well to tables, forms, and reviewer tooling,
- integrated Angular structure reduces early architectural drift.

React remains a valid stack for similar products; it is not the choice for Project Trident.

---

## Vue

Considered for simplicity.

Rejected for this project due to team direction toward Angular and Material.

---

## Server-rendered templates only

Rejected because the product requires dynamic comparison, trust UI, and reviewer workflows.

---

# Long-Term Consequences

The platform will evolve toward:

- a modular Angular application,
- a shared Trident Material theme,
- separate public and reviewer feature areas,
- and trust-oriented reusable components.

Disciplined theming is required so Material defaults do not undermine platform identity.

---

# Enforcement Principles

- Use Angular Material through **shared wrappers** where Trident-specific trust UI repeats.
- Keep vendor, user, and platform signals **visually distinct** on product and compare screens.
- Do not introduce paid-placement or marketplace patterns in navigation or layout components.
- Prefer clarity over clever abstractions.

---

# Final Principle

> Frontend architecture should support clarity, maintainability, and trust-oriented experiences using Angular and a carefully themed Angular Material system — not default marketplace or enterprise UI patterns.
