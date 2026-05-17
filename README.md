# Open CAE Application Layer Initiative

An architecture-first open-source initiative to define the missing application layer for engineering simulation workflows.

## What this is

Open CAE Application Layer Initiative is an architecture-first open-source effort to define and eventually build a CAE application layer that connects existing open-source engineering tools into one coherent desktop workflow.

The long-term scope includes CAD geometry, assemblies, multibody dynamics, finite element analysis, CFD-ready workflows, meshing, visualization, results, reporting, and future AI-agent operation.

At this stage, the project is focused on architecture, scope, technical decisions, open questions, and MVP definition before implementation begins.

## Why this exists

Open-source engineering already has strong solvers, CAD kernels, meshing tools, visualization systems, and post-processing tools.

What is still missing is a coherent CAE application layer that connects these technologies into a professional engineering workflow.

Examples of existing technologies include:

- OCCT and FreeCAD concepts for CAD geometry and topology workflows
- Chrono and MBDyn for multibody dynamics
- Code_Aster and CalculiX for structural analysis
- OpenFOAM for CFD
- Gmsh and Salome for meshing
- VTK and ParaView-style workflows for visualization and results

This initiative is not about replacing these tools. It is about defining the layer that can connect them cleanly.

## The missing layer

This project focuses on the layer above individual solvers, kernels, and visualization tools.

That missing layer includes:

- a solver-independent core model
- a command and application layer
- geometry and topology references
- assembly and body workflows
- simulation cases
- solver adapters
- meshing workflows
- results storage
- visualization workflows
- validation and diagnostics
- reproducible operations for human users and future AI agents

The goal is to build a CAE application architecture where the internal model remains independent from GUI frameworks, visualization backends, and solver-specific runtime objects.

## What this project is not

This project is not:

- a new solver
- a clone of Ansys, Abaqus, Adams, SolidWorks, Simcenter, or any other commercial CAE product
- a replacement for FreeCAD
- a direct wrapper around a single backend
- a GUI demo
- an attempt to implement MBD, FEA, and CFD all at once
- a project that starts from buttons and visual polish before defining the engineering model

The project is intended to connect, learn from, and interoperate with existing open-source engineering tools rather than compete with them directly.

## Scope

The long-term scope includes:

- CAD and geometry workflows
- assembly modeling
- multibody dynamics
- finite element analysis
- CFD-ready architecture
- meshing workflows
- engineering visualization
- time-based and field-based results
- result comparison and reporting
- automation and future AI-agent operation

The first implementation scope will be much smaller than the long-term vision.

## Architecture direction

The proposed architecture is layered around a solver-independent internal model and a clear application layer.

```text
GUI Layer
Application / Command Layer
Core Model
Geometry / Topology Layer
Meshing Layer
Solver Adapter Layer
Results Layer
Visualization Layer
Storage Layer
Automation / Agent Layer
```

The internal model should be the source of truth.

It should not depend directly on:

- GUI widgets
- viewport actors
- solver runtime objects
- solver input files
- visualization backend objects
- external tool-specific document models

External tools should be connected through well-defined adapters or integration layers.

## Core principles

The project is based on the following principles:

1. **The internal model is the source of truth.**  
   GUI state, viewport state, solver runtime objects, and result files must not become the authoritative engineering model.

2. **Solvers are backends, not the application.**  
   Chrono, MBDyn, Code_Aster, CalculiX, OpenFOAM, and other tools should be integrated through adapters rather than shaping the entire application model directly.

3. **The application layer owns workflows.**  
   Engineering operations should go through commands, validation, logging, and controlled state changes.

4. **Results are engineering data, not just plots.**  
   Simulation results should be stored, linked to model entities, versioned, queried, compared, visualized, and exported.

5. **Human users and future AI agents should use the same command layer.**  
   AI operation should be reproducible, auditable, validated, and based on the same application commands used by the GUI.

## First MVP direction

The proposed first MVP is an MBD-first vertical slice.

The goal of the first MVP is not to implement the entire long-term vision. The goal is to prove that the architecture works end-to-end.

