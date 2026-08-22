# Volta System

**From intent to manufacturable electronics — with evidence, constraints, and validation at every step.**

Volta is an AI-native electronics design system for turning requirements into real schematics, PCBs, and manufacturing outputs. The implementation is private; this repository documents the public architecture, engineering model, and validation philosophy behind the system.

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

## System layers

See [system/ARCHITECTURE.md](system/ARCHITECTURE.md) for the public architecture.

See [workflow/REQUIREMENTS_AND_EVIDENCE.md](workflow/REQUIREMENTS_AND_EVIDENCE.md) for long-term requirement tracking.

See [workflow/VALIDATION_PIPELINE.md](workflow/VALIDATION_PIPELINE.md) for the verification model.

## Relationship to GSA

Volta is a domain application of the same governed-agent principles used across the broader GSA architecture: controlled model access to state, explicit tools, durable memory, unknown discovery, specialist review, sequenced work, and governed side effects.

Volta adds electronics-specific rigor because small requirement changes can alter the final physical product, component selection, routing, cost, compliance, or manufacturability.

## What this public repository is

This is an architectural and product-facing repository.

It intentionally does **not** contain:
- proprietary implementation code
- internal training data
- private component databases
- internal planning state
- production credentials
- unpublished product details

The purpose is to show how Volta is designed and why the system is structured this way.

## Status

Volta is under active development. The production implementation is maintained privately.
