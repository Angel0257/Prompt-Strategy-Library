## 思维链

Thinking Chain（链式推理）通过显式展开模型的中间推理步骤，使模型在执行复杂子任务时保持逻辑连贯，降低跳步推理和隐藏错误。

English
Thinking Chain improves reasoning quality by explicitly expanding intermediate reasoning steps, reducing logical jumps and hidden errors during task execution.

一句话核心定义（非常关键）

Thinking Chain is about HOW the model reasons, not WHAT the task is.
链式推理解决的是“怎么想”，而不是“做什么”。

## prompt

```text
任务：
通过逐步推理的方式完成以下任务。

规则：
1. 显式生成中间推理步骤。
2. 确保每一步在逻辑上承接前一步。
3. 禁止跳步或直接给出结论。
4. 不得引入新的子任务。
5. 推理仅用于内部，最终仅输出答案。

```

## Evaluation Signals 评估指标
| Metric             | 中文说明       |
| ------------------ | ---------- |
| Logical Coherence  | 推理逻辑连贯性    |
| Step Completeness  | 中间步骤完整度    |
| Error Reduction    | 相比无推理的错误下降 |
| Hallucination Rate | 是否因推理引入幻觉  |

## When to Use / When NOT to Use
**适合使用：**
数学 / 逻辑推理
规则判断
多条件决策
子任务执行阶段

**不适合使用：**
纯事实检索
强约束输出任务
高风险幻觉场景（配合 verification）

---
