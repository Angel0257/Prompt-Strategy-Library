
## 1. Overview
**Task Decomposition** improves reliability by breaking a complex task into smaller, manageable, and verifiable sub-tasks, reducing cognitive load and compounding errors.

任务分解通过将复杂任务拆解为多个可控、可验证的子任务，降低单步认知负荷与推理错误率，从而提升整体任务的可解释性与成功率。

---

## 2. 
**任务：**
将以下复杂任务拆解为一组清晰、有序的子任务。

**规则：**
1. 每个子任务应具备原子性，且可独立理解。
2. 子任务需按逻辑顺序排列。
3. 不得执行或解答子任务。
4. 不得输出推理过程或解释说明。
5. 避免过度或不必要的拆分。

**输出格式：**
1. 子任务 1
2. 子任务 2
3. 子任务 3

---

## 3. 
### Instructions
Please complete the task following this strict workflow:

**Step 1: Entity Extraction**
Identify all product names, dates, and error codes mentioned in the text. List them out.

**Step 2: Sentiment Analysis**
Analyze the tone of the user. Assign a sentiment score from 1 (Angry) to 5 (Happy). Explain the reason for your score based on keywords used.

**Step 3: Categorization**
Classify the complaint into ONE of the following categories: [Hardware Issue, Software Bug, Shipping, Billing].

**Step 4: Formatting**
Based on the results from Steps 1-3, generate a strict JSON object. Do not add any markdown formatting or explanation outside the JSON.

### Output Schema
{
  "entities": [],
  "sentiment_score": 0,
  "category": "",
  "summary": ""
}
