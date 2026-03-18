# Computational Logic of Time (CLT)
## Core Specification

Version: 1.0  
Status: Final  
Date: 2026-03-18 (UTC)  

Author: Jan Zdráhal  
ORCID: https://orcid.org/0009-0005-2012-1234  
DOI: https://doi.org/10.5281/zenodo.19083118  

License: CC BY-ND 4.0  
Copyright © 2026 Jan Zdráhal

---

## 1. Definition

Computational Logic of Time (CLT) is a minimal, system-independent formal framework for expressing and evaluating temporal propositions over ordered state sequences.

CLT defines:

- a discrete time domain
- a state mapping over time
- a formal language of temporal formulas
- an evaluation semantics

CLT does NOT define:

- system architecture
- storage models
- execution mechanisms
- transition systems

---

## 2. Formal Model

CLT is defined as a tuple:

```
CLT = (T, Σ, P, S, Φ, ⟦·⟧)
```

Where:

- T is a discrete, totally ordered set (time domain)
- Σ is a state space
- P is a set of atomic propositions, where p ∈ P : Σ → {true, false}
- S : T → Σ is a deterministic state mapping
- Φ is a set of well-formed formulas
- ⟦·⟧ is an evaluation function

---

## 3. Time Domain

T is a discrete, totally ordered set (T, <).

Define successor function:

```
succ : T → T ∪ {⊥}
```

such that:

```
succ(t) = min { t' ∈ T | t' > t }
succ(t) = ⊥ if no such t' exists
```

Properties:
- totally ordered
- discrete
- may be finite or infinite

---

## 4. State Mapping

```
S : T → Σ
```

Assigns a state to each time point.

CLT assumes S is deterministic,
but does not define system determinism.

---

## 5. Formula Language

### 5.1 Atomic Propositions

```
P : Σ → {true, false}
```

Define constant proposition:

```
true : Σ → {true, false}
```

such that:

```
true(s) = true for all s ∈ Σ
```

### 5.2 Core Syntax (BNF)

```
<formula> ::= <atomic>
            | "¬" <formula>
            | <formula> "∧" <formula>
            | "X" <formula>
            | <formula> "U" <formula>
            | "(" <formula> ")"
```

### 5.3 Operator Precedence (highest to lowest)

1. ¬, X
2. U
3. ∧
4. ∨ (derived)
5. → (derived)

### 5.4 Associativity

```
¬, X → right
U → right
∧ → left
```

### 5.5 Derived Operators

```
φ ∨ ψ ≡ ¬(¬φ ∧ ¬ψ)
φ → ψ ≡ ¬φ ∨ ψ
◇ φ ≡ true U φ
□ φ ≡ ¬◇¬φ
φ R ψ ≡ ¬(¬φ U ¬ψ)
```

---

## 6. Evaluation Semantics

```
⟦φ⟧(S, t) ∈ {true, false}
```

### 6.1 Atomic

For p ∈ P:

```
⟦p⟧(S, t) = p(S(t))
```

### 6.2 Boolean

```
⟦¬φ⟧(S, t) = true iff ⟦φ⟧(S, t) = false

⟦φ ∧ ψ⟧(S, t) = true iff
    ⟦φ⟧(S, t) = true AND ⟦ψ⟧(S, t) = true
```


### 6.3 Temporal

#### Next (Strong)

If succ(t) ≠ ⊥:

```
⟦X φ⟧(S, t) = ⟦φ⟧(S, succ(t))
```

If succ(t) = ⊥:

```
⟦X φ⟧(S, t) = false
```

#### Until

```
⟦φ U ψ⟧(S, t) = true iff
    ∃t' ∈ T, t' ≥ t :
        ⟦ψ⟧(S, t') = true AND
        ∀t'' ∈ T, (t ≤ t'' < t') :
            ⟦φ⟧(S, t'') = true
```
---

## 7. Derived Semantics (Theorems)

From definitions in Sections 5.5 and 6:

```
⟦◇ φ⟧(S, t) = true iff
    ∃t' ∈ T, t' ≥ t : ⟦φ⟧(S, t') = true

⟦□ φ⟧(S, t) = true iff
    ∀t' ∈ T, t' ≥ t : ⟦φ⟧(S, t') = true
```

---

## 8. Evaluation Properties

CLT defines evaluation semantics only.

For infinite time domains:

- evaluation of temporal operators may not terminate
- this is consistent with LTL semantics

---

## 9. Relationship to Existing Work

CLT corresponds to Linear Temporal Logic (LTL) interpreted over a single linear trace.

Unlike standard LTL formulations based on Kripke structures, CLT eliminates:

- transition systems
- branching semantics

and operates directly on:

```
S : T → Σ
```

CLT is not a new temporal logic.

It is a minimal evaluation framework
for applying LTL semantics to concrete state sequences.

---

## 10. Properties

- system-independent
- data-independent
- evaluation-oriented
- linear-time only

---

## 11. Scope Boundaries

CLT explicitly excludes:

- transition systems
- branching semantics
- persistence
- identity / hashing
- distributed semantics

---

## 12. Minimal Core

- atomic propositions
- ¬
- ∧
- X
- U

---

## 13. Intended Use

- audit systems
- compliance validation
- financial invariants
- monitoring systems
- AI decision trace evaluation

## 14. Conclusion

CLT provides a minimal, formally precise,
and fully consistent evaluation layer
for temporal reasoning over discrete state sequences.
