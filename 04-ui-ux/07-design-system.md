# Design System

# Project Trident — Angular Material Design System (V1)

---

# Introduction

Project Trident uses **Angular** and **Angular Material** for the frontend ([ADR-005](../08-decisions/ADR-005-angular-frontend-choice.md)).

Angular Material’s defaults skew toward generic enterprise or app-store patterns. This document defines how Material is **themed and used** so the product stays:

- calm,
- editorial,
- trustworthy,
- and non-marketplace.

Canonical navigation: [Navigation Flow — V1 Global Header](02-navigation-flow.md#v1-global-header-navbar).

---

# Design Intent

| Attribute | Target |
|-----------|--------|
| Tone | Calm, intelligent, technically grounded |
| Density | Comfortable — prefer whitespace over packed grids |
| Motion | Minimal — no attention-grabbing animations |
| Color | Neutral base, one restrained accent |
| Trust | Layers always labeled and visually separated |

**Anti-patterns:** deal banners, “#1 pick” trophies, star-rating-only cards, urgency copy, neon gaming chrome on global shell.

---

# Stack

| Piece | Choice |
|-------|--------|
| Framework | Angular (LTS) |
| UI library | Angular Material + CDK |
| Language | TypeScript |
| Theming | Material 3 custom theme (`@angular/material`) |
| Icons | Material Symbols or consistent SVG set |

---

# Theme Tokens (V1 direction)

Define a custom M3 theme in `src/styles/theme.scss` (exact values refined during implementation).

| Token role | Direction |
|------------|-----------|
| Primary | Muted blue or teal — links, focus, key actions |
| Surface | Off-white / light grey backgrounds |
| On-surface | Dark grey body text — high readability |
| Outline | Subtle borders for cards and trust blocks |
| Error / warn | Used sparingly — uncertainty disclaimers, not sales |

**Elevation:** prefer `outlined` cards; limit raised shadows on public pages.

**Ripple:** reduce or disable on navigational elements where it feels click-baity.

**Typography:** readable sans (e.g. Roboto via Material, or bundled alternative); clear heading scale; 14–16px body.

**Dark mode:** optional post-MVP; light mode first for editorial clarity.

---

# Core Components (Material mapping)

| Trident need | Material component | Notes |
|--------------|-------------------|--------|
| Global navbar | `MatToolbar` + router links | Match V1 nav labels exactly |
| Footer | layout + `MatDivider` | Routes per navigation doc |
| Trust badge | custom `TrustBadgeComponent` wrapping `MatChip` | Muted colors per verification state |
| Trust layer block | `MatCard` (outlined) + header | Vendor / User / Platform labels mandatory |
| Product sections | `MatTabGroup` or stacked `MatCard` | Tabs only when sections are peer-level |
| Comparison matrix | `MatTable` | Explain rows — no winner highlight column |
| Education long-form | layout + `MatExpansion` optional | Doc-style width (~65–75ch) |
| Methodology / trust pages | typography + `MatAccordion` | Documentation feel |
| Search | `MatFormField` + input in toolbar | Utility, not primary nav item |
| Reviewer forms | `MatFormField`, `MatStepper`, `MatTable` | Denser layout acceptable internally |
| Uncertainty callout | `MatCard` or styled alert | “Limited long-term data”, etc. |

Wrap repeated Trident patterns in `shared/` — do not restyle Material ad hoc per screen.

---

# Trust Layer Presentation

Every product and comparison view must separate:

1. **Vendor claims**
2. **User feedback**
3. **Platform verification**

Rules:

- Each layer gets a **visible heading** and distinct container (border/background).
- Never merge into a single composite score without breakdown.
- Verification states use shared badges:

| State | Presentation |
|-------|----------------|
| Verified | Neutral positive chip |
| Under observation | Neutral amber/grey chip |
| Limited long-term data | Muted outline chip |
| Emerging technology | Informational chip |

---

# Buttons & CTAs

| Use | Style |
|-----|--------|
| Primary navigation | `mat-button` or `mat-stroked-button` |
| Secondary / learn more | `mat-stroked-button` |
| Destructive (reviewer only) | `mat-flat-button` color warn |

Avoid `mat-flat-button` color primary for commerce-style “Buy” on public pages. External purchase links, if ever added, are tertiary text links — not hero CTAs.

---

# Layout

- **Max content width** for reading pages: ~960–1100px.
- **Comparison / tables:** may use wider layout with horizontal scroll on small viewports.
- **Grid:** use `MatGridList` sparingly; prefer vertical section flow on homepage per wireframe.
- **Responsive:** mobile nav collapses to menu; Transparency sub-links accessible.

---

# Screen-Specific Notes

| Screen | Guidance |
|--------|----------|
| Home | Hero + trust strip — no product grid above fold |
| Product detail | Section order per product wireframe; trust before recommendation |
| Compare | Table-first; prose trade-off column |
| Reviewer dashboard | Higher density allowed; still use theme tokens |

---

# Accessibility

- Rely on Material’s focus management and ARIA defaults.
- Ensure trust badges are not **color-only** — include text labels.
- Maintain WCAG-friendly contrast on custom theme tokens.

---

# Related Documents

- [ADR-005 — Angular Frontend](../08-decisions/ADR-005-angular-frontend-choice.md)
- [Screen List](01-screen-list.md)
- [Home Wireframe](03-home-wireframe.md)
- [Product Page Wireframe](04-product-page-wireframe.md)
- [Comparison Page Wireframe](05-comparison-page-wireframe.md)

---

# Final Principle

> Angular Material is the implementation layer; calm editorial trust UX is the product layer. Theme and component discipline bridge the two.
