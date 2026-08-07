---
title: "TimeSqueeze: Dynamic Patching for Efficient Time Series Forecasting"
title_zh: TimeSqueeze：用于高效时间序列预测的动态分块
authors: "Sravan Kumar Ankireddy, Nikita Seleznev, Nam H Nguyen, Yulun Wu, Senthil Kumar, Furong Huang, C. Bayan Bruss"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=rbJWsCoGm4"
tags: ["query:time-series"]
score: 9.0
evidence: 提出用于未来值预测的动态分块高效时间序列预测方法
tldr: 本文针对时间序列预测中Transformer计算复杂度随序列长度二次增长的问题，提出TimeSqueeze混合预测架构。该架构通过动态分块结合逐点嵌入与分块嵌入，既降低计算开销又保留关键高频时间细节。实验结果表明，TimeSqueeze在多个预测任务上取得有竞争力的精度，同时显著提升长序列处理效率，为大规模时间序列预测提供了高效的解决方案。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 现有时间序列预测模型采用Transformer架构，序列长度带来的二次复杂度迫使模型在高频信息保留与长序列效率之间权衡。
method: 提出混合预测架构TimeSqueeze，结合逐点嵌入与分块嵌入的优势，实现动态分块以减少序列长度同时保留关键时间细节。
result: 实验表明TimeSqueeze在保持高精度预测的同时显著提升效率，优于现有基线。
conclusion: TimeSqueeze为大规模时间序列预测提供了一种兼顾效率与精度的新架构。
---

## Abstract
Recent progress in time series forecasting has produced large foundation models with strong generalization across domains. However, many of these models rely on transformer backbones, making their effectiveness constrained by the cost of processing the input context. The quadratic computational complexity with respect to sequence length imposes a fundamental trade-off on existing designs: they must either preserve high-frequency information using point-wise embeddings, which is computationally expensive for long sequences, or employ patch-based embeddings to reduce sequence length at the risk of discarding critical temporal details. To overcome this limitation, we present TimeSqueeze, a hybrid forecasting architecture that combines the strengths of both point and patch embeddings through dynamic time series compression. TimeSqueeze introduces a novel two-stage hybrid representation: (1) a lightweight state-space encoder processes the full-resolution time series with point-wise embeddings to extract fine-grained temporal features, and (2) an adaptive patching module intelligently prunes these features using variable-sized patches, assigning smaller patches to information-rich regions and larger patches to redundant segments. This hybrid approach yields a variable-resolution representation that preserves critical temporal details while reducing computational overhead. By retaining the fidelity of point embeddings and the efficiency of patch embeddings, the resulting compressed sequence enables the Transformer backbone to substantially reduce the input length without sacrificing forecasting accuracy. Extensive experiments demonstrate that TimeSqueeze achieves state-of-the-art forecasting performance while delivering substantial computational advantages, including up to $8\times$ improvement in pretraining data efficiency and up to $20\times$ reduction in pretraining time compared to equivalent point-embedding models.

---

## 论文详细总结（自动生成）

# TimeSqueeze：用于高效时间序列预测的动态分块

## 1. 论文的核心问题与整体含义

### 研究背景
- 近年来，时间序列预测领域涌现出大规模基础模型（foundation models），展现出跨领域的强大泛化能力。
- 然而，这些模型大多依赖 Transformer 作为骨干网络，其有效性受限于处理输入上下文的计算成本。

### 核心问题
- **二次复杂度困境**：Transformer 的注意力机制计算复杂度随序列长度呈二次增长，给现有模型设计带来根本性权衡：
  - **逐点嵌入（point-wise embeddings）**：能保留高频细粒度信息，但对长序列计算开销过大。
  - **分块嵌入（patch-based embeddings）**：可缩短序列长度以提高效率，但面临丢弃关键时间细节的风险。

### 研究意义
- 如何在**保留关键高频时间信息**的同时**显著降低计算开销**，是构建高效且高精度时间序列预测模型的关键挑战。
- 现有设计被迫在“信息保真度”与“计算效率”之间做出取舍，缺乏兼顾两者的方案。

## 2. 论文提出的方法论

### 核心思想
论文提出 **TimeSqueeze**——一种**混合预测架构**，通过**动态时间序列压缩**结合逐点嵌入与分块嵌入的优势，在高频信息保真与计算效率之间取得平衡。

### 关键技术创新：两阶段混合表示

**阶段一：轻量级状态空间编码器**
- 使用**逐点嵌入**处理全分辨率时间序列
- 提取细粒度的时间特征，确保高频细节不丢失
- 采用状态空间模型（State-Space Model）实现高效编码

**阶段二：自适应分块模块**
- 智能剪枝已提取的特征
- 采用**可变大小的分块**策略：
  - 对信息丰富区域分配**较小分块**（更高分辨率）
  - 对冗余片段分配**较大分块**（更低分辨率）
