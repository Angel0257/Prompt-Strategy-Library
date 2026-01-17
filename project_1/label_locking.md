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
<Selected Label>
```

---

## 6. Before / After Comparison

**Without Label Locking**
- Output varies across runs
- Occasional new labels appear
- Explanatory text mixed with labels

**With Label Locking**
- Stable label selection across runs
- Zero label invention
- Clean outputs suitable for automation

---

## 7. Evaluation Signals

This strategy can be evaluated using lightweight metrics:
- Label Set Compliance Rate
- Cross-run Consistency
- Invalid Output Rate
- Human Review Correction Frequency

Even small-scale manual testing (10–20 samples) is sufficient
to observe improvements.

---

## 8. Trade-offs and Limitations

- May reduce nuance in borderline cases
- Forces decisions where ambiguity exists
- Should be combined with boundary clarification strategies
  when label definitions overlap heavily

---

## 9. Applicable Scenarios

- Dataset annotation pipelines
- AI-assisted moderation systems
- Large-scale tagging workflows
- Prompt-driven data preprocessing

---

## 10. Related Strategies

- Boundary Clarification
- Output Schema Enforcement
- Uncertainty Expression Control

---
