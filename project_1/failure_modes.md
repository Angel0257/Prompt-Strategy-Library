## Overview

This document lists common failure modes observed in LLM-based
classification and tagging tasks.

The focus is on **recurring, systemic issues** that impact output
consistency and downstream usability.

---

## FM-1: Label Drift

**Description**  
The model outputs labels outside the predefined label set.

**Typical Symptoms**
- Invented or renamed labels
- Combined labels (e.g. "Neutral-Positive")

**Impact**
- Schema violations
- Manual correction required

**Primary Fix Direction**
- Label Locking
- Output Schema Enforcement

---

## FM-2: Boundary Ambiguity

**Description**  
Inconsistent labeling near category boundaries.

**Typical Symptoms**
- Different labels for similar inputs
- Output variance across runs

**Impact**
- Low annotation agreement
- Reduced trust in results

**Primary Fix Direction**
- Boundary Clarification
- Decision Forcing

---

## FM-3: Multi-Label Confusion

**Description**  
Multiple labels returned when only one is allowed.

**Typical Symptoms**
- Label lists
- Conjunctions in output

**Impact**
- Invalid outputs
- Parsing failures

**Primary Fix Direction**
- Single-choice Enforcement
- Output Format Constraints

---

## FM-4: Over-Explanation Leakage

**Description**  
Explanatory text included in label-only outputs.

**Typical Symptoms**
- Sentences instead of atomic labels
- Mixed structured/unstructured output

**Impact**
- Downstream automation breakage

**Primary Fix Direction**
- Output Schema Control
- Verbosity Constraints

---

## FM-5: Cross-Run Instability

**Description**  
Identical inputs produce different labels across runs.

**Typical Symptoms**
- Label flipping
- High output variance

**Impact**
- Unreliable production behavior

**Primary Fix Direction**
- Deterministic Prompting
- Explicit Fallback Rules

---

## Summary Table

| Failure Mode | Core Risk | Fix Direction |
|-------------|-----------|---------------|
| Label Drift | Schema violation | Label Locking |
| Boundary Ambiguity | Inconsistency | Boundary Clarification |
| Multi-Label Confusion | Invalid output | Single-choice Enforcement |
| Over-Explanation | Parsing failure | Output Control |
| Cross-Run Instability | Low reliability | Deterministic Prompting |

---

## Notes

- Failure modes often co-occur
- Each strategy targets a specific failure mechanism
- This document serves as a quick diagnostic reference
