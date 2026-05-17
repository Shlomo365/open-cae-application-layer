# RFC-001: Open CAE Application Layer

## Status

Draft

## Summary

This RFC proposes an architecture-first open-source initiative to define and eventually build a CAE application layer for engineering simulation workflows.

The goal is not to create a new solver, clone commercial CAE software, or replace existing open-source tools. The goal is to define the missing desktop workflow layer that can connect existing open-source engineering technologies into one coherent system.

The long-term scope includes CAD/geometry, assemblies, multibody dynamics (MBD), finite element analysis (FEA), computational fluid dynamics (CFD), meshing, visualization, results, reporting, and future AI-agent operation.

At this stage, this RFC is asking for technical criticism before implementation.

---

## Motivation

Open-source engineering already has strong tools in many areas:

- CAD and geometry kernels
- multibody dynamics solvers
- finite element analysis solvers
- CFD solvers
- meshing tools
- visualization and post-processing systems

However, these tools often exist as separate systems with different workflows, data models, file formats, assumptions, and user interfaces.

The missing piece is a coherent CAE application layer that can connect these tools into a professional engineering workflow.

This project starts from the application-layer problem rather than from writing a new solver.

---

## Problem Statement

A complete CAE workflow usually requires more than a solver.

A useful engineering simulation application needs to manage:

- projects
- geometry and imported CAD references
- assemblies
- bodies and part instances
- materials
- topology references such as faces, edges, and vertices
- joints and constraints
- contacts
- loads and boundary conditions
- mesh definitions and mesh regions
- simulation cases
- solver settings
- simulation execution
- results
- plots and visualization
- reports
- validation and diagnostics
- file storage
- reproducible operations

Many open-source tools solve parts of this problem, but there is still a gap at the level of application workflow and system integration.

The central question of this RFC is:

> What should an open-source CAE application layer look like if it is designed from the beginning to connect existing tools instead of replacing them?

---

## Proposed Direction

The project should be designed as a layered CAE application, not as a direct wrapper around one solver or one GUI framework.

The proposed direction is:

1. Define a solver-independent core model.
2. Place a command/application layer above the core model.
3. Keep GUI, visualization, solver runtime objects, and storage formats separate from the core model.
4. Connect external solvers through adapters.
5. Store results as application-level engineering data, not as solver-specific objects or viewport-only state.
6. Design workflows so they can be operated by both human users and future AI agents through the same command/application layer.
7. Start with a small MBD-first vertical slice that proves the architecture end-to-end.

---

## Architecture Principles

### 1. The Core Model Is the Source of Truth

The internal project model should be the source of truth.

It should not be replaced by:

- GUI widgets
- solver runtime objects
- VTK actors or viewport state
- CAD-kernel-specific runtime objects
- solver input files
- exported result files

The GUI displays the model.  
Solver adapters translate the model.  
The results layer stores outputs from simulations.  
The visualization layer renders geometry and results.

### 2. External Tools Are Integrated Through Layers and Adapters

External tools should not take over the application model.

Examples of possible long-term integrations:

- CAD/geometry: OCCT and FreeCAD concepts
- MBD: Chrono and possibly MBDyn
- FEA: Code_Aster and/or CalculiX
- CFD: OpenFOAM
- Meshing: Gmsh and/or Salome
- Visualization: VTK and ParaView-compatible export
- Results storage: future HDF5/XDMF-compatible workflows

These tools should be connected through explicit layers or adapters.

### 3. The Application Layer Owns Engineering Workflow

The application layer should manage:

- commands
- validation
- selection
- workflow state
- transactions
- project operations
- simulation execution
- result management
- diagnostics
- logging
- future undo/redo and scripting support

The GUI should not contain engineering logic directly.

### 4. Commands Are First-Class Operations

Every significant engineering operation should be represented as a command or application service.

Examples:

- import geometry
- create body
- assign material
- create joint
- define load
- define simulation case
- run simulation
- export results
- generate report

This is important for GUI usage, testing, scripting, automation, and future AI-agent operation.

### 5. Results Are Application-Level Engineering Data

Results should not be treated as temporary solver objects or viewport-only state.

A result set should include:

- simulation case reference
- run ID
- solver metadata
- status
- units
- time steps where relevant
- entity references
- result fields
- logs
- diagnostics
- storage paths
- validity/staleness state

The results layer should support MBD time histories, FEA field results, CFD field results, plots, animation, comparison between runs, and future reporting.

### 6. AI-Agent Operation Should Be Auditable

Future AI agents should operate the application through the same command/application layer used by human GUI workflows.

They should not bypass validation, directly mutate project files, or rely only on screen pixels.

