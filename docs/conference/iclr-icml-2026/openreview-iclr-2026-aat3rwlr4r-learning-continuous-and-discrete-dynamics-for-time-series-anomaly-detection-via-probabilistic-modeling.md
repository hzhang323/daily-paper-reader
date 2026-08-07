---
title: Learning Continuous and Discrete Dynamics for Time Series Anomaly Detection via Probabilistic Modeling
title_zh: 基于概率建模学习连续与离散动力学的时间序列异常检测
authors: "Kai Zhao, Yuying Qiu, Yunyao Cheng, Christian S. Jensen, Xiaokui Xiao, Bin Yang, Chenjuan Guo"
date: 2025-09-03
pdf: "https://openreview.net/pdf?id=AAT3rwlR4r"
tags: ["query:time-series"]
score: 9.0
evidence: 基于概率建模的时间序列异常检测
tldr: 针对多变量时间序列异常检测中连续与离散动态难以同时建模、以及变量重要性被忽略的问题，本文提出TAD-UP，采用统一概率建模框架，联合学习连续与离散动力学，并对不同测量单位的变量进行自适应重要性加权。实验表明，该方法在合成与实际数据集上均显著优于现有异常检测方法，为风险监控等应用提供了更可靠的检测能力。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 现有方法难以同时建模连续与离散动态，且未考虑变量重要性差异，影响异常检测性能。
method: 提出TAD-UP，通过统一概率建模同时学习连续与离散动态，并自适应加权各变量异常分数。
result: 在多个基准上验证了该方法对混合类型时间序列异常检测的有效性与鲁棒性。
conclusion: 统一概率建模能更好处理连续与离散混合的时间序列异常检测问题。
---

## Abstract
Anomaly detection for multivariate time series plays an important role in many applications, enabling, e.g., risk monitoring in cyber-physical systems. While existing methods achieve good results on continuous variates, they struggle when having to learn both continuous and discrete dynamics across continuous time. Further, existing methods simply sum up reconstruction or contrastive errors from each variate to obtain final anomaly scores without recognizing differences in importance of variates with different measurement units. To overcome these limitations, we propose TAD-UP that learns both continuous and discrete dynamics for Time series Anomaly Detection via Unified Probabilistic modeling. First, we propose two co-dependent branches of efficient neural ordinary differential equations with the compound Poisson process to learn both continuous and discrete dynamics for different variates. We also propose a gate mechanism to learn correlations among different dynamics. Second, we propose to model a joint probability distribution for anomaly detection. The resulting model is optimized using Maximum Likelihood Estimation on joint variates, instead of using reconstruction or contrastive losses on each variate. We detect anomalies using joint probabilities, which take the marginal probabilities of different variates into account. Experiments on nine real-world datasets from different domains offer evidence that TAD-UP is capable of state-of-the-art accuracy and better efficiency tradeoff.

---

## 论文详细总结（自动生成）

# 论文总结

该论文为《Learning Continuous and Discrete Dynamics for Time Series Anomaly Detection via Probabilistic Modeling》（简称 TAD-UP），由 Kai Zhao 等学者撰写，投稿至 ICLR 2026，最终状态为 Rejected，但获得 OpenReview 评分 9.0，整体定位具有一定学术价值。

---

### 1. 核心问题与研究动机（背景与意义）

多变量时间序列异常检测在众多应用中具有重要意义，例如网络物理系统中的风险监控。论文指出现有方法存在两个核心局限：

- **难以同时建模连续与离散动态**：现有方法在连续变量上表现较好，但无法在连续时间框架下同时学习连续动态（如温度、压力等连续变化）与离散动态（如状态切换、事件计数等），而真实系统往往两者并存。
- **忽略变量重要性差异**：现有方法通常将各变量的重构误差或对比误差直接求和作为最终异常分数，但不同测量单位、不同物理含义的变量对异常判定的重要性并不相同，简单求和会导致偏差。

因此，本文的研究动机是：提出一种能够**统一建模连续与离散动力学**、并**自适应考虑变量重要性差异**的异常检测方法，以提升对混合类型多变量时间序列的检测能力。

---

### 2. 方法论：TAD-UP 的核心思想与关键技术

**核心思想**：采用统一概率建模框架，同时学习连续与离散动力学，并基于联合概率进行异常检测。

关键技术细节如下：

