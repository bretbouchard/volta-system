# Validation Pipeline

Volta uses layered verification. Passing one layer does not imply the next will pass.

## 1. Structural validation
Confirm the design representation is internally valid and round-trippable.

## 2. Electrical validation
Check connectivity, power intent, pin use, shorts, unconnected nets, and rule violations.

## 3. Behavioral simulation
Where appropriate, simulate expected performance against explicit acceptance criteria.

## 4. Component validation
Verify package, electrical ratings, availability/source facts, and relevant manufacturer constraints.

## 5. PCB validation
Validate placement constraints, board geometry, net classes, routing, clearances, vias, planes, and physical rules.

## 6. Manufacturing validation
Confirm the selected fabrication/assembly path can accept the actual artifacts and constraints.

## 7. Release gate
Before manufacturing or other external side effects:
- requirements reconciled
- blocking unknowns resolved
- required evidence current
- approvals satisfied
- manufacturing package reproducible

## Failure behavior

A failed hard gate blocks advancement. It must not be converted into a model-generated reassurance.

The model may diagnose the failure and propose a correction, but a new deterministic check is required to clear the gate.
