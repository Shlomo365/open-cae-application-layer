# Architecture Overview

## Purpose

This document describes the proposed target architecture for the **Open CAE Application Layer Initiative**.

The goal is to define a modular, solver-independent CAE application architecture that can connect existing open-source engineering technologies into one coherent desktop workflow.

This is not a description of a fully implemented system. It is the intended architecture direction for discussion, review, and future implementation.

The architecture is designed to support:

- CAD and geometry workflows
- Assembly modeling
- Multibody dynamics
- Finite element analysis
- CFD-ready workflows
- Meshing
- Engineering visualization
- Results and reporting
- Automation and future AI-agent operation

The central idea is simple:

> Open-source engineering already has strong tools. This project focuses on the missing CAE application layer that can connect them into one coherent workflow.

---

## Core Architecture Principle

The most important architecture rule is:

> The Core Model is the source of truth.

The source of truth must not be:

- the GUI
- a viewport actor
- a solver runtime object
- a mesh file
- a solver input file
- a solver output file
- a temporary visualization object
- a backend-specific data structure

Instead, the project should maintain its own solver-independent internal model. External tools should be connected through clearly defined layers and adapters.

This prevents the project from becoming a direct wrapper around one backend.

---

## High-Level Architecture Diagram

```text
Human GUI / AI Agent / Scripts
        |
        v
Application + Command Layer
        |
        v
Core Model
        |
        +--> Geometry / Topology Layer
        |
        +--> Meshing Layer
        |
        +--> Solver Adapter Layer
        |       +--> MBD Adapter: Chrono / MBDyn
        |       +--> FEA Adapter: Code_Aster / CalculiX
        |       +--> CFD Adapter: OpenFOAM
        |       +--> Future Coupling: FSI / thermal / multiphysics
        |
        +--> Results Layer
        |
        +--> Visualization Layer
        |
        +--> Storage Layer
```

The architecture should make it possible to add or replace backends without rewriting the application model, user workflow, project file structure, or result management system.

---

## Layer Responsibilities

### 1. GUI Layer

The GUI Layer is responsible for user interaction and presentation.

It may include:

- main window
- menus
- command toolbar
- model tree
- property panels
- viewport
- timeline
- result panels
- logs
- dialogs

The GUI must not contain engineering logic.

The GUI should send user actions to the Application / Command Layer. It should display project state, validation results, selections, progress, and results, but it should not become the authority for model state.

---

### 2. Application + Command Layer

The Application + Command Layer coordinates engineering workflows.

It is responsible for:

- command execution
- validation
- project operations
- selection management
- workflow state
- simulation case management
- solver execution requests
- result registration
- logging
- diagnostics
- error handling
- future undo/redo support
- future automation and scripting support

All significant operations should be represented as commands or application services.

Examples:

- import geometry
- create body
- delete body
- assign material
- define joint
- define load
- create simulation case
- run simulation
- load result set
- export result data

A button in the GUI should not directly modify the model or call a solver. It should invoke a command or application service.

---

### 3. Core Model

The Core Model is the project-owned representation of the engineering model.

It should remain independent from:

- Qt or any other GUI framework
- VTK or any visualization backend
- Chrono, MBDyn, Code_Aster, CalculiX, OpenFOAM or any solver backend
- FreeCAD runtime objects
- OCCT runtime objects where avoidable at the application-model level

The Core Model may include entities such as:

- Project
- MechanicalModel
- AssemblyNode
- PartDefinition
- PartInstance
- GeometryReference
- Body
- Material
- Joint
- Constraint
- Motor
- Load
- Contact
- BoundaryCondition
- SimulationCase
- SolverSettings
- ResultReference
- Units
- Transform
- CoordinateSystem

The Core Model should store stable IDs and references so that other layers can map their runtime objects back to project entities.

---

### 4. Geometry / Topology Layer

The Geometry / Topology Layer manages geometry and geometric references.

It may interact with tools such as:

- OCCT
- FreeCAD concepts
- STEP files
- B-Rep geometry
- topology reference mechanisms

Responsibilities include:

