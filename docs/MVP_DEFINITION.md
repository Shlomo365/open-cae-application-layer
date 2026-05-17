# MVP Definition

## Purpose

This document defines the proposed first MVP for the **Open CAE Application Layer Initiative**.

The MVP should be small, focused, and architectural.

It should not attempt to implement the full long-term vision. Its purpose is to prove that the main layers of the system can work together in a real engineering workflow.

---

## MVP Summary

The proposed first MVP is an **MBD-first vertical slice**.

It should prove that the project can:

- define an engineering model in a solver-independent core model
- execute a simple multibody simulation through a solver adapter
- store time-based results independently from the solver
- replay motion through a visualization path
- drive the workflow through commands
- keep a clean path toward future FEA, CFD, meshing, and multiphysics workflows

The MVP is not about feature count.

The MVP is about proving the architecture.

---

## Why MBD First

MBD is a strong first vertical slice because it tests many core architecture concepts early:

- bodies
- transforms
- coordinate frames
- joints
- constraints
- motors
- simulation cases
- time stepping
- solver adapters
- results over time
- animation
- diagnostics

It also produces visible motion, which makes the result easier to understand and demonstrate.

MBD-first does not mean MBD-only.

The architecture must remain open to FEA, CFD, meshing, field results, and coupled workflows.

---

## MVP Goals

The MVP should demonstrate the following.

### 1. Project Creation and Persistence

The user should be able to create a project, save it, and load it again.

The project should include:

- metadata
- units
- bodies or body definitions
- simulation cases
- solver settings
- result references where applicable

The project file should be open, readable, and versioned.

### 2. Solver-Independent Core Model

The MVP should include a minimal core model that is not dependent on GUI objects, visualization objects, or solver runtime objects.

Required core concepts may include:

- Project
- MechanicalModel
- Body
- Transform
- Joint or Constraint
- Motor or motion input
- SimulationCase
- SolverSettings
- ResultSet reference
- Units

The model does not need to be complete.

It needs to be clean enough to prove the architecture.

### 3. Command-Driven Workflow

Important operations should be performed through commands or application services.

Example commands:

- create project
- add body
- set body transform
- create joint
- create motor
- create simulation case
- run simulation
- load results
- replay result state

The GUI, tests, scripts, and future AI agents should use the same command path.

### 4. Basic MBD Simulation

The MVP should run a simple MBD case.

Possible example cases:

- pendulum
- two-body revolute joint
- slider-crank simplified case
- motor-driven rotating body
- constrained body under gravity

The simulation should run through a solver adapter, not through direct GUI-to-solver code.

### 5. Solver Adapter Boundary

The MBD solver adapter should:

- validate supported inputs
- translate the core model to solver-specific runtime data
- run or prepare the simulation
- collect diagnostics
- return results to the Results Layer
- map solver objects back to stable project entity IDs

The adapter should not become the project model.

### 6. Time-Based Results

The MVP should store basic time-based result data.

Possible result data:

- body transforms over time
- body velocities
- body accelerations
- joint reaction data if available
- motor data if available
- solver diagnostics
- time step information

Results should be stored as engineering data, not only as visual animation state.

### 7. Timeline / Replay

The MVP should support basic motion replay.

The replay does not need to be visually advanced.

It should prove that:

- result time steps can be loaded
- body states can be queried by time
- visualization can display result state
- result playback does not modify the initial model state

### 8. Diagnostics

The MVP should include useful diagnostics.

Examples:

- unsupported joint type
- missing body
- invalid simulation case
- solver unavailable
- failed run
- stale result
- unit mismatch warning
- missing geometry reference

Good diagnostics are part of the product, not an afterthought.

---

## MVP Non-Goals

The MVP should not include:

- full CAD editing
- full sketching
- full assembly constraints
- full FEA
- full CFD
- advanced meshing
- advanced contact modeling
- advanced stress visualization
- production-level post-processing
- plugin system
- full AI agent interface
- full optimization or design studies
- complete UI polish
- full commercial-CAE feature parity

The MVP must remain small enough to finish.

---

## Minimal Workflow

A possible MVP workflow:

1. Create a new project.
2. Add one or more simple bodies.
3. Assign transforms.
4. Define a basic joint or constraint.
5. Define a motor or initial condition.
6. Create a simulation case.
7. Run the simulation through an MBD adapter.
8. Store results.
9. Replay motion on a timeline.
10. Save and reload the project.
11. Inspect logs and diagnostics.

This workflow is intentionally small.

It should prove that the core architecture is usable.

---

## Architecture Requirements for the MVP

The MVP must respect these rules:

1. The Core Model is the source of truth.
2. The GUI must not directly modify engineering state outside commands.
3. The solver must be accessed through an adapter.
4. Solver runtime objects must not become persistent project objects.
5. Results must be stored independently from visualization.
6. Replay must not mutate initial model state.
7. Project files must be open and versioned.
8. The command path must be usable by GUI and future automation.
9. The design must not block future FEA, CFD, or meshing.
10. Diagnostics must be structured and useful.

---

## Suggested MVP Entities

The MVP may include minimal versions of these entities:

```text
Project
MechanicalModel
Body
Transform
Joint
Motor
SimulationCase
SolverSettings
SimulationRun
ResultSet
TimeSeriesResult
Units
CommandResult
DiagnosticMessage
```

These do not need to be final.

They should be simple enough to implement and strong enough to test the architecture.

---

## Suggested First Simulation Cases

### Case 1: Pendulum

Purpose:

- test body, joint, gravity, time results, replay

### Case 2: Motor-Driven Revolute Joint

Purpose:

- test motor input, joint motion, time-based results

### Case 3: Slider-Crank Simplified Mechanism

Purpose:

- test multiple bodies and constraints

Only one case is required for the earliest MVP.

Additional cases can become benchmark examples.

---

## Acceptance Criteria

The MVP can be considered successful when:

- a project can be created, saved, loaded, and validated
- a simple MBD model exists in the core model
- a simulation case can be executed through an adapter
- result data is registered in the Results Layer
- motion can be replayed from stored results
- logs and diagnostics are available
- the workflow can be driven through commands
- tests can verify the model and application layer without relying only on the GUI
- future FEA, CFD, and meshing remain architecturally possible

---

## What the MVP Should Communicate Publicly

The MVP should communicate:

> This project is not just a vision document. It has an application architecture that can drive a real engineering workflow end to end.

It should not claim:

> This is a complete CAE platform.

The correct message is:

> This is the first verified vertical slice of a broader open CAE application-layer architecture.

---

## Summary

The first MVP should be a small MBD-first vertical slice that proves the architecture, not the entire vision.

It should show that a solver-independent core model, command-driven application layer, solver adapter, results system, and visualization/replay path can work together in a coherent engineering workflow.
