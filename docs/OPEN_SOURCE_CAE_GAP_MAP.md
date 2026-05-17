# Open-Source CAE Gap Map

## Purpose

This document maps the gap that the **Open CAE Application Layer Initiative** is trying to address.

The project is not based on the claim that open-source engineering tools do not exist.

They do exist.

The problem is that many strong tools exist as separate systems, while the missing part is a coherent CAE application layer that connects them into one professional workflow.

---

## Core Claim

Open-source CAE has many strong components, but lacks a unified application-layer workflow that connects them across geometry, assemblies, MBD, FEA, CFD, meshing, visualization, results, reporting, and automation.

This project focuses on that missing layer.

---

## High-Level Gap

| Area | Existing Open-Source Strength | Remaining Gap |
|---|---|---|
| CAD / Geometry | OCCT, FreeCAD concepts, STEP workflows | CAE-oriented application model, stable references, simulation workflow integration |
| MBD | Chrono, MBDyn | Desktop workflow, assembly integration, result management, user-facing simulation cases |
| FEA | Code_Aster, CalculiX, others | Unified model setup, references, meshing integration, results integration |
| CFD | OpenFOAM | Application-level case setup, CAD/mesh/BC integration, result workflow |
| Meshing | Gmsh, Salome, SMESH-style tools | Consistent mesh controls, groups, boundary mapping, solver integration |
| Visualization | VTK, ParaView-style workflows | Integrated viewport, result review, timeline, plots, entity-linked results |
| Results | Solver-specific outputs, ParaView-compatible formats | Unified result model across MBD/FEA/CFD |
| Automation | Scripts and APIs in separate tools | Shared command/application layer for GUI, scripts, tests and AI agents |

---

## CAD / Geometry Gap

### Existing Strengths

Open-source CAD and geometry tools provide important capabilities:

- geometry kernels
- STEP import/export
- B-Rep geometry
- document/object models
- workbench concepts
- shape operations
- visualization and selection foundations

### Remaining Gap

CAE workflows require more than geometry display.

They require:

- stable body references
- subobject references
- face, edge, and vertex references
- reference geometry
- assembly relationships
- links between geometry and simulation entities
- links between geometry and mesh groups
- links between geometry and boundary conditions
- links between geometry and results

The gap is not just geometry.

The gap is simulation-oriented geometry ownership and reference management.

---

## MBD Gap

### Existing Strengths

Open-source MBD solvers can provide:

- rigid body dynamics
- constraints
- joints
- motors
- contacts
- time integration
- simulation outputs

### Remaining Gap

A solver alone does not provide a full CAE workflow.

The missing application layer must handle:

- project model
- body definitions
- assembly structure
- user-defined joints
- simulation cases
- solver settings
- validation
- diagnostics
- result storage
- timeline replay
- comparison between runs
- visualization and reporting

The project should not become only a GUI for one MBD solver.

It should define an MBD workflow that can connect to solvers through adapters.

---

## FEA Gap

### Existing Strengths

Open-source FEA solvers can provide:

- structural analysis
- displacement
- stress
- strain
- thermal workflows
- modal workflows
- nonlinear workflows in some cases

### Remaining Gap

A solver does not automatically provide a clean engineering workflow.

The missing layer must handle:

- material definitions
- loads
- boundary conditions
- named selections
- mesh controls
- simulation cases
- solver input generation
- solver diagnostics
- result registration
- stress visualization
- result comparison
- reporting

The hardest part is not only running the solver.

The hard part is connecting CAD references, mesh regions, solver inputs, and result fields back to one project model.

---

## CFD Gap

### Existing Strengths

Open-source CFD tools can provide:

- flow solvers
- transient simulation
- turbulence models
- heat transfer workflows
- solver-specific case systems
- field outputs

### Remaining Gap

The missing layer must eventually handle:

- fluid domains
- boundary conditions
- fluid materials
- mesh zones
- solver case generation
- transient result storage
- field visualization
- pressure and velocity results
- coupling with structural workflows
- future FSI workflows

CFD should influence the architecture early, but it should not overload the first MVP.

---

## Meshing Gap

### Existing Strengths

Open-source meshing tools can provide:

- surface meshes
- volume meshes
- mesh sizing
- physical groups
- solver export formats
- mesh quality data

### Remaining Gap

CAE applications require meshing to be connected to:

- geometry
- named selections
- boundary conditions
- materials
- solver cases
- result mapping

The mesh should not become the only model.

Meshes are generated or derived data linked back to stable project entities.

---

## Visualization Gap

### Existing Strengths

Open-source visualization tools can provide:

- 3D rendering
- mesh display
- scalar fields
- vector fields
- animation
- post-processing
- plots and color maps

### Remaining Gap

An engineering application needs visualization to be integrated with:

- project entity IDs
- selections
- reference geometry
- simulation cases
- result sets
- timeline
- plots
- reports
- diagnostics

Visualization should display state, not own engineering truth.

---

## Results Gap

### Existing Strengths

Solvers can produce result files.

Visualization tools can display result fields.

### Remaining Gap

A CAE application must manage results as first-class engineering data.

A result system must handle:

- simulation run identity
- solver metadata
- units
- time steps
- entity references
- field data
- logs
- validity states
- stale result detection
- result comparison
- export
- reporting

The Results Layer must support both:

- time-based MBD results
- field-based FEA and CFD results

---

## Automation and AI-Agent Gap

### Existing Strengths

Many tools support scripts, APIs, command-line workflows, or configuration files.

### Remaining Gap

The missing application layer should provide a consistent operation path for:

- GUI users
- scripts
- tests
- batch workflows
- future AI agents

This requires:

- explicit commands
- structured inputs
- validation
- diagnostics
- auditable state changes
- reproducible workflows

An AI agent should not rely on hidden GUI behavior or uncontrolled file edits.

It should use the same command/application layer as human workflows.

---

## What This Project Adds

This project aims to add the missing application layer between existing tools.

It should provide:

- solver-independent model ownership
- command-driven workflows
- adapter boundaries
- result management
- validation and diagnostics
- project persistence
- visualization integration
- automation-ready operation

The project should make existing open-source engineering technologies easier to connect into coherent workflows.

---

## What This Project Does Not Add

This project should not claim to replace the existing tools.

It does not aim to replace:

- CAD kernels
- MBD solvers
- FEA solvers
- CFD solvers
- meshing tools
- visualization frameworks

It should use them.

The added value is the layer that connects them.

---

## Summary

The open-source CAE gap is not a lack of every individual component.

The gap is the missing application layer that connects those components into a coherent engineering workflow.

This initiative exists to define and eventually build that layer.
