# Validation Pipeline

Volta uses layered verification. Passing one layer does not imply the next will pass, and passing every implementation gate does not prove that the physical design achieved its intended outcome.

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
- expected physical outcome recorded where relevant

## 8. Physical outcome observation
After fabrication, assembly, bring-up, or deployment, compare observed reality against the expected outcome.

Outcome evidence may include:
- bench measurements
- thermal behavior
- power behavior
- signal-integrity measurements
- simulation-to-hardware discrepancies
- bring-up failures
- manufacturing defects
- component substitutions
- field reliability
- user or engineer feedback

This stage answers a different question from the earlier gates.

Implementation verification asks:

> Was the design produced correctly according to the current requirements and checks?

Outcome validation asks:

> Did the resulting hardware actually achieve the intended effect in reality?

The two states must remain separate.

```text
Implementation: Not Started → Executing → Implemented → Verified
Outcome:        Not Observed → Observing → Outcome Validated | Outcome Failed | Inconclusive
```

A board may therefore be fully `Verified` while its physical outcome is still unobserved, failed, or inconclusive.

## Reality Feedback

Observed physical evidence feeds back into GSA's Modeled World and Historian.

A failed or contradictory outcome may expose a new unknown, invalidate an assumption, threaten a requirement, or justify a new governed Change. It must not silently rewrite durable requirements or bypass GSD and Obdurate.

## Failure behavior

A failed hard gate blocks advancement. It must not be converted into a model-generated reassurance.

The model may diagnose the failure and propose a correction, but a new deterministic check is required to clear the gate.

Likewise, a failed real-world outcome is preserved as outcome evidence even if the original implementation passed every prior validation layer.
