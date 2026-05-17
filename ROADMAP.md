# Roadmap

## Purpose

This roadmap describes the proposed development path for the **Open CAE Application Layer Initiative**.

The roadmap is intentionally staged. The project should not attempt to implement the entire long-term vision at once.

The goal is to move from architecture review to a small but real CAE vertical slice, then gradually expand toward MBD, FEA, CFD-ready workflows, meshing, visualization, results, automation, and future AI-agent operation.

---

## Roadmap Principles

1. Start with architecture and technical review.
2. Build a small vertical slice before large feature expansion.
3. Keep the core model independent from GUI, solvers, and visualization.
4. Use adapters for external tools.
5. Treat results as engineering data, not visual state.
6. Make commands the shared path for GUI, scripts, tests, and future AI agents.
7. Expand gradually through verified capabilities.

---

## Phase 0: Architecture and Public RFC Foundation

### Goal

Define the project direction clearly before implementation begins.

### Outputs

- README
- Vision document
- Architecture overview
- RFC-001
- MVP definition
- open-source CAE gap map
- founding problems
- initial roadmap

### Main Questions

- Is the application-layer direction valid?
- Are the architecture boundaries correct?
- What should the first MVP prove?
- Which technical risks are most important?
- Which existing open-source tools should be targeted first?

### Success Criteria

- The project direction is understandable within a few minutes.
- The architecture can be reviewed by technical people.
- The project does not look like an empty repository or an unrealistic promise.
- Reviewers know exactly what kind of feedback is requested.

---

## Phase 1: Technical Review and Community Seeding

### Goal

Get early technical criticism from relevant people before building too much.

### Target Review Areas

- CAD and topology references
- MBD solver adapter design
- FEA workflow boundaries
- CFD-ready architecture
- meshing workflow
- results storage
- visualization responsibilities
- project file format
- human and AI command operation

### Activities

- open GitHub Discussions
- share RFC-001 with selected reviewers
- request criticism, not commitment
- collect issues and questions
- turn feedback into decisions and revisions

### Success Criteria

- useful feedback from technical reviewers
- architecture risks identified early
- first group of serious followers
- updated RFC and roadmap based on feedback

---

## Phase 2: Minimal Project Skeleton

### Goal

Create a small application foundation without implementing full CAE functionality.

### Scope

- repository structure
- project file format prototype
- core model skeleton
- application command system
- basic validation and diagnostics
- simple save/load
- test framework
- initial documentation structure

### Not in Scope

- full CAD editing
- full MBD
- FEA
- CFD
- advanced visualization
- complete UI
- production solver integration

### Success Criteria

- project state can be created, saved, loaded, and validated
- commands can modify the model
- tests can exercise the application layer without GUI
- the project foundation does not depend on one solver or GUI backend

---

## Phase 3: MBD-First Vertical Slice

### Goal

Prove the architecture through a small MBD simulation workflow.

### Scope

- simple body representation
- basic transforms
- basic joints or constraints
- simulation case definition
- first MBD solver adapter
- simulation execution service
- time-based results
- timeline-ready result data
- basic visualization or replay path
- logs and diagnostics

### Possible Backend

- Chrono as the first MBD backend
- MBDyn as a possible future comparison or adapter

### Success Criteria

- a simple mechanism can be represented in the core model
- the model can be translated through an adapter
- a simulation can run
- results can be stored independently from the solver
- motion can be replayed
- the same workflow can be driven through commands

---

## Phase 4: Geometry and Topology Workflow

### Goal

Strengthen the geometry foundation required for real CAE workflows.

### Scope

- imported geometry references
- STEP workflow
- body instances
- topology references
- face, edge, and vertex references
- reference geometry
- selection model
- geometry-to-model mapping
- diagnostics for stale or invalid references

### Success Criteria

- engineering references are not based only on transient viewport picks
- bodies can reference geometry cleanly
- topology references can be stored, resolved, validated, and reported
- future FEA/CFD boundary conditions and mesh groups have a reference foundation

---

## Phase 5: Results Infrastructure

### Goal

Build a results layer that can support more than one solver type.

### Scope

- ResultSet model
- run metadata
- simulation case links
- entity ID links
- time-series results
- field-result-ready structure
- units
- logs
- status and validity states
- export-ready structure

