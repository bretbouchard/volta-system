# Volta System Atlas

**From intent to manufacturable electronics — with evidence, constraints, and validation at every step.**

This repository is the public **System Atlas** for Volta. It documents the architecture, engineering model, validation philosophy, representative execution flow, and selected implementation evidence behind the private production system.

Volta is an AI-native electronics design system for turning requirements into real schematics, PCBs, and manufacturing outputs.

## Why Volta exists

Generative models are good at proposing designs. Electronics requires something stricter.

A plausible-looking schematic can still be electrically wrong. A valid schematic can still fail simulation. A routed PCB can still violate manufacturing constraints. A design can pass local checks while silently violating a requirement captured weeks earlier.

Volta therefore treats the model as a **planner and problem-solving component**, not the source of truth.

The system owns:

- requirements
- design state
- component facts
- constraints
- verification evidence
- decisions and rationale
- manufacturing outputs

Every material change must be reconciled against that state.

## Core workflow

```text
Intent / requirements
        ↓
Requirements ledger
        ↓
Planning + unknown discovery
        ↓
Circuit architecture
        ↓
Schematic generation / mutation
        ↓
Electrical validation
        ↓
Simulation + evidence
        ↓
PCB constraints + placement
        ↓
Routing
        ↓
Design-rule validation
        ↓
Manufacturing package
        ↓
Human approval / release
```

## What is implemented behind this public surface

The private implementation combines AI orchestration with real EDA and manufacturing workflows rather than treating PCB generation as a text-generation problem.

Its engineering surface includes:

- Python-based orchestration and domain tooling
- structured circuit and PCB representations
- explicit design operations and transactional rollback patterns
- electrical-rule and design-rule validation
- circuit simulation against acceptance criteria
- component and manufacturing data sources
- placement and routing orchestration
- local multimodal inference on Apple Silicon
- electronics-specific model adaptation/training workflows
- automated tests across mutation, validation, simulation, and artifact generation
- BOM and fabrication/assembly artifact generation

The source, private datasets, internal component data, and production implementation remain private.

## Agent + tool boundary

```text
Model / Specialist
       |
       | structured proposal or tool call
       v
Tool Contract
       |
       v
Authorization / Policy
       |
       v
Domain Operation
       |
       v
Authoritative Design-State Mutation
       |
       v
Deterministic Verification
       |
       v
Evidence + Decision Record
```

The model is valuable for ambiguity reduction, planning, investigation, diagnosis, and strategy. It cannot clear its own verification failures or declare its own proposed design correct.

## Design principles

### 1. Requirements survive the whole project

Volta carries initial requirements and later changes forward as explicit constraints. A late change in supply voltage, enclosure, connector, thermal limits, cost, or manufacturer can invalidate work far downstream. The system must make that visible.

### 2. Models do not own reality

A model may propose a circuit, choose a component, recommend a route, or explain a tradeoff. It does not get to declare a result correct. The authoritative state is maintained outside the model and verified through deterministic tools and evidence.

### 3. Hard gates beat confident prose

Where a deterministic check exists, Volta uses it:

- electrical-rule checks
- simulation
- design-rule checks
- component and package validation
- manufacturing constraints
- artifact round-trip checks

A failed gate blocks progression rather than becoming a warning inside an AI response.

### 4. Unknowns are first-class

Missing information is not silently guessed. The workflow identifies unresolved assumptions, records them, and either investigates or requests a decision before the assumption becomes expensive.

### 5. Every important decision is explainable

Design decisions retain the requirement, evidence, alternatives, constraint, and outcome that caused them.

## Representative case study

See [Requirement to Verified Board](examples/REQUIREMENT_TO_BOARD.md) for a public example of how a requirement moves through unknown discovery, design-state mutation, failed simulation, model diagnosis, deterministic re-verification, PCB validation, and governed release.

The important behavior is that a model may propose the fix, but only new evidence clears the gate.

## System documentation

- [Public Architecture](system/ARCHITECTURE.md)
- [Agent and Tool Integration Model](system/INTEGRATION_MODEL.md)
- [Requirements and Evidence](workflow/REQUIREMENTS_AND_EVIDENCE.md)
- [Validation Pipeline](workflow/VALIDATION_PIPELINE.md)
- [Requirement to Verified Board](examples/REQUIREMENT_TO_BOARD.md)

## Relationship to GSA

Volta is a domain application of the [GSA System Atlas — Governed Stewardship Architecture](https://github.com/bretbouchard/gsa-system): controlled model access to authoritative state, explicit tools, durable memory, unknown discovery, specialist review, sequenced work, evidence, and governed side effects.

Volta adds electronics-specific rigor because small requirement changes can alter the final physical product, component selection, routing, cost, compliance, or manufacturability.

## What this System Atlas contains

Public here:

- system boundaries and design rationale
- technology and integration choices
- validation and evidence patterns
- representative execution flows
- selected implementation evidence

Kept private:

- proprietary implementation code
- internal training data
- private component databases
- internal planning state
- production credentials
- unpublished product details

## Status

Volta is under active development. The production implementation is maintained privately; this repository is its public System Atlas.