- imported geometry references
- body-to-geometry relationships
- faces, edges, vertices and subobject references
- reference geometry
- coordinate systems
- topology reference resolution
- geometry validity checks
- geometry-to-selection mapping
- geometry-to-mesh mapping support

Topology references are a major architecture risk. The system must avoid pretending that raw viewport picks or transient backend IDs are durable engineering references.

---

### 5. Meshing Layer

The Meshing Layer is responsible for preparing geometry for FEA, CFD, and future multiphysics workflows.

It may integrate with tools such as:

- Gmsh
- Salome
- SMESH or similar tools

Responsibilities include:

- mesh definitions
- mesh controls
- mesh groups
- named selections
- boundary regions
- mesh quality data
- geometry-to-mesh mapping
- mesh-to-result mapping
- solver-specific mesh export

The Meshing Layer should not become the Core Model. Meshes are generated or derived data linked back to stable project entities.

---

### 6. Solver Adapter Layer

The Solver Adapter Layer connects external solvers to the internal model.

The project should not become a wrapper around one solver. Each solver should be isolated behind an adapter boundary.

Possible adapter families:

- MBD Adapter: Chrono / MBDyn
- FEA Adapter: Code_Aster / CalculiX
- CFD Adapter: OpenFOAM
- Future Coupling Adapter: FSI / thermal-structural / multiphysics workflows

A solver adapter is responsible for:

- checking whether a simulation case is supported
- translating Core Model entities into solver-specific runtime/input data
- executing or preparing solver execution
- collecting solver diagnostics
- returning results to the Results Layer
- mapping solver results back to stable project entity IDs

A solver adapter must not redefine the project data model.

---

### 7. Results Layer

The Results Layer stores, loads, indexes, queries, and exports simulation results.

Results are not solver objects and not visualization widgets.

A ResultSet should be linked to:

- project ID
- simulation case ID
- run ID
- solver backend
- solver version or metadata
- units
- time information where relevant
- model entity IDs
- result fields
- logs
- status
- storage path
- validity state

The Results Layer should support both:

- time-based results, such as MBD body transforms, velocities, accelerations, joint reactions, contacts, and motor data
- field-based results, such as displacement, stress, strain, temperature, pressure, velocity fields, and CFD variables

The Results Layer should be designed so that future HDF5/XDMF and ParaView-compatible workflows are possible.

---

### 8. Visualization Layer

The Visualization Layer displays geometry, selections, animations, fields, plots, and result states.

It may use VTK or other visualization technologies.

Responsibilities include:

- 3D viewport rendering
- selection highlighting
- reference visualization
- motion replay
- deformation display
- stress plots
- pressure or velocity fields
- legends and color maps
- result animation
- timeline visualization
- plot display
- image or animation export

The Visualization Layer must not be the source of truth. It should map visual objects back to stable Core Model or Results Layer references.

---

### 9. Storage Layer

The Storage Layer manages project files, generated data, and external assets.

It is responsible for:

- project file format
- metadata
- geometry file references
- mesh files
- solver input files
- solver output files
- result files
- logs
- reports
- exported data
- versioning
- relative paths
- validation of missing or stale assets

The project format should be open, readable, portable, and friendly to Git workflows where possible.

Generated or heavy data should be stored separately from the main project definition.

---

### 10. Automation / AI Agent Layer

The system should be designed so that future AI agents, scripts, and automated tools can operate the application through the same command and application layer used by the GUI.

The AI or automation layer should not bypass validation or directly mutate project files.

Required principles:

- reproducible operations
- explicit commands
- structured inputs
- structured results
- validation diagnostics
- logs
- auditable state changes
- clear error reporting
- no hidden GUI-only behavior

The goal is not to make an AI click randomly through the interface. The goal is to expose engineering operations through a controlled command/application layer.

---

## Data Flow

A typical simulation workflow should follow this pattern:

```text
User / Agent action
        |
        v
Command
        |
        v
Application validation
        |
        v
Core Model update or SimulationCase request
        |
        v
Solver Adapter translation
        |
        v
Solver execution
        |
        v
Results Layer registration
        |
        v
Visualization / plots / reports
```

This flow keeps engineering state, runtime solver state, result data, and visual presentation separated.

---

## Solver Adapter Boundary

