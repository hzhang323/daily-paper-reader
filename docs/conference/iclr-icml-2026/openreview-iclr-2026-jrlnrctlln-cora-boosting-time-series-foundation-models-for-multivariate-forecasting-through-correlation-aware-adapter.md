---
title: "CoRA: Boosting Time Series Foundation Models for Multivariate Forecasting through Correlation-aware Adapter"
title_zh: CoRA：通过相关性感知适配器提升多元时序预测的基础模型
authors: "Hanyin Cheng, Xingjian Wu, Yang Shu, Zhongwen Rao, Lujia Pan, Bin Yang, Chenjuan Guo"
date: 2026-01-26
pdf: "https://openreview.net/pdf?id=JRlNrcTllN"
tags: ["query:time-series"]
score: 9.0
evidence: 面向多元预测的时序基础模型相关感知适配器
tldr: 针对现有时间序列基础模型（TSFM）忽略通道相关性的问题，提出CoRA轻量级即插即用适配器。将相关性矩阵分解为低秩时变与时不变成分，仅需微调即可捕获不同通道间相关性。在多元时序预测上有效提升基础模型的预测性能，同时保持较低计算复杂度。该工作为TSFM在多变量场景下的应用提供了高效的增强方案。
source: ICLR-2026-Accepted
selection_source: conference_retrieval
motivation: 现有TSFM多采用通道独立建模，忽视通道间的相关性，限制了多元预测性能。
method: 提出CoRA适配器，将通道相关性分解为低秩时变与时不变成分，通过微调增强TSFM。
result: 实验表明CoRA在多元时序预测任务上显著提升TSFM的性能，且开销低。
conclusion: 为时间序列基础模型在多元相关场景下的应用提供了轻量可复用的改进方法。
---

## Abstract
Most existing Time Series Foundation Models (TSFMs) use channel independent modeling and focus on capturing and generalizing temporal dependencies, while neglecting the correlations among channels or overlook the different aspects of correlations. However, these correlations play a vital role in Multivariate time series forecasting. To address this, we propose a Correlation-aware Adapter (**CoRA**), a lightweight plug-and-play method that requires only fine-tuning with TSFMs and is able to capture different types of correlations, so as to improve forecast performance. Specifically, to reduce complexity, we innovatively decompose the correlation matrix into low-rank Time-Varying and Time-Invariant components. For the Time-Varying component, we further design learnable polynomials to learn dynamic correlations by capturing trends or periodic patterns. To learn positive and negative correlations that appear only among some variables, we introduce a novel dual contrastive learning method that identifies correlations through projection layers, regulated by a Heterogeneous-Partial contrastive loss during training, without introducing additional complexity in the inference stage. Extensive experiments on 10 real-world datasets demonstrate that CoRA improves the state-of-the-art TSFMs in average forecast performance.

---

## 论文详细总结（自动生成）

# 论文总结：CoRA —— 相关性感知适配器用于多元时序预测

## 1. 核心问题与整体含义（研究动机与背景）

- **问题背景**：现有时间序列基础模型（Time Series Foundation Models, TSFMs）大多采用**通道独立（channel independent）建模**策略，即每个变量通道单独处理，主要致力于捕捉和泛化**时间维度上的依赖关系**。
- **关键缺陷**：这种建模方式**忽视了不同变量（通道）之间的相关性**。即便部分方法尝试建模相关性，也未能区分相关性的不同类型与特性（如时变与时不变、正相关与负相关、全局与局部相关）。
- **核心动机**：在多变量时间序列预测（multivariate time series forecasting）中，通道间的相关性对预测精度**至关重要**。忽略这些信息会显著制约基础模型的性能上限。
- **论文主张**：提出一种轻量级、即插即用的**相关性感知适配器（CoRA, Correlation-aware Adapter）**，在不重新训练整个基础模型的前提下，仅通过微调即可捕获多种类型的通道相关性，从而**提升现有先进TSFM在多元预测任务上的表现**。

## 2. 论文提出的方法论

**核心思想**：以**轻量级适配器**的形式嵌入现有TSFM，将通道相关性矩阵进行结构化分解，并设计相应的学习机制，在不显著增加计算开销的前提下，让基础模型具备跨通道相关性建模能力。

**关键技术细节（文字说明）**：

- **相关性矩阵的低秩分解**：
  - 为降低相关性建模的复杂度，CoRA将完整的通道相关性矩阵分解为两个组成部分：
    - **低秩时变（Time-Varying）成分**：捕捉随时间演变的动态相关性；
    - **低秩时不变成分（Time-Invariant）成分**：刻画通道之间长期稳定的静态相关结构。
  - 这种分解有效避免了直接建模全量相关性矩阵带来的高计算开销。

- **可学习多项式机制（Learnable Polynomials）**：
  - 针对**时变成分**，设计了可学习的多项式函数，用于建模相关性随时间的变化趋势，能够捕捉通道相关性中的**趋势性（trends）与周期性（periodic patterns）**，从而更精确地刻画动态相关结构。

