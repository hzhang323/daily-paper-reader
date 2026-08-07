---
title: Towards a Multimodal Foundation Model for Time Series Analysis
title_zh: 迈向多模态时间序列分析基础模型
authors: "Peng Chen, Siyuan Wang, Shiyan Hu, Xingjian Wu, Yang Shu, Zhongwen Rao, Meng Wang, Yijie Li, Bin Yang, Chenjuan Guo"
date: 2025-09-15
pdf: "https://openreview.net/pdf?id=dcfHcCAG3C"
tags: ["query:time-series"]
score: 9.0
evidence: 面向通用时间序列分析的多模态基础模型预训练
tldr: 针对现有时间序列基础模型仅依赖单模态预训练、缺乏互补模态信息的问题，本文率先探索多模态时间序列基础模型。作者构建了覆盖六个领域、包含时间序列、文本和图像的大规模多模态数据集MM-TS，并研究了异构模态的有效集成和跨模态、跨域泛化。相关工作为后续多模态时间序列建模提供了数据集和方法基础，有望显著提升时间序列理解的性能与鲁棒性。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 现有时序基础模型缺少多模态信息，难以充分利用文本图像等互补数据，性能受限。
method: 构建大规模多模态时序数据集MM-TS，覆盖六领域并集成时间序列、文本与图像，探索异构模态融合方案。
result: 数据集和模型在跨模态、跨领域泛化上展现出潜力，为多模态时序研究提供基准与基线。
conclusion: 多模态时序基础模型具有可行性，有望成为通用时序分析的重要方向。
---

## Abstract
Time series analysis supports a wide range of real-world applications. While existing time series foundation models primarily rely on large-scale unimodal pretraining, they lack complementary modalities to enhance time series understanding. Building multimodal foundation models is a natural next step, but it introduces key challenges: 1) the scarcity of large-scale and high-quality multimodal time series data; 2) how to effectively integrate heterogeneous modalities and enhance model generalization across both modalities and domains. To address these challenges, we take an early step toward multimodal foundation models for time series analysis. We first construct MM-TS, a large-scale multimodal dataset spanning time series, text, and image across six domains, with more than one billion time points. Then we propose HORAI, a frequency-enhanced multimodal foundation model. HORAI integrates two core components: a Frequency-guided Cross-Modality Encoder, which leverages the correspondence between modality-specific information and different frequency components of time series to effectively fuse multiple modalities, and a Time-Frequency Decoder, which incorporates frequency information into a MoE router to improve pattern discrimination and generalization. After pretraining on MM-TS, HORAI achieves state-of-the-art zero-shot performance on time series forecasting and anomaly detection tasks, demonstrating strong task versatility and generalization.

---

## 论文详细总结（自动生成）

# 中文总结：迈向多模态时间序列分析基础模型

## 1. 论文的核心问题与整体含义

- **研究动机**：时间序列分析广泛应用于真实世界场景，但现有时间序列基础模型主要依赖大规模单模态（仅时间序列）预训练，缺乏文本、图像等互补模态信息，限制了模型对时间序列的深层理解。
- **核心问题**：
  1. 大规模、高质量的多模态时间序列数据稀缺；
  2. 如何有效融合异构模态，并提升模型在跨模态、跨领域上的泛化能力。
- **整体意义**：本文是“多模态时间序列基础模型”方向的早期探索，旨在为通用时间序列分析建立数据与模型基础，具有前瞻性和推动性价值。

## 2. 论文提出的方法论

- **核心思想**：构建大规模多模态数据集，并设计一个能利用频域信息引导跨模态融合的基础模型，使模型不仅处理时间序列本身，还能引入文本和图像的互补信息。
- **数据集构建——MM-TS**：
  - 覆盖六个领域；
  - 包含时间序列、文本、图像三种模态；
  - 总规模超过 10 亿个时间点。
