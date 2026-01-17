
# Strategy: Hallucination Mitigation

# 消除幻觉

---

## 1. Strategy Overview

Hallucination Mitigation is a prompt engineering strategy that suppresses fabricated, unsupported, or misleading outputs through **explicit constraints, evidence grounding, uncertainty exposure, and strict output control**.
The core goal is not to maximize answers, but to **maximize correctness by allowing abstention**.

幻觉消除（Hallucination Mitigation）的核心目标不是“让模型尽量回答”，而是**让模型在不确定时选择不回答**。

---

## 2. Target Task Types

### 适用任务类型

该策略更适合 **LLM 作为“系统组件”而非“创作助手”** 的场景。

* Fact-based Question Answering 事实型问答
* Knowledge Extraction / Summarization 知识抽取 / 总结
* Reference-sensitive Content Generation 需依赖来源的生成
* Factual Classification & Labeling 事实约束分类


---

## 3. Common Failure Modes Addressed

### 主要对抗的模型失效模式

| Failure Mode           | Description                          | 中文解释    |
| ---------------------- | ----------------------------------------- | ----------- |
| Fabrication            | Model invents non-existent facts          | 模型编造不存在的信息  |
| Confident Misstatement | Wrong answers delivered confidently       | 错误但语气极其肯定   |
| Contradiction          | Inconsistent outputs across turns or runs | 前后输出自相矛盾    |
| Unsupported Reference  | Cites sources not in context              | 引用未提供或虚假的来源 |

---

## 4. Design Rationale

### 4.1 Uncertainty as a Valid Output

Explicitly allowing `"Unknown"` reduces hallucination more effectively than forcing completion.

通过允许并鼓励输出 `"Unknown"`来降低幻觉率。

---

### 4.2 Evidence-Bounded Generation
 
The model is strictly bounded to explicitly provided input, with no external inference or world knowledge allowed.

模型只能使用**输入中显式提供的信息**，禁止使用“常识补全”或外部推断。

---

### 4.3 Answer / Reasoning Separation

 
Suppressing reasoning prevents the model from hallucinating justifications to sound coherent.

隐藏推理过程，避免模型“为了显得合理而编造解释”。


---

## 5. Prompt Skeleton

```text
You are a factual information processor.

Constraints:
1. Only answer using information explicitly provided in the input.
2. If the answer cannot be determined with certainty, output "Unknown".
3. Do NOT infer, assume, or fabricate any facts.
4. Do NOT cite sources unless they appear in the input.
5. Output must strictly follow the format below.

Output Format:
<Answer>

Do not include explanations, reasoning steps, or additional commentary.
```

---

## 6. Advanced Variants

### 6.1 Evidence Quotation Mode

 
要求模型在回答后**逐字引用证据片段**（若无证据则 Unknown）。

---

### 6.2 Dual-Pass Verification


第一次生成答案，第二次只做“是否有证据”的验证。

Use a second pass solely to verify evidence existence.

---

### 6.3 Boundary Sample Injection

在 few-shot 中加入“看似合理但信息缺失”的边界样本，强化拒答能力。

Inject borderline examples where refusal is correct.

---

## 7. Before / After Comparison

### Without Hallucination Mitigation

* Invented facts appear
* Overconfident tone
* Hard to use in automated pipelines

### With Hallucination Mitigation

* Correct use of `"Unknown"`
* Zero fabricated references
* Stable, automation-ready output
* High cross-run consistency

---

## 8. Evaluation Signals
### 评估指标

| Metric                | Description |
| --------------------- | ----------- |
| Unknown Precision     | 正确拒答的比例     |
| Fabrication Rate      | 幻觉输出占比      |
| Cross-run Consistency | 多次运行一致性     |
| Human Correction Rate | 人工修正频率下降    |

> 这些指标可直接用于 **prompt A/B 测试 + 数据回流优化**

---

## 9. Related Prompt Strategies

### 关联策略

* Constraint Layering 多层约束
* Verification Prompting 验证型提示
* Output Schema Enforcement 结构化输出
* Self-Consistency (with Abstention) 带拒答的一致性

---