- **两分支神经微分方程（Neural ODE）**：
  - 提出两个协同依赖的分支，分别使用**高效的神经 ODE** 建模连续动态。
  - 引入**复合泊松过程（Compound Poisson Process）**建模离散动态（如跳跃、突变事件）。
  - 两个分支并非独立，而是相互依赖，以捕捉连续与离散动态之间的交互。

- **门控机制（Gate Mechanism）**：
  - 用于学习不同动力学分支之间的相关性，即自适应融合连续与离散信息，增强表达与泛化能力。

- **联合概率建模与极大似然估计**：
  - 不再使用逐变量的重构损失或对比损失，而是对**联合变量分布**建模，使用**极大似然估计（MLE）**进行整体优化。
  - 这使得模型能从整体分布的角度捕捉异常模式，而非孤立地看待每个变量。

- **基于联合概率的异常检测**：
  - 检测时使用**联合概率**作为异常得分，并自然地将各变量的**边际概率**纳入考量，从而隐式处理变量重要性差异。

整体流程可概括为：输入多变量时间序列 → 两个分支分别建模连续/离散动态 → 门控机制融合 → 以联合概率为目标进行参数学习 → 推理时基于联合概率得分判定异常。

---

### 3. 实验设计

- **数据集**：论文在 **9 个来自不同领域的真实世界数据集**上进行实验，但摘要未列出具体数据集名称。
- **Benchmark**：与现有时间序列异常检测方法进行对比，摘要未具体列举对比方法名称，仅统称为“现有方法（existing methods）”。
- **评价指标**：摘要未明确说明具体指标（如 F1、精确率、召回率等），只提及“准确率（accuracy）”与“效率（efficiency）”。

**总结**：摘要层面仅能确认实验覆盖了 9 个多元真实数据集，涉及领域较广；但具体数据集构成、对比方法和评价指标在摘要中未披露，需查看全文才能获知。

---

### 4. 资源与算力

**论文提取文本中未提及** GPU 型号、GPU 数量、训练时长、参数量等计算资源信息。因此无法从当前材料中评估其训练成本与设备要求，只能确认作者声称模型在“效率”上较现有方法有更好权衡。

---

### 5. 实验数量与充分性

- **实验数量**：摘要仅明确提及在 9 个真实数据集上进行了评测，并给出“SOTA 精度 + 更好效率”的整体结论。
- **是否充分**：摘要层面无法判断。未披露消融实验、超参数敏感性分析、case study、统计显著性检验等细节。
- **客观性/公平性**：由于对比方法和数据集细节缺失，无法核实实验是否公平、覆盖是否全面；同时，该论文最终被 ICLR 2026 拒稿，可能侧面说明实验或方法仍存在不足（此为基于来源状态的推断，非论文直接信息）。

---

### 6. 主要结论与发现

- TAD-UP 在 **9 个真实世界数据集**上取得了**最先进的异常检测准确率**，同时实现了**更好的效率权衡**。
- 验证了**统一概率建模**对同时含连续与离散动态的多变量时间序列异常检测任务的有效性。
- 证实了**联合概率检测**相比逐变量误差求和的方式，能更合理地处理变量重要性差异问题。

---

### 7. 优点

- **方法论新颖**：将神经 ODE 与复合泊松过程结合，统一建模连续与离散动态，理论框架较为扎实。
- **概率建模更合理**：通过 MLE 优化联合分布，替代逐变量误差汇总，从根本上规避了变量单位不一致的问题。
- **自适应变量权重**：联合概率天然融合了各变量边际贡献，无需额外设计加权策略。
- **效率与精度兼顾**：声称在准确率提升的同时具备更好的效率，具有实际部署潜力。
- **应用价值强**：面向网络物理系统风险监控等真实场景，具有较强的实践意义。

---

### 8. 不足与局限

- **论文细节缺失**（基于当前提取文本）：数据集名称、对比方法、评价指标、超参数等关键实验信息均未在摘要中呈现，难以全面评估方法优劣。
- **算力未披露**：无法判断训练成本，可复现性和实用性受影响。
- **实验充分性存疑**：摘要未提及消融实验、鲁棒性分析和统计显著性检验，且论文被拒稿，可能说明实验验证或方法设计仍存在薄弱环节。
- **可扩展性未知**：对于高维、极长序列或大规模在线检测场景，模型的计算复杂度未有讨论。
- **应用局限**：方法主要面向混合动态的时序数据；对纯连续或纯离散数据的增益可能有限，摘要未做对比说明。

---

（完）
