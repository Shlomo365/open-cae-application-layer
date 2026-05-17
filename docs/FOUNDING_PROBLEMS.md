# Founding Problems

## Purpose

This document lists the core problems that the **Open CAE Application Layer Initiative** is founded to address.

The project should not begin as a list of features.

It should begin as a set of hard engineering software problems that must be solved correctly for an open CAE application layer to become useful.

---

## Problem 1: Open-Source CAE Is Fragmented

Open-source engineering has many strong tools, but they are often separated by different workflows, formats, assumptions, and data models.

A user may need one tool for CAD, another for meshing, another for MBD, another for FEA, another for CFD, and another for visualization.

The founding problem is:

> How can existing open-source engineering tools be connected through one coherent CAE application workflow?

This requires more than file conversion.

It requires an application model.

---

## Problem 2: The Core Model Must Be Solver-Independent

If the project stores its engineering model as solver-specific objects, it becomes locked to one backend.

That would make the project difficult to extend to other solvers, other domains, and future workflows.

The founding problem is:

> What should belong in the project-owned Core Model, and what should remain solver-specific?

This affects:

- bodies
- materials
- joints
- loads
- contacts
- boundary conditions
- simulation cases
- mesh references
- result references
- units
- transforms

The Core Model must be expressive enough to represent engineering intent, but not so solver-specific that it becomes a hidden wrapper around one backend.

---

## Problem 3: Topology References Are Hard

CAE workflows often depend on selecting faces, edges, vertices, regions, and subobjects.

These references are used for:

- joints
- mates
- contacts
- loads
- boundary conditions
- mesh controls
- named selections
- result scoping

But topology references can break when geometry changes.

The founding problem is:

> How should geometry and topology references be represented, stored, resolved, validated, and diagnosed?

The project must avoid treating transient viewport picks or temporary backend IDs as durable engineering references.

This is one of the most important technical risks.

---

## Problem 4: Solver Adapters Must Not Become the Application

A solver adapter should connect the internal model to a solver backend.

It should not become the project itself.

The founding problem is:

> How can external solvers be integrated without letting one solver define the entire application architecture?

A good adapter should:

- validate supported inputs
- translate project entities to solver-specific data
- execute or prepare solver execution
- collect diagnostics
- return results
- map results back to stable entity IDs

A bad adapter turns the application into a thin GUI around one solver.

---

## Problem 5: Results Need a Unified Model

MBD, FEA, and CFD produce different kinds of results.

MBD often produces time-based body, joint, contact, and motor data.

FEA and CFD often produce field-based data over meshes.

The founding problem is:

> How can the Results Layer support time-series results, field results, solver metadata, units, validity states, and entity links across different simulation domains?

Results should not be stored only as:

- solver output files
- viewport state
- screenshots
- temporary arrays
- backend-specific objects

They should be first-class engineering data.

---

## Problem 6: Visualization Must Not Own Engineering Truth

Visualization is essential, but it must not become the model.

A viewport can display bodies, selections, motion, stress fields, pressure fields, plots, and timelines.

But the viewport should not own engineering state.

The founding problem is:

> How can visualization remain connected to the model and results without becoming the source of truth?

Visual objects must map back to stable project and result references.

---

## Problem 7: Meshes Are Derived Data, Not the Whole Model

FEA and CFD depend on meshes, but meshes should not replace the engineering model.

The founding problem is:

> How should the project connect geometry, mesh groups, boundary conditions, solver inputs, and results without making the mesh the only source of truth?

This is important for:

- remeshing
- mesh convergence
- solver export
- result mapping
- named selections
- boundary regions
- geometry changes

---

## Problem 8: Human Users and AI Agents Need the Same Operation Path

Future engineering software should support both human users and automation.

But automation should not bypass the application logic.

The founding problem is:

> How can GUI users, scripts, tests, and future AI agents operate the same engineering model through the same command/application layer?

This requires:

- explicit commands
- structured inputs
- validation
- structured outputs
- diagnostics
- logs
- reproducible operations
- auditable state changes

The project should not depend on hidden GUI-only behavior.

---

## Problem 9: Project Files Must Be Open and Evolvable

CAE projects contain many types of data:

- model definitions
- geometry references
- meshes
- solver settings
- generated files
- result sets
- logs
- reports
- display state

The founding problem is:

> How should project data be stored so it remains open, readable, portable, versioned, and able to evolve?

The project should avoid opaque runtime dumps as the primary format.

Generated data should be separated from model definition.

---

## Problem 10: Verification Must Be Part of the Project Culture

Simulation software can produce convincing but wrong results.

The founding problem is:

> How can the project make verification, validation, benchmark cases, and diagnostics part of the workflow from the beginning?

This requires:

- simple analytical benchmark cases
- regression tests
- solver comparison cases
- documented limitations
- unit consistency checks
- result validation
- mesh convergence examples where relevant

A colorful plot is not enough.

Engineering usefulness requires evidence.

---

## Problem 11: MVP Scope Must Stay Small

The long-term vision includes CAD, MBD, FEA, CFD, meshing, visualization, results, reporting, automation, and AI-agent workflows.

Trying to build all of this at once would fail.

The founding problem is:

> What is the smallest MVP that proves the architecture without pretending to implement the entire vision?

The proposed answer is an MBD-first vertical slice.

It should prove:

- core model
- command layer
- solver adapter
- simulation case
- time-based results
- replay
- persistence
- diagnostics

---

## Problem 12: The Project Must Collaborate With Existing Communities

The project should not position itself as a replacement for existing open-source tools.

The founding problem is:

> How can the project learn from and integrate with existing communities without appearing as a competitor or shallow wrapper?

The project should be positioned as:

- an application-layer initiative
- an integration workflow
- a place for adapters
- a system that benefits from existing tools
- a project that sends users and contributors toward open-source engineering ecosystems

---

## Problem 13: Domain Breadth Must Not Destroy Architecture Focus

MBD, FEA, CFD, meshing, and visualization all have different requirements.

The founding problem is:

> How can the architecture remain broad enough for future domains while keeping the first implementation small enough to complete?

This requires:

- future-ready data boundaries
- staged implementation
- explicit non-goals
- adapter design
- clear MVP scope
- no premature feature explosion

---

## Problem 14: Engineering Workflows Need Traceability

A CAE workflow is not only a sequence of clicks.

It should be traceable.

The founding problem is:

> How can the project record what was defined, what was run, what solver was used, what results were produced, and whether those results are still valid?

This requires:

- simulation run metadata
- logs
- diagnostics
- result provenance
- validity states
- links to model entities
- project history or command records in the future

---

## Problem 15: The Project Needs Credibility Before Scale

A large open-source CAE project cannot rely on vision alone.

The founding problem is:

> How can the project build credibility before it has a full implementation?

The early answer is:

- clear architecture
- honest scope
- RFC process
- technical criticism
- benchmark thinking
- small MVP
- documented decisions
- transparent limitations

Credibility comes before scale.

---

## Summary

This project is founded on a set of hard problems, not on a feature checklist.

The most important founding problems are:

- fragmentation of open-source CAE tools
- solver-independent model ownership
- durable topology references
- solver adapter boundaries
- unified results management
- visualization without ownership of truth
- mesh and geometry mapping
- human and AI operation through commands
- open project files
- verification culture
- small MVP scope
- collaboration with existing communities

Solving these problems gradually is the path toward a real open CAE application layer.