- 形成**可变分辨率表示**，在保留关键细节的同时减少计算开销

### 架构优势
- **保留了逐点嵌入的信息保真度**（信息维度）
- **获得了分块嵌入的计算效率**（效率维度）
- 压缩后的序列允许 Transformer 骨干大幅缩短输入长度，**不牺牲预测精度**

## 3. 实验设计

### 数据集与基准
- 论文未在提取文本中明确列出具体使用的数据集名称（如 ETT、Electricity、Traffic 等），但从摘要的表述看，实验覆盖了时间序列预测的多个标准任务场景。

### 对比方法
- 与现有时间序列预测基线方法进行了对比，涵盖逐点嵌入模型和分块嵌入模型（具体基线名称未在提取文本中列出）。

### 主要评测指标
- 预测精度：与现有基线保持同等或更优水平
- 预训练数据效率：相比同等逐点嵌入模型最高提升 **8 倍**
- 预训练时间：相比同等逐点嵌入模型最高减少 **20 倍**

## 4. 资源与算力

- **论文提取文本中未明确说明**所使用的 GPU 型号、数量及具体训练时长。
- 仅提供了相对效率指标：与同等逐点嵌入模型相比，预训练时间最高减少 20 倍。
- 如需更详细的算力配置信息，需要查阅论文全文中的实验设置部分。

## 5. 实验数量与充分性

### 实验覆盖范围
- 从摘要来看，实验涵盖多个时间序列预测任务和多个数据集，并包含与基线的系统性对比。
- 报告了**预训练数据效率**和**预训练时间**两个维度的效率评估，实验维度较全面。

### 充分性评估
- **充分性**：实验设计覆盖了精度与效率两个关键评估维度，对比对象包括逐点嵌入模型（验证效率提升）和分块嵌入模型（验证精度保持），设计较为合理。
- **客观性**：由于提取文本中未提供详细的实验表格、误差棒、消融实验细节等信息，无法完全评估实验统计显著性和公平性。
- **潜在不足**：缺少关于动态分块策略本身的消融研究信息，以及不同压缩率下的性能权衡分析。

## 6. 论文的主要结论与发现

1. **动态分块策略有效**：TimeSqueeze 通过信息感知的分块策略，在保留关键时间细节的同时显著缩短序列长度，验证了“智能压缩优于均匀压缩”的假设。
2. **混合架构可行**：将逐点嵌入与分块嵌入结合，可以同时获得两者的优势，打破传统设计中的二元对立。
3. **效率提升显著**：相比同等逐点嵌入模型，预训练数据效率最高提升 **8 倍**，预训练时间最高减少 **20 倍**。
4. **精度有竞争力**：在保持高精度预测的同时实现效率提升，达到或超越现有基线的预测性能。

## 7. 优点

### 方法设计亮点
- **思路新颖**：将“动态分辨率”理念引入时间序列分块设计，借鉴了人类视觉注意力机制（信息密集区域高分辨率）的思路。
- **结构优雅**：两阶段设计巧妙分工——状态空间编码器负责特征提取，自适应分块负责信息压缩，模块间耦合清晰。
- **通用性强**：作为架构创新，可适配不同的 Transformer 骨干模型，具有较好的可迁移性。
- **直击痛点**：精准解决 Transformer 在时间序列上的二次复杂度问题，具有明确的实际应用价值。

### 实验设计亮点
- **双维度评估**：同时评估精度和效率，特别是引入了预训练阶段的数据效率和时间效率指标，评估角度较为全面。
- **与传统基线对比**：同时对比逐点嵌入和分块嵌入两类基线，验证了混合方法的优势来源。

## 8. 不足与局限

### 实验覆盖局限
- **数据集信息不明确**：提取文本中未列出具体数据集，无法判断是否覆盖了足够多样的领域（如金融、医疗、能源等）。
- **缺乏消融实验细节**：未展示对不同分块策略、压缩率、状态空间编码器配置等关键因素的消融分析。

### 偏差风险
- **基线选择不明确**：未列出具体对比方法，无法判断是否与最强基线（如 PatchTST、iTransformer 等）进行了对比。
- **统计显著性未报告**：缺少多次运行的方差、置信区间等信息。

### 应用限制
- **面向预训练场景**：效率优势主要体现在预训练阶段，对推理阶段的收益需要进一步说明。
- **额外开销**：动态分块模块本身引入的计算和内存开销未在提取文本中讨论。
- **超参数敏感性**：分块大小范围、信息丰富度判定阈值等超参数对效果的影响有待验证。
- **信息丰富度判定的可靠性**：如何准确判断“哪些区域信息丰富”是动态分块的核心，其鲁棒性需要进一步检验。
- **未见未来展望**：摘要中未讨论方法的局限性和未来改进方向。

---

*注：以上分析基于论文摘要及元数据信息，部分细节（如具体数据集、基线方法、超参数设置等）需要查阅论文全文以获取更全面的信息。*

（完）
