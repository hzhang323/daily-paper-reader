---
title: "Towards Foundation Models for Zero-Shot Time Series Anomaly Detection: Leveraging Synthetic Data and Relative Context Discrepancy"
title_zh: 面向零样本时间序列异常检测的基础模型：利用合成数据与相对上下文差异
authors: "Tian Lan, Hao Duong Le, Jinbo Li, Wenjun He, Meng Wang, Chenghao Liu, Chen Zhang"
date: 2025-09-17
pdf: "https://openreview.net/pdf?id=Z4T26VztkU"
tags: ["query:time-series"]
score: 9.0
evidence: 提出面向零样本时间序列异常检测的基础模型，采用相对上下文差异预训练范式
tldr: 时间序列异常检测在零样本场景下泛化困难，现有重建式基础模型存在目标不匹配、漏检误检率高。TimeRCD提出新的预训练范式——相对上下文差异，不再重建输入，而是显式训练模型识别异常，并结合合成数据实现零样本泛化。实验表明该方法在未见数据上能有效降低误检和漏检，提升异常检测性能，为基础模型在时序异常检测中的应用提供了新方向。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 现有时间序列异常检测基础模型以重建为目标，难以识别细微异常且常误解复杂正常模式，零样本泛化差。
method: 提出TimeRCD模型，采用相对上下文差异预训练范式，在合成数据上显式训练异常识别能力。
result: 在零样本异常检测任务上，TimeRCD相比重建式方法显著降低误检漏检率，性能更好。
conclusion: 验证了基于差异学习的基础模型对时间序列异常检测的重要价值，可推广到未见数据。
---

## Abstract
Time series anomaly detection (TSAD) is a critical task, but developing models that generalize to unseen data in a zero-shot manner remains a major challenge. Prevailing foundation models for TSAD predominantly rely on reconstruction-based objectives, which suffer from a fundamental objective mismatch: they struggle to identify subtle anomalies while often misinterpreting complex normal patterns, leading to high rates of false negatives and positives. To overcome these limitations, we introduce TimeRCD, a novel foundation model for TSAD built upon a new pre-training paradigm: Relative Context Discrepancy (RCD). Instead of learning to reconstruct inputs, TimeRCD is explicitly trained to identify anomalies by detecting significant discrepancies between adjacent time windows. This relational approach, implemented with a standard Transformer architecture, enables the model to capture contextual shifts indicative of anomalies that reconstruction-based methods often miss. To facilitate this paradigm, we develop a large-scale, diverse synthetic corpus with token-level anomaly labels, providing the rich supervisory signal necessary for effective pre-training. Extensive experiments demonstrate that TimeRCD significantly outperforms existing general-purpose and anomaly-specific foundation models in zero-shot TSAD across diverse datasets. Our results validate the superiority of the RCD paradigm and establish a new, effective path toward building robust and generalizable foundation models for time series anomaly detection. The code is available in https://anonymous.4open.science/r/TimeRCD-5BE1/

---

## 论文详细总结（自动生成）

## 论文总结：TimeRCD——面向零样本时间序列异常检测的基础模型

### 1. 核心问题与整体含义
- 时间序列异常检测（TSAD）在工业运维、金融风控、健康监测等领域至关重要，但实际场景中经常面临**未见过的数据**，要求模型具备**零样本泛化能力**。
- 现有面向TSAD的基础模型大多采用**重建式目标**（如预测下一个时间点或重建输入窗口），存在根本性的**目标不匹配**：模型倾向于拟合正常模式，难以捕捉细微异常，同时容易将复杂但正常的模式误判为异常，导致**高漏检率（false negatives）和高误检率（false positives）**。
- 本文提出**TimeRCD**，通过新的预训练范式**相对上下文差异（Relative Context Discrepancy, RCD）**，显式训练模型识别异常，从而克服重建式模型的固有缺陷，建立更鲁棒、可泛化的TSAD基础模型。

