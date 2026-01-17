## 自我一致性

### 1. Overview
Self-Consistency 本质上是一种 decoding / sampling 策略：
- 通过多次独立采样，让模型暴露其最稳定的推理结论。
- 通过降低单次推理偶然性带来的错误，从而提升复杂任务中的稳定性与准确率。

模型不会判断“对不对”，只判断“像不像同一个答案”

---

### 2. Prompt Skeleton

针对给定任务，生成多个相互独立的推理过程，
并基于一致性原则确定最终答案。
每一次推理必须彼此独立，不得相互引用。

每一次推理应：
- 尝试使用不同视角或思路
- 避免逻辑路径的高度相似

在完成所有推理后：
- 仅比较最终答案（不比较推理过程）
- 选择出现频率最高的答案
- 若不存在明显一致结果，输出 "Uncertain"

若多个结果差异明显，
不得强行选择答案，
应输出 "Uncertain"。


constraints：
1. 生成多个相互独立的推理路径。
2. 不得复用其他推理中的表述、结构或结论。
3. 不得默认某次推理是正确的。
4. 每次推理应视为一次全新的解题尝试。

boundary awareness：
自我一致性并不等于正确性。
多个推理一致也可能是错误的。
在可信度不足时，应优先选择 "Uncertain"。


---

## 3. Related Strategies 关联策略

Task Decomposition

Verification Prompting

Hallucination Mitigation

Multi-Constraint Prompting 多约束控制

---

 
