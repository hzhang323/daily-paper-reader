---
title: "CC-Time: Cross-Model and Cross-Modality Time Series Forecasting"
title_zh: CC-Time：面向时间序列预测的跨模型与跨模态学习
authors: "Peng Chen, Yihang Wang, Yang Shu, Yunyao Cheng, Kai Zhao, Zhongwen Rao, Lujia Pan, Bin Yang, Chenjuan Guo"
date: 2025-09-19
pdf: "https://openreview.net/pdf?id=Ktd8Zus4G8"
tags: ["query:time-series"]
score: 9.0
evidence: 将预训练语言模型应用于时间序列预测，探索跨模型与跨模态学习
tldr: 针对当前基于预训练语言模型的时间序列预测方法未能充分发挥语言模型序列建模能力的问题，提出CC-Time方法，从跨模型与跨模态两个角度增强PLM对时间序列特征的利用。该方法系统探究PLM可建模的时间序列特征以及单独依赖PLM是否足以构建时序模型，并在预测任务上取得更优的准确性。该工作为语言模型在时间序列预测中的应用提供了新的思路和实证基础。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 现有基于预训练语言模型的时间序列预测方法尚不能达到语言模型应有的序列建模精度，预测准确性不足。
method: 提出CC-Time框架，从跨模型与跨模态两方面探索PLM对时间序列特征的建模潜力，并设计相应的特征与学习策略。
result: 在时间序列预测任务上，CC-Time相比已有PLM-based方法取得更优的预测精度，验证了跨模型跨模态学习的有效性。
conclusion: 研究表明合理利用PLM的跨模型跨模态信息能够显著提升时间序列预测性能，为后续PLM时序建模提供参考。
---

## Abstract
With the success of pre-trained language models (PLMs) in various application fields beyond natural language processing, language models have raised emerging attention in the field of time series forecasting (TSF) and have shown great prospects. However, current PLM-based TSF methods still fail to achieve satisfactory prediction accuracy matching the strong sequential modeling power of language models. To address this issue, we propose Cross-Model and Cross-Modality Learning with PLMs for time series forecasting (CC-Time). We explore the potential of PLMs for time series forecasting from two aspects: 1) what time series features could be modeled by PLMs, and 2) whether relying solely on PLMs is sufficient for building time series models. In the first aspect, CC-Time incorporates cross-modality learning to model temporal dependency and channel correlations in the language model from both time series sequences and their corresponding text descriptions. In the second aspect, CC-Time further proposes the cross-model fusion block to adaptively integrate knowledge from the PLMs and time series model to form a more comprehensive modeling of time series patterns. Extensive experiments on nine real-world datasets demonstrate that CC-Time achieves state-of-the-art prediction accuracy in both full-data training and few-shot learning situations.

---

## 论文详细总结（自动生成）

## 论文中文总结

### 1. 核心问题与整体含义（研究动机与背景）
- 预训练语言模型（PLM）在自然语言处理之外的多个领域取得成功，近年来被引入时间序列预测（TSF）并展现出潜力。
- 然而，现有基于 PLM 的时间序列预测方法**未能达到与语言模型强大序列建模能力相匹配的预测精度**，准确性不足。
- 论文的核心问题：如何充分挖掘 PLM 在时间序列建模中的潜力，具体包括：
  - PLM 能够建模哪些时间序列特征？
  - 仅依赖 PLM 是否足以构建有效的时间序列预测模型？

### 2. 论文提出的方法论（核心思想与技术细节）
- 提出 **CC-Time**（Cross-Model and Cross-Modality Learning），从两个角度增强 PLM 对时间序列的建模能力：
  - **跨模态学习（Cross-Modality Learning）**：
    - 将时间序列序列与其对应的**文本描述**同时输入语言模型。
    - 在 PLM 内部同时建模**时间依赖**和**通道相关性**，使模型能利用文本模态补充时序信息。
  - **跨模型融合（Cross-Model Fusion）**：
    - 设计跨模型融合模块，**自适应地整合** PLM 提取的知识与专门时间序列模型提取的知识。
    - 目标是对时间序列模式形成更全面的建模，避免单独依赖 PLM 的局限。
- 论文在摘要中未给出具体公式或算法流程，但可推断其流程为：
  1. 将原始时间序列编码为 token 序列，并生成对应的文本描述；
  2. 将两类输入送入 PLM 进行联合建模；
  3. 同时用传统时间序列模型提取互补特征；
  4. 通过融合模块自适应结合两者输出，得到最终预测。

### 3. 实验设计（数据集、场景、基准与方法）
- 数据集：使用 **9 个真实世界数据集**，但摘要未列出具体名称。
- 场景：包括**全量数据训练**和**少样本学习（few-shot learning）**两种情形。
- Benchmark：与现有 **PLM-based 时间序列预测方法**进行对比，目标是达到 state-of-the-art（SOTA）精度。
- 对比方法：摘要未列出具体基线名称，仅笼统说明为“现有 PLM-based TSF 方法”。

### 4. 资源与算力
- 论文摘要**未提及任何算力信息**，如 GPU 型号、数量、训练时长等。
- 元数据中也没有相关说明，因此无法总结资源消耗情况。

### 5. 实验数量与充分性
- 实验数量：在 9 个数据集上进行了预测精度对比，并覆盖全量训练和少样本两种设置，属于中等规模实验。
- 充分性评估：
  - **优点**：多数据集、多场景验证，能较好说明方法的泛化性。
  - **不足**：摘要未报告消融实验、模型效率分析、不同 PLM 基座对比等细节，无法全面判断实验设计的完整性。
  - 由于缺乏具体基线和统计显著性说明，公平性需要查看论文全文才能评估。

### 6. 主要结论与发现
- CC-Time 在 9 个真实数据集上，在全量训练和少样本场景下均取得 **SOTA 预测精度**。
- 实验验证了**跨模型与跨模态学习**的有效性：合理利用 PLM 的文本/语言知识，并融合专门时序模型，能显著提升时间序列预测性能。
- 结论表明：仅靠 PLM 不够，但结合跨模态信息和传统时序模型可以更好地发挥 PLM 的序列建模能力。

### 7. 优点（方法或实验设计亮点）
- **创新视角**：系统化回答“PLM 能建模什么时序特征”和“是否只要 PLM 就够了”两个关键问题，具有研究价值。
- **跨模态设计**：引入文本描述作为辅助信息，拓展了时序预测中模态融合的思路。
- **跨模型融合**：自适应融合 PLM 与传统时间序列模型，兼顾两者优势，避免单一模型局限。
- 实验覆盖全量训练和少样本场景，有利于评估模型的适应性和实际应用潜力。

### 8. 不足与局限
- **信息不全**：摘要未给出数据集名称、基线方法、具体性能数值，难以独立复现或深入验证。
- **缺乏细节**：未提供模型架构图、公式、融合机制的具体设计，方法论描述偏高层。
- **计算成本**：未讨论引入 PLM 和跨模态文本生成带来的额外计算开销，实际部署可行性存疑。
- **文本依赖**：方法依赖对应的时间序列文本描述，在无文本标注或自动描述质量不佳的场景下效果可能受限。
- **实验深度**：未见消融实验、鲁棒性分析、不同 PLM 选择的影响、超参敏感性等，充分性有待加强。

（完）
