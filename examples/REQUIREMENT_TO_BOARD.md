# Example — Requirement to Verified Board

This example illustrates Volta's execution model without exposing the private implementation.

## Intent

> Design an analog preamplifier with a specified gain, supply, physical constraints, and manufacturing target.

## 1. Capture requirements

The system records the requested gain, supply range, I/O, board constraints, cost or component constraints, and target manufacturing assumptions as durable requirements rather than leaving them only in a prompt.

## 2. Discover unknowns

Before implementation, the workflow identifies missing or ambiguous information such as source impedance, load, bandwidth, noise target, headroom, connector choice, environmental limits, or enclosure constraints.

## 3. Propose architecture

A model or specialist may propose topology and component choices. The proposal is not yet authoritative.

## 4. Create design state

Approved operations update the structured circuit representation through explicit tool contracts.

## 5. Electrical verification

Connectivity and electrical-rule checks run against the actual design state. Failures block progression.

## 6. Behavioral verification

Simulation tests the design against explicit acceptance criteria.

Example failure path:

```text
Requirement: gain >= 40 dB
        |
        v
Simulation result: 38.4 dB
        |
        v
GATE FAILED
        |
        v
Agent diagnoses likely feedback-network mismatch
        |
        v
Proposed component-value change
        |
        v
Design state updated through bounded operation
        |
        v
Simulation rerun: 40.2 dB
        |
        v
GATE PASSED
```

The important part is not the diagnosis; it is that the new design is not accepted until the verifier produces new evidence.

## 7. PCB constraints and layout

Placement, board geometry, net classes, routing, clearances, vias, planes, connectors, and mounting constraints become part of the authoritative design state.

## 8. PCB verification

Design-rule validation tests the actual board artifacts. A failed rule produces new work rather than a model-generated waiver.

## 9. Manufacturing validation

The system reconciles the design with the selected fabrication/assembly path, component/package facts, and required output artifacts.

## 10. Release

Manufacturing release occurs only when required evidence is current, blocking unknowns are resolved or explicitly waived, and the necessary approval is present.

## What this demonstrates

Volta uses AI to handle ambiguity, planning, investigation, diagnosis, and design strategy while keeping correctness, durable state, evidence, and consequential side effects under system control.
