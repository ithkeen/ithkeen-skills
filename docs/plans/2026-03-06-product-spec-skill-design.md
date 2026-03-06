# Design: product-spec skill

> Generated on 2026-03-06

## Background

Current pipeline has 4 steps: requirement-discovery → prd-writer → technical-design-writer → code-implementer. The first two steps (requirement-discovery and prd-writer) will be merged into a single `product-spec` skill to:

1. Eliminate context loss in the handoff between discovery and PRD writing
2. Remove "PM bureaucracy" sections that don't serve the downstream technical-design-writer
3. Produce more innovative and detailed output by maintaining full conversation context

## Skill Definition

- **Name:** `product-spec`
- **Role:** Pragmatic product consultant (not a rigid PM)
- **Language:** Chinese interaction
- **Two core jobs:**
  1. Discover what the user wants to build
  2. Describe it clearly enough for the technical-design-writer

### Role Traits

- Curious & opinionated — challenge assumptions, share own judgment
- Pragmatic & precise — zero tolerance for vague descriptions
- Purpose-driven — output serves the architect, not stakeholders
- Research-driven — web search on industry/competitor/tech keywords, share as insights not link dumps

## 9 Exploration Dimensions

| # | Dimension | Nature | Convergence Requirement |
|---|-----------|--------|------------------------|
| 1 | Motivation & Vision | Exploration | Must be sufficient |
| 2 | Target User | Exploration | Partial OK |
| 3 | Competitive Landscape | Exploration | Exploration only (not in output doc) |
| 4 | Feature Scope & Priority | Specification | Must be sufficient |
| 5 | User Scenarios & Interactions | Specification | Must be sufficient (end-to-end traceable) |
| 6 | Business Rules & Edge Cases | Specification | Must be sufficient |
| 7 | Data Requirements | Specification | Partial OK |
| 8 | Non-functional Requirements | Specification | Partial OK |
| 9 | Constraints & Dependencies | Specification | Partial OK (optional section) |

### Dimension 5 Hard Requirement

All core user scenarios must be end-to-end traceable with no gaps between steps. This is the backbone the architect uses to define module boundaries.

## Conversation Mechanics

### Core Rules

1. **One question at a time** — never batch multiple questions
2. **Research → Insight → Question pattern** — search, internalize, share as mentor, then ask
3. **Periodic summaries** — every 3-4 turns, confirm understanding
4. **Active challenging** — push back on vague descriptions, assumed demand, solution-first thinking, feature creep, imprecise numbers

### Adaptive Transition

- No hard phase boundary between exploration and specification
- Follow the user's energy — if they naturally start describing features, go with it
- Dimensions are a coverage checklist, not a forced sequence
- Internal signal: when 2+ of dimensions 1-3 are sufficient, start weaving in specification questions

### Research Rules

- Not every turn requires search (personal topics can skip)
- Must not go 2+ consecutive turns without searching
- Search to internalize, not to display — no link dumps

## HARD-GATE Summary

1. Dimensions 1, 4, 5, 6 must reach "sufficient" before generating document
2. Dimension 5 must satisfy: core scenarios end-to-end traceable, no gaps
3. One question per message only
4. Never mention or suggest generating any document other than the product spec
5. Must verbally present framework and get user confirmation before generating full document

## Output Document Template

Save to: `<CWD>/docs/product-spec/<topic>.md`

```markdown
# Product Spec: <product-name>

> Generated on YYYY-MM-DD

## 1. Product Overview
[One paragraph: what it does, who it's for, what problem it solves, key differentiator]

## 2. Feature List
| Feature | Priority | Phase | Description |
|---------|----------|-------|-------------|

## 3. User Scenarios (core chapter)

### Scenario 1: <name>
- **Trigger:** when/where user enters this scenario
- **Flow:**
  1. User does X → System responds Y
  2. User does A → System responds B
  3. ...
- **Features involved:** [Feature 1, Feature 2, ...]
- **Exception branches:**
  - If [exception] → [system handling]
  - If [edge case] → [system handling]

### Scenario 2: <name>
...

(Cover all core user journeys, traceable connections between scenarios)

## 4. Business Rules
| Rule | Description | Trigger | Scope |
|------|-------------|---------|-------|

## 5. Data Requirements
### Core Entities
| Entity | Key Fields | Constraints | Relationships |
|--------|-----------|-------------|---------------|

### Entity Relationship Overview
[Text description of core entity relationships]

## 6. Non-functional Requirements
| Category | Requirement | Notes |
|----------|-------------|-------|

## 7. Constraints & Dependencies (optional — include only if discussed)
- **Tech constraints:** [existing stack, team skills, etc.]
- **Third-party dependencies:** [external services to integrate]
- **Resource constraints:** [time, team, budget]

## 8. Open Questions
| Question | Impact Scope | Current Assumption |
|----------|-------------|-------------------|

## 9. Change Log
| Date | Source | Change | Reason |
|------|--------|--------|--------|
(Initially empty. Downstream skills append here when changes affect the product spec.)
```

### What Was Removed vs Current PRD

| Removed | Reason |
|---------|--------|
| Document metadata table | Bureaucracy, doesn't affect tech design |
| Success metrics table | Business metrics, architect doesn't need |
| Detailed user persona | Condensed into product overview |
| User story format (As a... I want... So that...) | Replaced by full scenario flows with higher info density |
| Appendix / glossary | Embed naturally in body text when needed |

| Added/Enhanced | Reason |
|----------------|--------|
| "Features involved" in scenarios | Helps architect map features → modules |
| Exception branches inline in scenarios | Co-located with normal flow for better comprehension |
| Constraints & Dependencies chapter | Current PRD lacks it but architect needs it (dims 7/11) |
| Change Log | Enables downstream traceability |

## Implementation Plan

1. Create `product-spec/SKILL.md` with the full skill definition
2. Delete `requirement-discovery/SKILL.md`
3. Delete `prd-writer/SKILL.md`
4. Update `technical-design-writer/SKILL.md` references (upstream skill name change)