- **异质-部分对比学习（Heterogeneous-Partial Contrastive Learning）**：
  - 针对仅存在于**部分变量之间**的正相关与负相关，引入了一种新的**双对比学习（dual contrastive learning）** 方法。
  - 通过**投影层（projection layers）** 学习通道相关性表征，并使用 **Heterogeneous-Partial 对比损失（contrastive loss）** 在训练阶段对相关结构进行约束与监督。
  - 该机制的关键优势是：对比学习的额外复杂度**仅存在于训练阶段**，在**推理（inference）阶段不引入任何额外开销**。

- **即插即用特性**：CoRA以适配器形式与各类现成TSFM结合，只需微调适配器参数，无需改动或重新预训练整个基础模型。

## 3. 实验设计

- **数据集与场景**：论文在 **10个真实世界数据集** 上进行了广泛实验，覆盖多元时间序列预测的主要场景（具体数据集名称在提供文本中未逐一列出）。
- **Benchmark 设定**：以当前**最先进的TSFM（state-of-the-art TSFMs）** 作为基准模型与对比对象，评估CoRA加装后对这些模型的性能提升效果。
- **对比方法**：主要是各类主流/先进的时间序列基础模型（具体模型名称在提供文本中未逐一列举），以及在同等条件下未加装CoRA的原始模型（用于验证模块增量贡献）。

## 4. 资源与算力

- 提供的论文文本中**未明确说明**具体使用的GPU型号、数量、训练时长、参数量等算力与资源信息。
- 仅能从方法论上判断：由于采用**低秩分解**和**轻量适配器**设计，CoRA的计算复杂度显著低于直接全量建模相关性矩阵的方法；但具体的数值化资源开销（如FLOPs、额外参数占比、训练时间增长比例）在文本中未给出，有待原文补充。

## 5. 实验数量与充分性

- **实验数量**：
  - 在 **10个真实数据集** 上进行了主要性能评估；
  - 方法设计中包含多个组件（低秩分解、可学习多项式、双对比学习），按学术惯例应有相应的**消融实验（ablation study）** 验证各组件贡献；但所提供文本未明确展开消融细节。
- **充分性评估**：
  - **优点**：10个数据集的覆盖规模在时序预测领域属于相对充分的实验设置；跨多个数据集验证有利于说明方法的泛化性。
  - **局限性/不确定性**：所提供的提取文本**未列出具体对比基线、基准模型名称、各数据集上的具体数值**，因此无法从现有材料中判断实验是否覆盖了多样性足够高的数据领域（如金融、能源、交通、天气等），也难以确认是否做了统计显著性检验、误差棒分析、不同参数规模下的鲁棒性测试等。整体而言，需阅读全文才能对实验公平性与充分性做出更严谨的结论。

## 6. 主要结论与发现

- CoRA在**10个真实数据集**上，一致性地提升了**现有最先进TSFM的平均预测性能**。
- 通过捕捉**时变与时不变**、**正向与负向**、**全局与局部**等多维度的通道相关性，CoRA有效弥补了TSFM在多元预测中忽略跨通道信息的短板。
- 该方法以**轻量级、即插即用**的方式实现上述提升，保持了较低的复杂度，训练成本可控，**不增加推理阶段开销**，适合实际部署。

## 7. 优点

- **方法设计创新性强**：
  - 将相关性矩阵分解为**低秩时变 + 时不变成分**，在建模能力和计算效率之间取得了较好的平衡；
  - 借鉴对比学习思想处理**部分变量间的异质相关性（正/负相关共存）**，设计角度新颖且训练-推理阶段解耦。
- **实用性强**：
  - 即插即用架构，可适配主流已有TSFM，无需重新预训练基础模型，工程落地成本低；
  - 面向实际部署场景友好，推理阶段无额外开销。
- **实验规模较好**：10个真实数据集上的广泛验证增强了结论的可信度；
- **问题定位准确**：针对TSFM领域普遍存在的“通道独立假设”这一关键瓶颈开展研究，研究动机清晰、有现实需求支撑。

## 8. 不足与局限

- **实验信息在现有材料中不够完整**：所提供文本未列出具体数据集领域、对比模型名称、预测长度设置、误差指标数值等细节，难以对实验设计与结论的完整性做出全面判断；
- **资源/复杂度报告不透明**：论文提取文本中未提供计算资源使用量（GPU型号、训练时间）、额外参数占比等具体数据，影响对其“轻量”主张的量化评估；
- **可能存在的偏差风险**：
  - 若实验集中于特定类型数据集，可能对方法的跨领域泛化性结论产生偏差影响；
  - 需要确认是否对不同TSFM规模（如小参数量与大参数量基础模型）均做了验证，以排除方法仅适用于特定模型规模的可能性；
- **应用限制**：CoRA主要面向**多元**时序预测场景；对于单变量预测或无通道相关结构的场景，预期收益有限；
- **理论支撑深度**：相关性分解与多项式设计的理论性质（如分解唯一性、多项式阶数的选择依据）在提供文本中未展开论述；
- **超参数敏感性未知**：如低秩维度、多项式阶数、对比学习损失权重等关键超参数对性能的影响，在提取内容中未说明，可能影响复现与适用范围。

---

（完）
