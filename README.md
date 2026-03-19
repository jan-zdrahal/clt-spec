# Computational Logic of Time (CLT)

Version: 1.0  
Status: Public Release  
Date: 2026-03-18  

Author: Jan Zdráhal  
ORCID: https://orcid.org/0009-0005-2012-1234  
DOI: https://doi.org/10.5281/zenodo.19083118  

---

## Overview

Computational Logic of Time (CLT) is a formal, system-independent framework for evaluating temporal propositions over ordered state sequences.

CLT defines a minimal semantic model for reasoning about time-dependent properties without introducing transition systems, branching structures, or execution assumptions.

---

## Conceptual Structure

The specification is organized into the following conceptual layers:

### 1. Time Domain

Defines a totally ordered set of time points.

- linear ordering (t₀ < t₁ < t₂ < ...)
- discrete or abstract time representation
- no metric or physical time assumption

---

### 2. State Mapping

Defines how states are assigned to time.

- mapping S: T → Σ
- Σ as abstract state space
- no constraints on state structure

---

### 3. Temporal Language

Defines the set of valid temporal formulas.

- propositional base
- temporal operators (e.g. X, F, G, U)
- well-formed formula constraints

---

### 4. Evaluation Semantics

Defines how formulas are evaluated over a trace.

- interpretation over a single linear sequence
- no branching semantics
- deterministic truth evaluation

---

## Scope

This specification defines:

- a formal time domain
- a state mapping over time
- a temporal logic language
- an evaluation function over traces

This specification does NOT define:

- system architecture
- execution models
- transition systems
- storage mechanisms
- concurrency or branching semantics

---

## Formal Model

CLT is defined as:

CLT = (T, Σ, S, Φ, ⟦·⟧)

Where:

- T is a totally ordered time domain
- Σ is a state space
- S: T → Σ is a state mapping
- Φ is a set of well-formed temporal formulas
- ⟦·⟧ is an evaluation function over (T, S)

---

## Relation to Other Systems

CLT:

- corresponds to Linear Temporal Logic (LTL) evaluated over a single trace
- removes transition system dependency
- removes branching-time semantics (e.g. CTL)

CLT is:

- execution-agnostic
- storage-agnostic
- deterministic at the evaluation level

---

## Intended Use

CLT serves as a foundational semantic layer for:

- deterministic logs and ledgers
- temporal audit systems
- invariant verification over time
- formal reasoning about system evolution

CLT is designed to be embedded into higher-level systems, including:

- Deterministic System Specification (DSS)
- Deterministic Ledger models
- Audit and compliance frameworks

---

## Conformance

A system conforms to CLT if it:

- provides a totally ordered time domain
- defines a deterministic state mapping S
- evaluates temporal formulas according to CLT semantics

---

## License

CC BY-ND 4.0
