# Frontend Implementation Plan

# Angular 17 + Material — Screen Build Guide (V1)

---

# Introduction

This document is the **working implementation plan** for the Project Trident web app. It may be updated as we build; it supersedes informal chat guidance when versions conflict.

**Stack (pinned for V1):** see [Tech Stack](../00-meta/02-tech-stack.md) for the full platform list.

| Package | Version |
|---------|---------|
| Angular | **17.3.x** |
| Angular Material + CDK | **17.3.x** |
| TypeScript | **5.4.x** (≥ 5.2) |
| Node | **20.x LTS** |

Related: [ADR-005](../08-decisions/ADR-005-angular-frontend-choice.md), [Design System](07-design-system.md), [Navigation Flow](02-navigation-flow.md), [Screen List](01-screen-list.md).

Docs are **living** — see [Living Documentation](../00-meta/01-living-documentation.md).

---

# Project Bootstrap

```bash
# From repo root (suggested folder name)
ng new trident-web --standalone --routing --style=scss --strict
cd trident-web
ng add @angular/material@17
```

**Angular 17 defaults to use:**

- Standalone components (no NgModules for features),
- `application` builder,
- new control flow in templates: `@if`, `@for`, `@switch` (prefer over structural directives in new code),
- `inject()` for DI in components/services.

**Material setup:**

- Custom Material 3 theme in `src/styles/theme.scss`,
- Include `provideAnimationsAsync()` or `provideAnimations()` in `app.config.ts`,
- Typography: Roboto (Material default) unless we change in theme.

---

# Repository Layout (inside `trident-web/` or monorepo app folder)

```txt
src/app/
├── app.config.ts
├── app.routes.ts
├── core/
│   └── layout/
│       ├── app-shell.component.ts
│       ├── header.component.ts
│       └── footer.component.ts
├── shared/
│   ├── components/
│   │   ├── trust-badge/
│   │   ├── trust-layer-card/
│   │   ├── page-header/
│   │   └── content-width/
│   └── models/
│       ├── product.model.ts
│       ├── technology.model.ts
│       └── verification-state.ts
└── features/
    ├── home/
    ├── technologies/
    ├── products/
    ├── compare/
    ├── transparency/
    ├── about/
    ├── contact/
    ├── search/
    └── reviewer/          # lazy + route guard
```

---

# Routing (V1)

Public routes use `AppShellComponent` as parent layout.

| Path | Page component | Screen # (screen list) |
|------|----------------|------------------------|
| `/` | `HomePage` | 1 |
| `/technologies` | `TechnologyListPage` | 5 (hub) |
| `/technologies/:slug` | `TechnologyDetailPage` | 5 |
| `/technologies/compare` | `TechnologyComparePage` | 6 |
| `/technologies/decision` | `DecisionFrameworkPage` | 7 |
| `/products/controllers` | `CategoryDiscoveryPage` | 2 |
| `/products/:slug` | `ProductDetailPage` | 3 |
| `/compare` | `CompareHubPage` | 4 + 6 (tabs) |
| `/methodology` | `ReviewMethodologyPage` | 8 |
| `/transparency` | `TransparencyHubPage` | 9–10 (hub) |
| `/transparency/ethics` | `TrustEthicsPage` | 9 |
| `/transparency/rankings` | `HowRankingsWorkPage` | 10 |
| `/about` | `AboutPage` | 11 |
| `/contact` | `ContactPage` | footer |
| `/search` | `SearchPage` | MVP search |

```ts
// app.routes.ts (shape)
export const routes: Routes = [
  {
    path: '',
    component: AppShellComponent,
    children: [
      { path: '', loadComponent: () => import('./features/home/...') },
      // ... feature routes
    ],
  },
  {
    path: 'reviewer',
    canActivate: [reviewerGuard],
    loadChildren: () => import('./features/reviewer/reviewer.routes'),
  },
];
```

**Reviewer (internal):**

| Path | Page |
|------|------|
| `/reviewer` | Dashboard |
| `/reviewer/queue` | Product queue |
| `/reviewer/evaluate/:id` | Evaluation workspace |

