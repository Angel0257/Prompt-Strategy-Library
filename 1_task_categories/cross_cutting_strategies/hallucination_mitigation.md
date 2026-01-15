# Strategy: Hallucination Mitigation

## 1. Strategy Overview
Hallucination Mitigation prevents the model from generating fabricated, unsupported, or misleading information by applying explicit constraints, uncertainty handling, and output control.

---

## 2. Target Task Types
- Fact-based QA
- Summarization / Knowledge extraction
- Content generation requiring references
- Classification with factual grounding

---

## 3. Common Failure Modes Addressed
| Failure Mode | Description |
|-------------|-------------|
| Fabrication | Model invents facts, events, or references |
| Confident Misstatement | Incorrect answers with confident tone |
| Contradiction | Inconsistent or conflicting outputs |
| Unsupported Reference | Cites sources or info not provided |

---

## 4. Design Rationale
- **Explicit Uncertainty Handling:** Output "Unknown" when unsure
- **Absolute Prohibition of Unsupported Content:** Do not fabricate
- **Evidence Requirement:** Only use context or verified sources
- **Structured Output:** Separate answers from commentary

---

## 5. Prompt Skeleton

```text
You are tasked with providing a factual answer.
Rules:
1. Only answer what is explicitly known or provided.
2. If unsure or unsupported, respond with "Unknown".
3. Do NOT fabricate facts, events, or references.
4. Provide output strictly in the following format:
   <Answer>
5. Do not include reasoning or additional commentary.

Example output:
<Answer>
```

## 6. Before / After Comparison

Without Hallucination Mitigation

- Outputs include invented details or references
- Confident tone hides uncertainty
- Downstream automation or QA is error-prone

With Hallucination Mitigation

- Clearly outputs "Unknown" when uncertain
- Avoids any fabricated content
- Structured output suitable for automation
- Consistent across multiple runs

## 7. Evaluation Signals

- Unknown Usage Rate – % of cases where model correctly outputs "Unknown"
- Fabrication Rate – % of outputs containing unsupported content
- Consistency Across Runs – same input produces same valid/Unknown output
- Human Review Correction Frequency – reduced need for manual correction

## 8. Applicable Scenarios

- Customer support / helpdesk bots
- Knowledge base generation
- Educational content summarization
- Any LLM workflow requiring factual reliability

## 9. Related Strategies

- Output Schema Enforcement
- Constraint Layering
- Uncertainty Expression Control
