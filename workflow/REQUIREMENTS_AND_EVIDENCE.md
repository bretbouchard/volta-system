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
- evidence
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

The design is not considered current until affected evidence has been regenerated or explicitly waived.

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
- test measurements

Claims should point to evidence rather than model confidence.
