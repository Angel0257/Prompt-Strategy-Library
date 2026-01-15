# Strategy: Label Locking

## 1. Strategy Overview

**Label Locking** is a prompt design strategy used to prevent large language models
from inventing, drifting, or inconsistently applying classification labels.

The core idea is to explicitly constrain the model to a closed label set
and enforce deterministic selection behavior when uncertainty arises.

This strategy is particularly effective in annotation, tagging,
and content moderation scenarios where label consistency is critical.

---

## 2. Target Task Type

- Text classification
- Content tagging
- Intent recognition
- Annotation consistency tasks

---

## 3. Common Failure Modes Addressed

This strategy is designed to mitigate the following failure modes:

### 3.1 Label Drift
- The model creates new labels not defined in the task
- Example: Outputting “Neutral-positive” when only “Positive / Neutral / Negative” are allowed

### 3.2 Boundary Ambiguity
- The model switches labels across runs for similar inputs
- Often occurs when classes are semantically close

### 3.3 Over-Explanation Leakage
- The model embeds reasoning or commentary into the output
- Breaks downstream parsing or automation pipelines

---

## 4. Strategy Design Rationale

Language models are generative by default.
When classification instructions are underspecified,
the model optimizes for semantic richness rather than label fidelity.

**Label Locking works by:**
1. Explicitly defining a closed label set
2. Prohibiting label creation or modification
3. Forcing a single-label decision even under uncertainty
4. Separating classification output from explanation (or removing explanation entirely)

This reduces entropy in the output space and improves stability.

---

## 5. Prompt Structure (Skeleton)

```text
You are performing a classification task.

You must choose exactly ONE label from the following list:
[Label A, Label B, Label C]

Rules:
- Do NOT create new labels
- Do NOT modify label names
- Output only the selected label
- If uncertain, choose the closest matching label

Output format:
<label>
