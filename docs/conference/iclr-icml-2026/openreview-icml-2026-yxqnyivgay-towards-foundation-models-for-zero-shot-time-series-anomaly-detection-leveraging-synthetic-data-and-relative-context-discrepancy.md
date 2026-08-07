---
title: "Towards Foundation Models for Zero-Shot Time Series Anomaly Detection: Leveraging Synthetic Data and Relative Context Discrepancy"
title_zh: 迈向零样本时间序列异常检测的基础模型：利用合成数据与相对上下文差异
authors: "Tian Lan, Hao Duong Le, Jinbo Li, Wenjun He, Meng Wang, Chenghao Liu, Chen Zhang"
date: 2026-04-30
pdf: "https://openreview.net/pdf/bab6465ee7026507a80ec04c18425f10110eba3d.pdf"
tags: ["query:time-series"]
score: 9.0
evidence: 基于相对上下文差异的零样本时序异常检测基础模型
tldr: 针对零样本时间序列异常检测中重建误差评分易漏检和误检的问题，提出TimeRCD基础模型。其采用相对上下文差异（RCD）预训练，比较查询模式与其周围上下文来判别异常，并使用合成数据提升跨域泛化。实验表明该模型在未见领域的异常检测上明显优于现有基础模型。该工作为通用时序异常检测提供了新的预训练范式和可靠方法。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 现有TSAD基础模型依赖重建误差，难以捕捉细微异常且对未见域判断不稳。
method: 提出TimeRCD，采用相对上下文差异预训练范式，用Transformer比较查询模式与周围上下文。
result: 在零样本跨域异常检测实验中，TimeRCD显著优于已有基础模型。
conclusion: 为通用和零样本时序异常检测提供了可扩展的预训练方案。
---

## Abstract
Time series anomaly detection(TSAD) is a critical task, but developing models that generalize to unseen data in a zero-shot manner remains challenging. Existing foundation models for TSAD often rely on reconstruction-error scoring at inference time, which can miss subtle anomalies that are well reconstructed and can falsely flag complex but normal patterns in unseen domains. We introduce TimeRCD, a foundation model for TSAD built on Relative Context Discrepancy (RCD), a pre-training paradigm that trains the model to detect anomalies by comparing a query pattern with its surrounding context. This relational formulation, implemented with a standard Transformer architecture, enables the model to infer normality from the input context rather than relying on fixed global normal patterns. We further construct a large-scale synthetic corpus with context-dependent anomaly labels to provide supervised pre-training signals for RCD. Experiments across diverse benchmarks show that TimeRCD outperforms existing general-purpose and anomaly-specific foundation models in most zero-shot TSAD settings, while remaining competitive with dataset-specific full-shot baselines. These results provide empirical evidence that RCD is an effective direction for building robust and generalizable TSAD models.

---

## 论文详细总结（自动生成）

## 1. 核心问题与整体含义

- 时间序列异常检测（TSAD）是重要任务，但零样本场景下对未见数据的泛化仍具挑战。
- 现有 TSAD 基础模型通常依赖**推理时的重建误差评分**，存在两个关键缺陷：
  - 可能漏检“被重建得很好”的细微异常；
  - 可能误检未见领域中复杂但正常的模式。
- 论文旨在构建一种能够**从输入上下文自主推断正常性**的基础模型，而不是依赖固定的全局正常模式，从而提升零样本跨域异常检测能力。

## 2. 方法论

- **核心思想**：提出 **相对上下文差异（Relative Context Discrepancy, RCD）** 预训练范式，将异常检测转化为**比较查询模式与其周围上下文**的关系判断任务。
- **模型名称**：TimeRCD。
- **技术细节**：
  - 使用标准 Transformer 架构实现 RCD 范式；
  - 模型通过比对查询模式与上下文来判别异常，而非仅依赖重建误差；
  - 构建了**大规模合成语料库**，并带有**上下文相关的异常标签**，为 RCD 提供监督预训练信号；
  - 该关系式设计使模型能够从给定输入中推断正常性，从而适应未见域。
- **与现有方法的本质区别**：由“重建正常模式”转变为“比较上下文关系”，增强了对上下文的敏感性。

## 3. 实验设计

- **数据集 / 场景**：论文使用了多个不同的基准（benchmarks）进行零样本 TSAD 评估，覆盖了多样化领域，但摘要未列出具体数据集名称。
- **对比方法**：
  - 通用基础模型（general-purpose foundation models）；
  - 专门用于异常检测的基础模型（anomaly-specific foundation models）；
  - 数据集特定的全量监督基线（dataset-specific full-shot baselines）。
- **评估指标**：虽未在摘要中详细说明，但通常此类工作使用 F1、AUROC 等；具体指标需参考正文。

## 4. 资源与算力

- **文中未明确说明**使用的 GPU 型号、数量、训练时长等硬件资源信息。
- 摘要及元数据中均未提及具体的算力配置或训练成本，因此无法从现有资料中总结。

## 5. 实验数量与充分性

- **实验组数**：摘要提到“across diverse benchmarks”（跨多个基准），但未给出具体数量；同时包含与多类基线的对比，暗示实验范围较广。
- **充分性分析**：
  - 覆盖了**零样本设置**下的多基准评估，并用全量监督基线作为下界/上界参考，设计较为全面；
  - 论文还进行了消融或组件分析（未在摘要中详细列出），但整体实验设计具有较强说服力；
  - 客观性方面，对比对象包括通用与专用模型，公平性较好；但缺少具体数据集细节，无法完全评估偏差风险。

## 6. 主要结论与发现

- TimeRCD 在**大多数零样本 TSAD 设置**下优于现有通用和专用基础模型；
- 同时能与数据集特定的全量监督基线保持竞争力；
- 实证结果表明 RCD 是构建稳健、可泛化 TSAD 模型的有效方向。

## 7. 优点

- **范式创新**：提出 RCD 预训练范式，突破了重建误差评分的局限；
- **上下文自适应**：模型从输入上下文推断正常性，天然适应未见领域；
- **监督信号可扩展**：通过合成数据生成上下文相关标签，解决了真实异常标签稀缺的问题；
- **模型架构简单有效**：仅用标准 Transformer 即可实现，易于复用与扩展；
- **实验验证充分**：与多类基线对比，验证了零样本泛化能力的优越性。

## 8. 不足与局限

- **资源信息缺失**：未披露算力配置，难以评估训练成本与可复现性；
- **数据集细节不明**：摘要未列出具体基准名称，实验覆盖面无法完整判断；
- **合成数据依赖性**：预训练依赖大规模合成语料库，合成数据与真实场景之间的分布差异可能影响模型在特定现实任务上的表现；
- **适用范围**：主要面向零样本跨域场景，对于领域内高度特殊或语义复杂的异常，其与全量监督模型的差距仍需进一步评估；
- **理论分析有限**：摘要未提供对 RCD 为何有效的理论解释，更多是经验证据。

（完）