A solver adapter should translate between the project model and a specific backend.

It should not:

- own the project model
- define the GUI workflow
- store persistent project state directly
- become the only representation of bodies, joints, loads, meshes, or results
- expose backend-specific objects as long-term application entities

It should:

- report supported and unsupported features
- validate required inputs
- produce clear diagnostics
- map internal entity IDs to solver objects
- map solver outputs back to internal entity IDs
- preserve reproducibility where possible

The first proposed implementation direction is an MBD-first vertical slice using an MBD adapter, while keeping the architecture open for FEA, CFD, and future multiphysics adapters.

---

## Results Boundary

Results should be treated as first-class engineering data.

The system should avoid:

- using viewport state as result storage
- storing results only as solver output files without project-level indexing
- mixing initial model state with result state
- making animation modify the original model
- losing the connection between results and model entities

Instead, the Results Layer should provide a consistent way to query and display results from different solvers and simulation domains.

---

## Human GUI and AI Agent Operation

Human users and future AI agents should use the same underlying operation path.

```text
GUI button
        |
        v
Command
        |
        v
Application Layer
        |
        v
Core Model / Solver / Results
```

```text
AI Agent / Script
        |
        v
Command
        |
        v
Application Layer
        |
        v
Core Model / Solver / Results
```

This ensures that GUI workflows, automated workflows, tests, scripts, and future agent workflows remain consistent.

If an operation is only possible through manual GUI state and not through the command/application layer, it is not properly integrated.

---

## First MVP Architecture Scope

The first MVP should be small but architectural.

The proposed first MVP is an **MBD-first vertical slice**.

It should prove:

- a project can be created and saved
- simple geometry or body definitions can exist in the Core Model
- bodies can be represented independently from the solver
- basic joints or constraints can be defined
- a simple MBD simulation can run through a solver adapter
- time-based results can be stored
- motion can be replayed through the Visualization Layer
- the workflow can be driven by commands
- the design does not block future FEA, CFD, meshing, field results, and coupled workflows

The MVP should not attempt to implement the full long-term vision.

It should prove that the layers connect correctly.

---

## Architecture Rules

The following rules should guide implementation decisions:

1. The Core Model is the source of truth.
2. The GUI must not contain engineering logic.
3. Solver backends must be isolated behind adapters.
4. Visualization must not own model state.
5. Results must be stored as engineering data, not as screen state.
6. Commands should represent significant operations.
7. Project files should be open, readable, and versioned.
8. Generated data should be separated from model definition.
9. Human users and future AI agents should use the same command/application path.
10. The architecture should support gradual implementation without blocking long-term MBD, FEA, CFD, meshing, visualization, and results workflows.

---

## What Must Not Happen

The project should avoid these failure modes:

- becoming a GUI wrapper around one solver
- turning solver runtime objects into persistent project objects
- placing engineering logic inside GUI callbacks
- using viewport picks as durable topology references without validation
- treating result visualization as result storage
- mixing model state and result playback state
- creating a project file format that cannot evolve
- implementing advanced features before the application model is stable
- claiming support for MBD, FEA, or CFD before there is a verified workflow
- adding AI-agent operation as a buzzword without command-level reproducibility

---

## Open Architecture Questions

This architecture is intentionally open for review.

Important questions include:

1. What is the correct boundary between the Core Model and Geometry / Topology Layer?
2. How should durable topology references be represented?
3. What should be solver-independent, and what should remain solver-specific?
4. What is the minimal Results Layer that can support both MBD time data and future FEA/CFD field data?
5. What should the first MBD MVP prove?
6. Which FEA backend should be targeted first after the MBD MVP?
7. How should OpenFOAM-style CFD cases influence the early data model without overloading the MVP?
8. What project file format should be used initially?
9. What validation and benchmark cases are needed before claiming engineering usefulness?
10. What is the safest way to expose operations to future AI agents?

---

## Summary

This architecture proposes a modular CAE application layer built around a solver-independent Core Model, a command-driven Application Layer, clear solver adapters, independent results management, and visualization that displays state without owning it.

The goal is not to replace existing open-source tools.

The goal is to connect them through a coherent engineering workflow.
