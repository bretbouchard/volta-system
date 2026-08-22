# Volta Public Architecture

## Architectural rule

The authoritative world state lives outside the language model. Models receive controlled projections of that state and may propose actions through explicit tools.

```text
User / Product Intent
          |
          v
+-----------------------+
| Requirements Ledger   |
| constraints + history |
+-----------+-----------+
            |
            v
+-----------------------+
| Planning / Discovery  |
| unknowns + decisions  |
+-----------+-----------+
            |
            v
+-----------------------+
| Domain Specialists    |
| EE / PCB / MFG review |
+-----------+-----------+
            |
            v
+-----------------------+
| Design State          |
| circuit + board IR    |
+-----------+-----------+
            |
     +------+------+
     |             |
     v             v
Simulation      Component facts
ERC / DRC       package / stock / MFG
     |             |
     +------+------+
            v
+-----------------------+
| Evidence + Gatekeeper |
+-----------+-----------+
            |
            v
+-----------------------+
| Approved side effects |
| export / manufacture  |
+-----------------------+
```

## Components

### Requirements ledger
Durable product and engineering requirements. Requirements are versioned, traceable, and evaluated after material changes.

### Modeled design state
The canonical representation of the current schematic, PCB, constraints, selected components, and manufacturing intent.

### Planning layer
Breaks work into verifiable steps and preserves dependencies.

### Unknown discovery
Actively identifies assumptions, missing specifications, unsupported claims, component uncertainty, and unverified manufacturing constraints.

### Specialist review
Different engineering viewpoints may investigate the same decision independently. Findings must identify evidence and uncertainty.

### Tool layer
Models act through explicit capabilities rather than arbitrary shell access. Tools can read authoritative state, propose mutations, run deterministic verification, or produce artifacts.

### Governance
Potentially destructive, expensive, externally visible, or manufacturing-related actions require policy checks and appropriate approval.

### Evidence
Verification outputs are stored as evidence attached to the design state and decisions that depend on them.

## Model independence

Volta is not designed around one model provider. Models are replaceable processors. The surrounding system defines state, permissions, constraints, workflow, evidence, and side effects.
