# Navigation Flow

# Project Trident Navigation & User Flow Strategy

---

# Introduction

Navigation within Project Trident is not designed primarily for:
- engagement maximization,
- infinite browsing,
- or impulsive purchasing behavior.

The navigation system is intended to support:
- understanding,
- trust,
- and informed technology decision-making.

This document defines the intended navigation philosophy and user movement structure across the platform.

**Implementation:** Angular + Angular Material ([ADR-005](../08-decisions/ADR-005-angular-frontend-choice.md), [Design System](07-design-system.md)).

---

# Core Navigation Philosophy

Project Trident navigation should help users move through:

1. Understanding
2. Trade-off awareness
3. Technology exploration
4. Product evaluation
5. Decision support

The platform should encourage:
- thoughtful exploration,
not:
- rapid conversion behavior.

Navigation should feel:
- structured,
- calm,
- and transparent.

---

# Primary UX Goal

Users should never feel:
- lost,
- overwhelmed,
- manipulated,
- or pressured.

Navigation should continuously reinforce:
- trust,
- clarity,
- and technology understanding.

---

# High-Level Navigation Structure

The platform navigation is divided into:

1. Technology Discovery
2. Product Discovery
3. Technology Education
4. Trust & Transparency
5. Platform Identity

---

# V1 Global Header (Navbar)

This section defines the **Phase 1 / MVP top navigation bar**. It is the canonical reference for header layout, labels, routes, and what stays out of the navbar.

The navbar should remain **minimal** — five primary areas plus utility chrome, not one link per screen.

---

## Layout

```txt
[Logo → Home]  Explore Technologies | Discover Products | Compare | How We Review | Transparency   [Search]
```

- **Logo** — always returns to Home.
- **Search** — utility control on the right (icon or compact field); not a primary nav section.
- **Transparency** — may use a small dropdown on desktop; on mobile, expand inside the menu.

---

## Primary Nav Items (V1)

| Label | Nav area | Primary screens | Default route (V1) |
|-------|----------|-----------------|-------------------|
| *(Logo)* | Platform identity | Home | `/` |
| **Explore Technologies** | Technology discovery | Technology Detail, Technology Comparison, Decision Framework (linked from flows) | `/technologies` |
| **Discover Products** | Product discovery | Category Discovery, Product Detail | `/products/controllers` |
| **Compare** | Comparison | Technology Comparison, Product Comparison | `/compare` |
| **How We Review** | Trust & transparency | Review Methodology | `/methodology` |
| **Transparency** | Trust & transparency | Trust & Ethics, How Rankings Work | `/transparency` |
| **Search** | Discovery utility | *(results inline or dedicated route later)* | `/search` |

### Transparency dropdown (recommended)

When using a dropdown under **Transparency**:

- Trust & Ethics → `/transparency/ethics`
- How Rankings Work → `/transparency/rankings`

A single **Transparency** landing page at `/transparency` that links to both is also acceptable for V1.

---

## Item Order & Rationale

Nav items appear left-to-right in this order:

1. **Explore Technologies** before **Discover Products** — technology-first discovery.
2. **Compare** — trade-offs across technologies and products.
3. **How We Review** and **Transparency** — trust and methodology remain structurally visible.

---

## Screens Not in the Top Navbar (V1)

These remain reachable via **footer**, **in-page links**, or **parent flows** — not duplicated as top-level nav items:

| Screen | Typical entry |
|--------|----------------|
| Decision Framework | Explore Technologies, homepage education sections |
| About Project Trident | Footer |
| Product Detail | Discover Products, search, comparisons |
| Technology Detail | Explore Technologies, product pages |

---

## Footer Navigation (V1)

The footer complements the navbar. Suggested groups:

| Link | Route | Notes |
|------|-------|-------|
| About Project Trident | `/about` | Mission and vision |
| Methodology | `/methodology` | Same destination as **How We Review** |
| Technology Education | `/technologies` | Same hub as **Explore Technologies** |
| Transparency Policies | `/transparency` | Ethics and rankings hub |
| Contact | `/contact` | Placeholder acceptable in MVP |

Footer may repeat trust links; the navbar must not hide methodology or transparency.

---

## Excluded from Public Navigation (V1)

Not shown in the public header or footer for end users:

- Reviewer Dashboard
- Product Evaluation Workspace
- Internal Product Queue
- Vendor Submission
- Vendor Product Management

Reviewer and vendor surfaces use **separate authenticated routes** (e.g. `/reviewer`) when implemented.

---

## Navbar Anti-Patterns (V1)

The header must **not** include:

- Marketplace patterns (cart, deals, “best sellers”)
- Category sprawl beyond the initial focus (controllers / input)
- Vendor or monetization CTAs
- Engagement bait (infinite feeds, urgency badges in nav)

---