The first MVP should demonstrate:

- a desktop application shell
- a project file
- a solver-independent internal model
- simple geometry or imported STEP geometry
- bodies represented in the core model
- an assembly or model tree
- basic joints or constraints
- a simple motion input or motor
- an MBD solver adapter
- a simulation case
- simulation execution
- time-based results
- timeline playback
- basic animation or motion replay
- logging and diagnostics
- save/load behavior
- a clean path toward future FEA, CFD, meshing, and multiphysics workflows

The MVP should be small, but it should be real.

## Why MBD-first

An MBD-first MVP is proposed because it tests important parts of the architecture early:

- bodies
- transforms
- coordinate frames
- joints and constraints
- solver adapters
- time-based results
- timeline playback
- animation
- validation
- result storage

It also creates a visible workflow that can later connect naturally to FEA through reaction forces, motion loads, stress-over-time workflows, flexible bodies, and coupled simulations.

## CFD and OpenFOAM

CFD is part of the long-term architecture, but not part of the first MVP.

The project should be designed so that OpenFOAM or other CFD backends can be integrated later through a CFD adapter layer.

This means the architecture should not block future support for:

- CFD domains
- boundary conditions
- mesh zones
- fluid properties
- turbulence models
- transient field results
- thermal-fluid workflows
- fluid-structure interaction
- multiphysics coupling

CFD-readiness is a design requirement. Full CFD implementation is not an early milestone.

## AI-agent operation

AI-agent operation is a long-term design requirement, not a marketing gimmick.

The project should be designed so that future AI agents can operate the software through the same application and command layer used by human users.

That means AI-driven workflows should be:

- command-based
- validated
- logged
- reproducible
- inspectable
- reversible where possible
- tied to project state and engineering results

The goal is not for an AI agent to click randomly through a GUI. The goal is to expose reliable engineering operations through a controlled application layer.

## Current status

Current status: architecture and RFC stage.

This repository currently focuses on:

- project positioning
- scope definition
- architecture direction
- open technical questions
- MVP definition
- technical review
- early contributor alignment

Implementation is intentionally not the first step. The first step is to define the architecture clearly enough that it can be reviewed, criticized, reduced, and then implemented in a focused way.

## How to give feedback

At this stage, the most valuable contribution is technical criticism.

Useful feedback includes:

- Which part of the architecture is most likely to fail?
- Are the core model boundaries correct?
- How should topology references be represented?
- What should the first MVP prove?
- Which solver adapter responsibilities are missing?
- How should results be stored across MBD, FEA, and CFD workflows?
- Which existing open-source projects already solve part of this problem?
- What should be explicitly excluded from the first MVP?
- What mistakes should this project avoid?

The goal is not to ask people for commitment before the project is ready. The goal is to invite serious technical review before implementation decisions become expensive.

## Planned documents

The initial documentation set is expected to include:

- `VISION.md`
- `ROADMAP.md`
- `docs/RFC-001-Open-CAE-Application-Layer.md`
- `docs/ARCHITECTURE_OVERVIEW.md`
- `docs/MVP_DEFINITION.md`
- `docs/OPEN_SOURCE_CAE_GAP_MAP.md`
- `docs/FOUNDING_PROBLEMS.md`
- `docs/BENCHMARK_CHALLENGE.md`
- `docs/AI_AGENT_OPERATION_MODEL.md`

These documents should stay short, focused, and reviewable. Deep technical detail should be added gradually as decisions are made.

## Documents

- [Vision](VISION.md)
- [Roadmap](ROADMAP.md)
- [RFC-001: Open CAE Application Layer](docs/rfcs/RFC-001-open-cae-application-layer.md)
- [Architecture Overview](docs/ARCHITECTURE_OVERVIEW.md)
- [MVP Definition](docs/MVP_DEFINITION.md)
- [Open-Source CAE Gap Map](docs/OPEN_SOURCE_CAE_GAP_MAP.md)
- [Founding Problems](docs/FOUNDING_PROBLEMS.md)
- 
## License

This project is licensed under the Apache License 2.0.
