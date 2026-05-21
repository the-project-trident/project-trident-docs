# Living Documentation

# How Project Trident Docs Relate to Implementation

---

# Purpose

This folder holds **meta** guidance about the documentation repository itself.

The markdown across `01-vision/` through `08-decisions/` was written to capture product intent, trust philosophy, and early UX planning. It is **context for building**, not an unchangeable contract.

---

# Core Rule

> **Documentation should follow what we are actually building.** When implementation, user feedback, or better technical choices disagree with a doc, update the doc — or supersede it with an ADR.

Agents and contributors should:

- treat docs as the default source of truth **until** a newer ADR or implementation note says otherwise,
- propose doc updates when stack, routes, or scope change,
- avoid letting outdated docs block sensible engineering decisions.

---

# What Should Stay Stable

These change rarely; update only with deliberate product shifts:

- trust principles (three-layer model, no paid rankings),
- technology-first discovery philosophy,
- calm / non-marketplace UX intent,
- credibility-over-growth roadmap mindset.

---

# What Should Change Often

These should track the codebase:

- frontend stack versions (e.g. Angular 17 pin),
- routes and navbar labels,
- screen build order and folder structure,
- mock vs API data assumptions,
- MVP feature inclusion.

---

# Where Implementation Truth Lives

| Topic | Primary doc |
|-------|-------------|
| **Full tech stack & versions** | [Tech Stack](02-tech-stack.md) |
| Frontend decision | [ADR-005](../08-decisions/ADR-005-angular-frontend-choice.md) |
| Routes & navbar | [Navigation Flow](../04-ui-ux/02-navigation-flow.md) |
| Screens | [Screen List](../04-ui-ux/01-screen-list.md) |
| UI patterns | [Design System](../04-ui-ux/07-design-system.md) |
| How to build the app | [Frontend Implementation Plan](../04-ui-ux/08-frontend-implementation-plan.md) |

When in doubt: **code + ADR + implementation plan** win over older narrative docs.

---

# Final Principle

> Docs exist to help us build the right product — not to preserve every early assumption forever.
