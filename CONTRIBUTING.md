# Contributing

## Current Project Stage

The **Open CAE Application Layer Initiative** is currently in an architecture and RFC stage.

The most valuable contribution right now is not code.

The most valuable contribution is technical criticism.

This repository is being used to define:

- project scope
- architecture boundaries
- core model principles
- solver adapter responsibilities
- results infrastructure
- MVP direction
- open technical questions
- risks and non-goals

Implementation should come after the initial architecture has been reviewed and refined.

---

## What Kind of Contributions Are Useful Now?

At this stage, useful contributions include:

- architecture review
- criticism of assumptions
- identification of missing layers
- review of solver adapter boundaries
- review of topology reference strategy
- review of results storage strategy
- review of the proposed MBD-first MVP
- comparison with existing open-source tools
- benchmark case suggestions
- documentation improvements
- clarification of risks and limitations

The project is especially interested in feedback from people familiar with:

- CAD and geometry kernels
- OCCT / FreeCAD concepts
- topology references
- multibody dynamics
- Chrono / MBDyn
- finite element analysis
- Code_Aster / CalculiX
- CFD and OpenFOAM-style workflows
- meshing tools such as Gmsh or Salome
- VTK / ParaView-style visualization
- CAE workflow design
- engineering automation and scripting

---

## What This Project Is Not Asking For Yet

The project is not currently asking contributors to implement the full system.

Please do not start large code contributions before the architecture and license are settled.

The project is not yet looking for:

- large feature implementations
- full solver integrations
- complete UI development
- large refactors
- production-level CAE functionality
- unsupported claims that a workflow is complete
- marketing-only contributions without technical substance

Small documentation improvements and architecture review are welcome.

---

## How to Give Feedback

The best feedback is specific.

Instead of writing:

> This looks good.

or:

> This will not work.

Try to explain:

- which part of the architecture you are commenting on
- what risk you see
- what alternative you suggest
- which existing tool or workflow supports your point
- whether the issue affects the MVP or long-term roadmap

Useful feedback examples:

- “The Core Model boundary is too close to the solver backend because...”
- “Topology references need a stronger durability model because...”
- “The Results Layer should separate time-series data from field data because...”
- “The MBD-first MVP is reasonable, but it should include this validation case...”
- “OpenFOAM will require these concepts later, so the early model should not block them...”

---

## Preferred Feedback Areas

### 1. Application Layer

- Is the separation between GUI, commands, core model, solvers, results, and visualization correct?
- Is any major application-layer responsibility missing?
- Which parts are too abstract or too vague?

### 2. Core Model

- What should belong in the solver-independent model?
- What should remain solver-specific?
- How should bodies, transforms, materials, joints, loads, contacts, and simulation cases be represented at a high level?

### 3. Geometry and Topology References

- How should face, edge, vertex, and region references be stored?
- What should be considered durable?
- What should be considered session-only or transient?
- What diagnostics are needed when references break?

### 4. Solver Adapters

- What should solver adapters be responsible for?
- What should they not be responsible for?
- How should unsupported features be reported?
- How should solver outputs map back to project entities?

### 5. Results Layer

- How should time-based MBD results be stored?
- How should future FEA and CFD field results be represented?
- How should result validity, solver metadata, and units be handled?
- How should results be linked to simulation cases and project entities?

### 6. MVP Scope

- Is an MBD-first vertical slice the right first MVP?
- What is the smallest workflow that proves the architecture?
- What should be explicitly excluded from the MVP?

### 7. Verification and Benchmarks

- Which simple benchmark cases should be used first?
- What analytical cases can verify early MBD behavior?
- What future cases should verify FEA, CFD, and coupled workflows?

---

## Issues vs Discussions

Use **GitHub Discussions** for:

- RFC review
- architecture questions
- broad technical debate
- alternative proposals
- tool comparisons
- long-form feedback

Use **GitHub Issues** for:

- specific documentation fixes
- broken links
- unclear wording
- small scoped tasks
- accepted follow-up actions from a discussion

A broad architecture debate should usually start as a Discussion, not as an Issue.

---

## Suggested Discussion Titles

Examples:

```text
RFC-001: Feedback on Core Model boundaries
RFC-001: Solver adapter responsibilities
RFC-001: Topology reference risks
MVP: What should the first MBD vertical slice prove?
Results Layer: Time-series and field data requirements
CFD readiness: What should OpenFOAM influence early?
```

---

## Suggested Issue Titles

Examples:

```text
Clarify non-goals in README
Add missing link to Architecture Overview
Improve wording in MVP Definition
Add benchmark candidate: simple pendulum
Document topology reference risk
```

---

## Documentation Style

Project documents should be:

- clear
- direct
- technical
- honest about status
- explicit about non-goals
- careful not to claim unimplemented features
- written in English
- easy to review

Avoid:

- hype
- vague marketing language
- unsupported claims
- claiming that future capabilities already exist
- mixing implementation details into high-level architecture documents
- creating too many documents before the structure is clear

Use terms like:

- proposed
- intended
- designed to support
- future
- architecture direction
- under review

Avoid terms like:

- implemented
- supported
- production-ready
- complete

unless the feature really exists and has evidence.

---

## Architecture Decision Process

Important decisions should eventually be captured as Architecture Decision Records.

A decision record should explain:

- the problem
- the options considered
- the decision
- the reason for the decision
- consequences and tradeoffs
- links to related discussions or RFCs

Until a formal decision is made, documents should keep open questions visible.

---

## Code Contributions

Code contributions are not the primary focus at the current stage.

Before larger code contributions begin, the project should settle:

- license
- repository structure
- development environment
- coding conventions
- test strategy
- first MVP implementation plan
- contribution workflow

Small prototype code may be useful later, but it should be clearly marked as experimental unless accepted into the main implementation plan.

---

## Licensing Note

The project license must be selected before accepting meaningful public code contributions.

Until the license is selected, discussion and documentation review are safe, but code contribution should remain limited or experimental.

---

## Conduct

Technical criticism is welcome.

Personal attacks are not.

The project needs direct, serious review, including disagreement and negative feedback. However, feedback should focus on the architecture, assumptions, documents, and technical risks.

A strong critique is useful when it helps the project make better decisions.

---

## Summary

The best contribution right now is not to build a large feature.

The best contribution is to help answer this question:

> What architecture is required for an open-source CAE application layer that can connect CAD, MBD, FEA, CFD, meshing, visualization, results, and future AI-agent workflows without becoming a wrapper around one tool?

That is the current contribution goal.
