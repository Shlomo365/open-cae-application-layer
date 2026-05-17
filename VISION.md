# Vision

## Project Name

**Open CAE Application Layer Initiative**

This is an architecture-first open-source initiative to define and eventually build the missing application layer for professional engineering simulation workflows.

The project is not intended to start as a finished product. It starts as a clear technical direction, an RFC process, and a focused attempt to define the architecture required for an open CAE workflow that can grow over time.

---

## Vision Statement

Open-source engineering already has strong individual tools: CAD kernels, solvers, meshing tools, visualization frameworks, and post-processing systems.

What is missing is a coherent CAE application layer that connects these tools into one professional engineering workflow.

The long-term vision is to create an open, modular CAE desktop platform that can connect:

- CAD and geometry workflows
- assembly modeling
- multibody dynamics
- finite element analysis
- CFD-ready workflows
- meshing
- visualization
- results management
- reporting
- automation
- future AI-agent operation

The goal is not to replace existing open-source tools.

The goal is to connect them through a clean, solver-independent, application-level architecture.

---

## The Problem

Open-source CAE is not missing every technical component.

Many important components already exist:

- geometry kernels and CAD systems
- MBD solvers
- FEA solvers
- CFD solvers
- meshing tools
- visualization frameworks
- post-processing tools

The problem is fragmentation.

A complete engineering workflow often requires moving between different tools, different file formats, different assumptions, different data models, and different result systems.

This makes open-source CAE harder to use, harder to automate, harder to validate, and harder to extend.

The missing piece is the application layer that organizes the engineering workflow above individual tools.

---

## What This Project Is Trying to Become

The project should become a modular open-source CAE application layer with:

- a solver-independent core model
- a command-driven application layer
- stable project files
- geometry and topology reference handling
- solver adapters
- results management
- visualization workflows
- validation and diagnostics
- automation-friendly operations
- a path toward AI-agent-operated engineering workflows

The project should eventually support multiple engineering domains through adapters and well-defined data boundaries.

The first goal is not to implement every simulation type.

The first goal is to define a correct structure and prove it through a small vertical slice.

---

## Long-Term Scope

The long-term scope includes the following domains.

### CAD / Geometry

The project should support geometry and CAD workflows through existing open-source technologies and concepts.

Relevant areas include:

- imported geometry
- STEP workflows
- B-Rep geometry
- topology references
- faces, edges, and vertices
- reference geometry
- coordinate systems
- assembly structure

### MBD

Multibody dynamics is the proposed first practical vertical slice.

Relevant areas include:

- rigid bodies
- joints
- constraints
- motors
- contacts
- gravity
- simulation cases
- time stepping
- motion results
- timeline replay
- reaction forces and diagnostics

### FEA

Finite element analysis is a major long-term target.

Relevant areas include:

- materials
- loads
- boundary conditions
- mesh generation
- stress
- strain
- displacement
- modal analysis
- thermal-structural workflows
- nonlinear workflows in the future

### CFD

CFD is part of the long-term architecture, not the first MVP.

Relevant areas include:

- fluid domains
- boundary conditions
- mesh zones
- field results
- transient results
- turbulence models
- OpenFOAM-style workflows
- future fluid-structure interaction

### Meshing

Meshing must connect geometry to simulation domains.

Relevant areas include:

- mesh controls
- mesh groups
- named selections
- boundary regions
- mesh quality
- geometry-to-mesh mapping
- mesh-to-result mapping

### Visualization and Results

The project should support engineering visualization and result review.

Relevant areas include:

- motion animation
- stress plots
- displacement plots
- velocity and acceleration plots
- contact forces
- joint reactions
- pressure fields
- temperature fields
- legends
- color maps
- plots
- timeline
- result comparison
- reports

---

## What Success Looks Like

### Early Success

Early success means the project has:

- a clear public technical direction
- reviewed architecture documents
- open questions that attract useful feedback
- a first MVP definition
- technical reviewers from relevant fields
- a small group of people following the project seriously

At this stage, success is not measured by feature count.

It is measured by clarity, credibility, and technical review.

### MVP Success

MVP success means the project proves an end-to-end architecture through a small MBD-first vertical slice.

The MVP should show:

- a project can be created and saved
- simple bodies can exist in a solver-independent core model
- basic joints or constraints can be defined
- a simulation can run through a solver adapter
- time-based results can be stored
- motion can be replayed
- the workflow can be driven through commands
- the design does not block future FEA, CFD, meshing, or coupled workflows

### Long-Term Success

Long-term success means the project becomes a real open-source CAE platform where humans and automated agents can define, run, inspect, compare, and report engineering simulations using open tools through a coherent application workflow.

Long-term success also means the project becomes useful to contributors, researchers, educators, engineers, and open-source tool communities.

---

## Guiding Principles

### 1. Application Layer, Not Solver Reinvention

The project should not write new solvers unless there is a very specific reason.

It should connect existing solvers through adapters.

### 2. Core Model as Source of Truth

The internal project model should be the source of truth.

The source of truth should not be the GUI, a solver runtime object, a viewport actor, a mesh file, or a temporary solver output.

### 3. Clear Layer Boundaries

The project should maintain clear boundaries between:

- GUI
- application logic
- commands
- core model
- geometry
- meshing
- solver adapters
- results
- visualization
- storage
- automation

### 4. Human and AI Operation Through the Same Commands

Human GUI users, scripts, tests, and future AI agents should operate the system through the same command/application layer.

This makes workflows reproducible, testable, and auditable.

### 5. Gradual Implementation

The project should start small.

The long-term vision is broad, but the first implementation should be a focused vertical slice.

### 6. Technical Honesty

The project should clearly distinguish between:

- implemented features
- proposed architecture
- future roadmap
- open questions
- research risks

Credibility matters more than hype.

---

## What This Project Should Never Become

The project should avoid becoming:

- a direct wrapper around one solver
- a GUI demo with weak engineering foundations
- a collection of disconnected scripts
- a clone of commercial CAE software
- a replacement campaign against existing open-source tools
- a project that claims support before validation exists
- an AI buzzword project without reproducible engineering commands

---

## Positioning

The simplest way to describe the project is:

> Open-source engineering has many strong tools. This initiative focuses on the missing CAE application layer that can connect them into one coherent workflow.

That is the core vision.