Agent-driven operations should be:

- command-based
- reproducible
- logged
- validated
- inspectable
- reversible where possible
- auditable by a human user

AI-agent support is a design requirement, not the primary marketing claim of the project.

---

## Proposed Layer Structure

The proposed long-term architecture includes the following layers:

```text
GUI Layer
Application / Command Layer
Core Model Layer
Geometry / Topology Layer
Meshing Layer
Solver Adapter Layer
Simulation Execution Layer
Results Layer
Visualization Layer
Storage / IO Layer
Automation / AI-Agent Operation Layer
```

The exact boundaries between these layers are open for review.

---

## Long-Term Scope

The long-term vision includes:

- CAD and geometry workflows
- assembly modeling
- reference geometry
- stable topology references
- MBD workflows
- FEA workflows
- CFD-ready architecture
- meshing workflows
- materials
- contacts
- loads and boundary conditions
- simulation cases
- solver adapters
- result storage
- engineering visualization
- timeline and animation
- plots
- reports
- scripting and automation
- future AI-agent operation

The first implementation scope should be much smaller than the long-term vision.

---

## Non-Goals

This project is not:

- a new solver
- a clone of Ansys, Abaqus, Adams, SolidWorks, Simcenter, or similar commercial tools
- a replacement for FreeCAD
- a direct wrapper around Chrono, Code_Aster, OpenFOAM, or any single backend
- a GUI demo
- an attempt to implement MBD, FEA, and CFD all at once
- an attempt to solve every CAE workflow in the first version
- a project where the GUI becomes the source of engineering truth

The project should connect, learn from, and interoperate with existing open-source tools where appropriate.

---

## First MVP Direction

The proposed first MVP is an MBD-first vertical slice.

The purpose of the MVP is not to implement the full long-term vision.  
The purpose is to prove that the application layers can work together correctly.

A minimal first MVP should aim to demonstrate:

- a desktop application shell
- a project file
- a solver-independent internal model
- simple geometry or imported geometry references
- bodies
- a basic assembly/model tree
- basic joints or constraints
- a simple MBD simulation case
- execution through an MBD solver adapter
- time-based results
- timeline playback
- simple animation/replay
- logs and diagnostics
- save/load
- a clean architectural path toward future FEA, CFD, meshing, and coupled workflows

MBD is proposed first because it tests bodies, transforms, frames, constraints, solver adapters, time-based results, and animation in one compact workflow.

FEA and CFD should remain part of the long-term architecture, but they do not need to be part of the first MVP.

---

## Why Include CFD in the Long-Term Vision?

CFD should be included in the long-term architecture because open-source CFD tools such as OpenFOAM already exist and have significant communities.

However, CFD should not be included in the first MVP.

The architecture should remain prepared for future CFD workflows involving:

- domains
- regions
- boundary conditions
- mesh zones
- fluid properties
- turbulence models
- transient field results
- coupling with thermal and structural workflows
- future fluid-structure interaction workflows

This keeps the project positioned as a general CAE application-layer initiative rather than an MBD-only or FEA-only tool.

---

## Open Questions

This RFC is intentionally open for criticism.

Important questions include:

1. Is the application-layer direction valid?
2. Are the proposed layer boundaries correct?
3. Should the first MVP be MBD-first, or should another vertical slice come first?
4. What is the minimum MVP that proves the architecture without becoming too large?
5. How should topology references be represented so they are useful for CAD, meshing, FEA, contacts, and results?
6. How should the core model avoid becoming locked to one solver backend?
7. What responsibilities belong in solver adapters versus the application layer?
8. How should results be stored so that MBD time data, FEA field data, and CFD field data can share a coherent model?
9. Which existing open-source projects already solve parts of this problem well?
10. What are the highest-risk assumptions in this architecture?
11. What should be excluded from the first implementation even if it is important long-term?
12. What would make this initiative useful to existing open-source engineering communities rather than competitive with them?

---

## Requested Feedback

At this stage, the most valuable contribution is technical criticism.

Useful feedback includes:

- identifying architectural risks
- pointing out missing layers or responsibilities
- warning about known failure modes in CAD/CAE workflows
- reviewing the proposed core model boundaries
- reviewing the solver adapter concept
- reviewing the results model direction
- suggesting better MVP definitions
- mapping existing open-source tools to specific parts of the proposed architecture
- identifying terminology that may be misleading
- identifying parts of the scope that are too large or too vague

This RFC is not asking for implementation commitment.

---

## Decision

Pending.

This RFC will remain in Draft status while the initial architecture, scope, MVP definition, and open questions are reviewed.

A future revision may mark the RFC as Accepted, Revised, Superseded, or Rejected.
