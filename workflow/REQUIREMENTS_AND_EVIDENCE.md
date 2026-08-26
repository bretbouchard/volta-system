# Requirements and Evidence

Volta treats requirements as a living engineering artifact rather than a prompt.

## Requirement lifecycle

Each significant requirement should have:

- stable ID
- statement
- source
- priority
- status
- affected subsystems
- acceptance criteria
- expected outcome where the requirement asserts a real-world effect
- implementation evidence
- outcome evidence where applicable
- dependent decisions
- change history
- unresolved questions

## Change impact

When a requirement changes, the system identifies downstream artifacts and decisions that may now be invalid.

Examples:

- supply voltage changes → topology, regulator, capacitor ratings, thermal checks
- enclosure changes → board outline, connector location, mounting holes
- target manufacturer changes → stackup, minimum trace/space, drill rules, BOM constraints
- cost ceiling changes → part selection and assembly choices
- environmental requirement changes → ratings, derating, materials, compliance

The design is not considered current until affected implementation evidence has been regenerated or explicitly waived.

Where a requirement also asserts a physical or operational outcome, that outcome remains separately unvalidated until observed evidence supports it.

## Evidence model

Evidence can include:

- ERC results
- simulation output
- DRC results
- component datasheet facts
- manufacturer capabilities
- dimensional checks
- cost/BOM calculations
- generated manufacturing artifacts
- human review
- bench measurements
- thermal and power measurements
- bring-up results
- manufacturing feedback
- field reliability observations

Claims should point to evidence rather than model confidence.

## Implementation evidence vs outcome evidence

Implementation evidence answers whether the design was produced correctly according to current requirements and validation rules.

Outcome evidence answers whether the resulting hardware actually produced the intended real-world effect.

A passing ERC, DRC, simulation, manufacturing package, or release gate does not by itself prove the physical outcome.

For consequential Changes, preserve the chain:

```text
Requirement / intent
  ↓
Expected outcome
  ↓
Design Change
  ↓
Implementation verification
  ↓
Fabrication / assembly / operation
  ↓
Observed outcome evidence
  ↓
Outcome Validated | Outcome Failed | Inconclusive
```

Observed failures or discrepancies become governed evidence. They may expose unknowns, invalidate assumptions, or justify follow-up work, but they must not silently rewrite requirements.