---

# Screen Construction Pattern

## Layers

1. **Shell** — header/footer, `router-outlet`
2. **Page** — one per route; loads data, sets `title`
3. **Sections** — dumb presentational blocks per wireframe section
4. **Shared** — trust UI, layout wrappers

## Naming

| Type | Suffix | Example |
|------|--------|---------|
| Routed page | `*-page.component` | `product-detail-page.component.ts` |
| Section block | `*-section.component` | `product-trust-section.component.ts` |
| Shared widget | descriptive name | `trust-layer-card.component.ts` |

## Page template skeleton (Angular 17)

```html
<app-page-header [title]="product.name" />
<app-content-width>
  @if (product(); as p) {
    <app-product-overview-section [product]="p" />
    <app-product-trust-section [product]="p" />
    <!-- more sections -->
  } @else {
    <p>Loading…</p>
  }
</app-content-width>
```

Use **signals** optionally (`input()`, `signal()`, `computed()`) where it simplifies state; services can still expose `Observable` for async data in V1.

---

# Shared Components (build first)

| Component | Material base | Priority |
|-----------|---------------|----------|
| `HeaderComponent` | `MatToolbar`, `MatMenu` (Transparency) | P0 |
| `FooterComponent` | layout | P0 |
| `TrustBadgeComponent` | `MatChip` | P0 |
| `TrustLayerCardComponent` | `MatCard` outlined | P0 |
| `PageHeaderComponent` | typography | P1 |
| `ContentWidthComponent` | layout | P1 |
| `ComparisonTableComponent` | `MatTable` | P2 |

---

# Build Order (recommended)

| Sprint | Deliverable |
|--------|-------------|
| **0** | `ng new`, Material theme, `AppShell`, all routes → placeholder pages |
| **1** | Home (sections from home wireframe), Methodology, Transparency hub |
| **2** | `TrustLayerCard`, Product detail + mock `ProductService` |
| **3** | Category discovery, Technology list + detail |
| **4** | Compare hub (product + technology tabs), `MatTable` |
| **5** | Decision framework, About, Contact, Search stub |
| **6** | Reviewer lazy module + guard + dashboard stub |

Each sprint: every navbar link works; no dead routes.

---

# Data (V1)

No backend required initially.

```ts
// features/products/services/product.service.ts
@Injectable({ providedIn: 'root' })
export class ProductService {
  private readonly products = MOCK_PRODUCTS;

  getControllers() {
    return of(this.products);
  }

  getBySlug(slug: string) {
    const product = this.products.find((p) => p.slug === slug);
    return product ? of(product) : throwError(() => new Error('Not found'));
  }
}
```

Swap to `HttpClient` later; keep the same service interface.

---

# Product Detail Section Order

Matches [Product Page Wireframe](04-product-page-wireframe.md):

1. Overview  
2. Trust layers (vendor / user / platform)  
3. Technology breakdown  
4. Trade-offs  
5. Recommendation context  

---

# Material Theming Reminders

- Outlined cards on public pages  
- No “winner” highlight in compare tables  
- Trust states: Verified, Under observation, Limited long-term data, Emerging  
- See [Design System](07-design-system.md)

---

# Angular 17 Notes

- Prefer **standalone** `loadComponent` / `loadChildren` in routes.  
- Prefer **`@if` / `@for`** in new templates.  
- Use **`provideRouter(routes, withComponentInputBinding())`** if route params as `input()` on pages.  
- **SSR:** defer until education/trust SEO is a priority; client-only SPA is fine for MVP.  
- **Tests:** `ng test` with Vitest or Karma per CLI choice at project creation.

---

# When to Update This Doc

Update when we:

- change Angular or Material major version,
- add/remove/rename routes,
- move the app folder location,
- change build order or shared component list,
- connect real APIs (document service contracts here or in `06-system-design`).

---

# Final Principle

> Ship a thin vertical slice (shell → home → product with trust layers) before polishing secondary screens.