### Success Criteria

- MBD results are stored as engineering data
- the results system is not tied to the viewport
- the results system is not tied to one solver
- the model can later support FEA and CFD fields

---

## Phase 6: FEA Vertical Slice

### Goal

Add the first structural simulation workflow through an FEA backend.

### Scope

- material definition
- loads
- boundary conditions
- mesh generation or mesh import
- simulation case
- FEA solver adapter
- displacement results
- stress results
- basic result visualization
- export-ready data

### Possible Backends

- Code_Aster
- CalculiX

### Success Criteria

- a simple structural case can run through the application model
- loads and boundary conditions are linked to stable references
- results are stored in the Results Layer
- stress or displacement can be visualized without becoming model state

---

## Phase 7: Meshing Workflow

### Goal

Build a stronger meshing layer for FEA and future CFD.

### Scope

- mesh controls
- mesh groups
- named selections
- region definitions
- boundary region mapping
- mesh quality checks
- mesh persistence
- solver-specific mesh export

### Possible Backends

- Gmsh
- Salome
- SMESH or similar tools

### Success Criteria

- mesh data is separated from core model definition
- geometry-to-mesh mapping is explicit
- mesh groups can support boundary conditions and result mapping

---

## Phase 8: CFD-Ready Architecture and OpenFOAM Adapter Prototype

### Goal

Prepare the architecture for CFD workflows without overloading early phases.

### Scope

- CFD domain model review
- boundary condition model review
- fluid material properties
- mesh zone requirements
- transient field result requirements
- OpenFOAM adapter prototype
- result import/export experiments

### Not in Scope Initially

- full CFD GUI
- full OpenFOAM case management
- turbulence model coverage
- production-level CFD validation

### Success Criteria

- the project data model does not block CFD
- CFD requirements influence the architecture safely
- an OpenFOAM-style adapter path is understood

---

## Phase 9: Visualization and Post-Processing Expansion

### Goal

Improve engineering visualization and result interpretation.

### Scope

- result animations
- plots
- legends
- color maps
- stress and displacement plots
- pressure and velocity field visualization
- timeline integration
- result comparison
- report exports
- ParaView-compatible export path

### Success Criteria

- visualization displays results without owning them
- result playback does not mutate the initial model
- visualization works across multiple result types

---

## Phase 10: Automation and AI-Agent Operation

### Goal

Make engineering workflows reproducible and accessible to automation.

### Scope

- command API
- structured command inputs
- structured command results
- diagnostics
- scripting support
- batch execution
- agent-safe operation model
- validation gates
- audit logs

### Success Criteria

- important operations can be performed without manual GUI-only behavior
- scripts and future AI agents can use the same command path as the GUI
- automated workflows are reproducible and auditable

---

## Phase 11: Verification, Benchmarks, and Credibility

### Goal

Make the project credible as engineering software.

### Scope

- benchmark cases
- analytical checks
- regression tests
- solver comparison cases
- result validation
- mesh convergence examples
- documented limitations

### Success Criteria

- the project does not rely only on visual demos
- engineering results can be checked against known cases
- claims are tied to verification evidence

---

## Phase 12: Broader CAE Platform Growth

### Goal

Expand from a working foundation into a broader open CAE platform.

### Possible Areas

- advanced MBD
- advanced FEA
- nonlinear cases
- contact workflows
- thermal workflows
- CFD workflows
- FSI
- multiphysics
- design studies
- optimization
- reporting
- plugins
- external tool integrations
- education examples
- community-maintained adapters

### Success Criteria

- growth happens through layers and adapters
- new capabilities do not break the core architecture
- the project remains modular and open

---

## Near-Term Priority

The immediate priority is not implementation of all features.

The near-term priority is:

1. finish the core architecture documents
2. open the RFC process
3. request technical review
4. refine the MVP definition
5. build the smallest MBD-first vertical slice

---

## Summary

The roadmap starts with architecture, review, and credibility.

It then moves to a small MBD-first vertical slice.

Only after the architecture is proven should the project expand toward FEA, CFD, meshing, advanced visualization, automation, AI-agent operation, and multiphysics workflows.