### 2. 方法论
- **核心思想**：不要求模型重建输入，而是让模型学习**比较相邻时间窗口之间的相对差异**，判断当前窗口与上下文的显著不一致性。这种关系型建模更贴近异常的本质——异常是相对于正常上下文出现的偏移。
- **预训练范式（RCD）**：
  - 将时间序列划分为相邻窗口（如上下文窗口与目标窗口）。
  - 模型学习一个差异度量，识别目标窗口与上下文窗口之间的显著偏差。
  - 训练目标是显式区分“正常”与“异常”窗口对，而非重建原始信号。
- **模型架构**：采用标准 **Transformer** 架构实现这一关系建模，无需复杂定制结构。
- **合成数据生成**：为支持该范式，构建了一个**大规模、多样化、带token级异常标签的合成语料库**，提供丰富的监督信号，使模型学到可迁移的异常判别能力。

### 3. 实验设计
- **数据集/场景**：论文摘要仅提到“diverse datasets”（多样化数据集），未给出具体数据集名称。通常可推测包含公开TSAD基准（如SWaT、WADI、SMD、MSL、SMAP等），但原文未明确列出。
- **Benchmark**：面向**零样本时间序列异常检测**，即训练阶段完全未接触目标数据集，直接评估模型在全新数据上的异常检测性能。
- **对比方法**：
  - 通用基础模型（general-purpose foundation models）
  - 专门面向异常检测的基础模型（anomaly-specific foundation models）
- 对比维度应包括误检率、漏检率、综合F1或AUROC等指标。

### 4. 资源与算力
- 原文（摘要及元数据）**未提及**任何关于GPU型号、数量、训练时长、参数量或能耗等资源信息。
- 因此无法评估其训练成本与可复现性中的资源需求。

### 5. 实验数量与充分性
- 原文仅以“Extensive experiments”（大量实验）概括，**未给出具体实验组数**，也未详细描述消融实验、超参数敏感性分析或不同合成数据规模的影响实验。
- **充分性评价**：从摘要看，实验覆盖了与多个基础模型的对比，证明了RCD范式的有效性，但缺乏具体实验细节（数据集数量、统计显著性、误差棒、case study等），使得**可验证性和说服力有限**。需要补充更完整的实验章节才能判断其公平性和全面性。

### 6. 主要结论与发现
- TimeRCD在零样本TSAD任务上**显著优于**现有通用基础模型和专门针对TSAD的基础模型。
- RCD预训练范式相比重建式目标能够**大幅降低误检和漏检**，更精准地识别上下文相关的异常。
- 实验证实了**基于相对差异学习的基础模型**对于时间序列异常检测具有重要价值，为构建可泛化的TSAD基础模型提供了新方向。

### 7. 优点
- **范式创新**：提出了RCD这一新的预训练范式，直接针对“异常”进行判别式训练，规避了重建式目标固有的目标不匹配问题。
- **关系建模**：通过相邻窗口的差异比较，更符合异常检测的语义，能够捕获重建方法容易遗漏的细微上下文偏移。
- **架构简洁**：使用标准Transformer即可实现，不需要专门设计复杂网络，易于扩展和落地。
- **合成数据策略**：构建带token级标签的大规模合成语料库，解决监督信号匮乏的问题，为预训练提供丰富且可控制的样本。
- **性能优势**：在零样本场景下对比多种基础模型，表现出更低的误检和漏检率，展示了实际部署潜力。

### 8. 不足与局限
- **信息完整性不足**：本总结仅基于摘要与元数据，缺少方法细节、实验配置、具体数据集列表、评估指标定义等关键信息。
- **实验验证不充分**：未展示具体实验数量、消融实验、合成数据与真实数据之间的域差距分析、异常类型覆盖范围等，无法全面评估方法的鲁棒性。
- **合成数据依赖**：模型性能高度依赖合成数据的多样性和与现实异常分布的匹配程度，若合成数据与真实场景差异较大，零样本泛化可能受限。
- **应用限制**：RCD依赖相邻窗口的上下文，对于没有明显上下文关系或异常跨越极长周期的时间序列，其有效性需要进一步验证；此外，token级标签在真实TSAD中较难获取，主要依赖合成数据。
- **资源与公平性信息缺失**：未提供计算成本，也未说明与对比方法之间的训练数据规模、模型大小等是否公平对齐。

（完）