- **模型——HORAI**（频率增强的多模态基础模型）：
  - **频域引导的跨模态编码器（Frequency-guided Cross-Modality Encoder）**：利用模态特定信息与时间序列不同频率分量之间的对应关系，实现多模态的有效融合。
  - **时频解码器（Time-Frequency Decoder）**：将频域信息引入 MoE（Mixture-of-Experts）路由器，增强模式判别能力与泛化性能。
- 整体流程（文字说明）：输入时间序列、文本、图像 → 分别编码 → 经频域引导的跨模态融合编码器对齐与融合 → 在时频解码器中整合频域信息，通过 MoE 路由输出任务结果。论文未给出具体公式，但描述了两个核心组件的机制。

## 3. 实验设计

- **预训练数据**：使用自建的 MM-TS 数据集，跨度六个领域。
- **下游任务**：
  - 时间序列预测（forecasting）；
  - 异常检测（anomaly detection）。
- **评估模式**：零样本（zero-shot）性能测试，即直接在未见过的数据上测试，不进行微调。
- **对比方法**：论文未列出具体基线名称，但声称达到“state-of-the-art”零样本性能，推测对比了现有单模态时间序列基础模型（如 TimeGPT、TimesFM、PatchTST 等，但原文未明确）。

## 4. 资源与算力

- **论文未明确说明**使用的 GPU 型号、数量、训练时长或计算量等具体资源信息。
- 仅可推断模型为大规模预训练，且数据集超过 10 亿时间点，所需算力应较大，但原文未提供任何硬件细节。

## 5. 实验数量与充分性

- 论文只汇报了两个任务（预测、异常检测）的零样本结果，未给出具体实验数量。
- 未提及消融实验（如去掉频域引导或 MoE 后效果变化）。
- 未给出跨模态迁移的细化分析（如哪种模态贡献最大）。
- **充分性评价**：从已提供信息看，实验覆盖面较窄，仅以摘要形式概述，缺乏详细表格、误差条、不同领域分解等证据。作为 ICLR 投稿被拒，可能也与实验验证不足有关。因此，实验充分性存疑，公平性难以从摘要层面判断。

## 6. 论文的主要结论与发现

- 多模态时间序列基础模型具有可行性，能够通过引入文本和图像互补信息提升时间序列分析性能。
- 频域引导的跨模态融合和时频 MoE 解码器是有效设计方案。
- 在 MM-TS 上预训练的 HORAI 在零样本预测和异常检测上实现当前最优，展示了强大的任务通用性与泛化能力。
- 该工作为后续多模态时序研究提供了数据集与基线基础。

## 7. 优点

- **开创性**：率先系统探索多模态时间序列基础模型，填补该方向空白。
- **数据贡献**：构建了大规模、多领域、三模态（时间序列+文本+图像）数据集 MM-TS，规模超过 10 亿时间点，可作为后续研究的基准。
- **方法创新**：
  - 引入频域引导的跨模态编码，理论上可更有效地对齐异构模态；
  - 将频域信息融入 MoE 路由器，思路新颖，可提升模式判别能力。
- **通用性**：模型支持多任务（预测、异常检测），零样本性能表明具有较强泛化潜力。

## 8. 不足与局限

- **数据偏差风险**：MM-TS 覆盖六个领域，但领域多样性可能仍不足以代表全部真实场景，存在领域偏置。
- **实验验证不足**：摘要层面未展示详细结果，缺少与广泛基线的标准对比、消融研究和统计显著性检验，结论可靠性待验证。
- **可复现性差**：未公开预训练细节、超参数、硬件资源等，难以独立复现。
- **模型可解释性**：频域融合与 MoE 的具体收益缺乏可视化或分析，机制解释多停留在概念层面。
- **应用限制**：仅验证了预测和异常检测，未覆盖分类、插补等其他常见时序任务。
- **资源需求**：大规模多模态预训练可能带来高昂计算成本，但论文未讨论效率优化。

（完）