## Search (V1)

MVP includes search and discovery. Search is **header utility**, not a sixth primary nav label.

- Prefer a persistent search control in the header.
- Results may route to `/search` or filter within Category Discovery until a dedicated results screen is defined.

---

# Primary Navigation Areas

The following sections describe user intent and destinations for each navbar area.

---

# 1. Explore Technologies

## Purpose
Technology-first entry point.

## User Intent
Users want to:
- understand technologies,
- explore engineering differences,
- and learn about category evolution.

## Example Destinations
- Hall Effect systems
- Input technologies
- Wireless technologies
- Technology comparison pages

---

# 2. Discover Products

## Purpose
Contextual product exploration.

## User Intent
Users want to:
- explore products,
- compare options,
- and evaluate trade-offs.

Products should appear:
- after educational context exists.

Discovery should remain:
- transparent,
- and technology-aware.

---

# 3. Compare

**Navbar label:** Compare

## Purpose
Structured trade-off understanding across **technologies and products**.

## User Intent
Users want to:
- compare approaches,
- evaluate strengths and weaknesses,
- and understand long-term implications.

Example comparisons:
- Hall Effect vs Mechanical
- Optical vs Traditional switches
- Wireless protocol differences

---

# 4. How We Review

## Purpose
Trust establishment.

## User Intent
Users want to understand:
- how products are evaluated,
- what methodologies exist,
- and why recommendations can be trusted.

This area is critical for long-term platform credibility.

---

# 5. Transparency & Ethics

## Purpose
Trust reinforcement.

## User Intent
Users want to understand:
- recommendation philosophy,
- independence policies,
- ranking logic,
- and ethical principles.

Transparency should remain highly visible.

---

# Homepage Flow Strategy

The homepage should guide users through:

1. Problem awareness
2. Platform philosophy
3. Technology awareness
4. Trust establishment
5. Exploration entry points

The homepage should avoid:
- immediate product pressure,
- marketplace-style product walls,
- and aggressive recommendation exposure.

---

# Technology Discovery Flow

Users entering technology sections should move through:

1. Technology explanation
2. Engineering trade-offs
3. Real-world implications
4. Product examples
5. Contextual recommendations

The flow should emphasize:
- understanding before selection.

---

# Product Discovery Flow

Users entering product sections should experience:

1. Technology context
2. Verification visibility
3. Trade-off explanation
4. Recommendation reasoning
5. Comparison opportunities

Products should never appear disconnected from:
- technology explanation,
- or trust context.

---

# Product Detail Flow

Product detail pages should guide users through:

1. Product overview
2. Trust layer visibility
3. Platform verification
4. Technology explanation
5. Trade-offs
6. Long-term considerations
7. Recommendation context

The page should feel:
- analytical,
not:
- promotional.

---

# Comparison Flow

Comparison systems should prioritize:
- understanding,
- transparency,
- and decision support.

Comparisons should explain:
- why differences matter,
- who benefits from each option,
- and what trade-offs exist.

The objective is:
- informed selection,
not:
- artificial winners.

---

# Trust Navigation Visibility

Trust-related pages should remain accessible from:
- homepage,
- product pages,
- recommendation areas,
- and comparison systems.

Users should never struggle to find:
- methodology,
- ranking explanations,
- or ethical policies.

Trust visibility should remain structural rather than hidden.

---

# Minimal Navigation Philosophy

Project Trident should avoid:
- excessive navigation complexity,
- feature overload,
- and unnecessary category expansion.

The platform should initially feel:
- focused,
- intentional,
- and specialized.

Clarity is more important than feature quantity.

---

# Emotional UX Direction

Navigation should feel:
- calm,
- educational,
- and trustworthy.

The platform should avoid:
- urgency-driven flows,
- addictive browsing loops,
- and engagement traps.

Users should feel:
- guided,
not:
- psychologically optimized.

---

# Information Depth Philosophy

Users should be able to:
- progressively explore deeper information layers.

The navigation system should support:
- shallow exploration for casual users,
and:
- deep technical understanding for advanced users.

The platform should accommodate both without:
- overwhelming either group.

---

# Long-Term Navigation Vision

As Project Trident evolves, navigation may eventually support:
- adaptive discovery systems,
- advanced filtering,
- technology pathways,
- and structured decision frameworks.

However, future complexity should never reduce:
- explainability,
- trust clarity,
- or educational flow.

---

# Anti-Goals

Navigation should avoid becoming:
- marketplace-like,
- advertisement-driven,
- engagement-optimized,
- or psychologically manipulative.

If navigation begins prioritizing:
- clicks,
- browsing time,
- or monetization visibility

over:
- understanding and trust,

the platform risks losing its identity.

---

# Final Principle

> Navigation should help users move toward clarity and understanding rather than toward impulsive purchasing behavior.