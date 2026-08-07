---
title: "TempoPFN: Synthetic Pre-training of Linear RNNs for Zero-shot Time Series Forecasting"
title_zh: TempoPFN：线性RNN的合成预训练用于零样本时间序列预测
authors: "Vladyslav Moroshan, Julien Siems, Arber Zela, Timur Carstensen, Frank Hutter"
date: 2025-09-19
pdf: "https://openreview.net/pdf?id=WcEbBJeqQ0"
tags: ["query:time-series"]
score: 9.0
evidence: 基于合成数据预训练线性RNN实现零样本时序预测
tldr: 针对零样本长时程预测效率低、已有全合成方法效果不佳等问题，本文提出TempoPFN，一种仅基于合成数据预训练的线性RNN时序基础模型。模型采用GatedDeltaProduct架构和状态编织，实现了跨序列长度的完全并行化训练，无需窗口化或摘要技术即可保持时序状态追踪。综合合成数据流水线统一了随机微分方程、高斯过程等多样生成器，使得零样本长期预测更具效率和可复现性。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 现有零样本时序基础模型长时程预测效率低，全合成方法性能不足。
method: 基于线性RNN和GatedDeltaProduct架构，仅用合成数据预训练，并实现全并行训练。
result: 在挑战性基准上展现了高效、可复现的零样本长期预测能力。
conclusion: 全合成预训练的线性RNN是零样本时序预测的强有力选择。
---

## Abstract
Foundation models for zero-shot time series forecasting face challenges in efficient long-horizon prediction and reproducibility, with existing synthetic-only approaches underperforming on challenging benchmarks. This paper presents TempoPFN, a univariate time series foundation model based on linear Recurrent Neural Networks (RNNs) pre-trained exclusively on synthetic data. The model uses a GatedDeltaProduct architecture with state-weaving for fully parallelizable training across sequence lengths, eliminating the need for windowing or summarization techniques while maintaining robust temporal state-tracking. Our comprehensive synthetic data pipeline unifies diverse generators including stochastic differential equations, Gaussian processes, and audio synthesis with novel augmentations such as time-varying TSMixup, differentiation, and integration. In zero-shot evaluations on the Gift-Eval benchmark, TempoPFN achieves state-of-the-art performance, matching models trained on real-world data while being significantly more efficient than existing baselines. We open-source our complete data generation pipeline and training code.

---

## 论文详细总结（自动生成）

# TempoPFN 论文中文总结

## 1. 核心问题与整体含义

- **研究背景**：零样本时间序列预测的基础模型在长时程预测中面临效率低、可复现性差的问题；已有的仅使用合成数据的方案在挑战性基准上表现不佳。
- **核心问题**：能否设计一种完全基于合成数据预训练、同时具备高效率与强零样本泛化能力的时序基础模型？
- **整体含义**：本文提出 **TempoPFN**，一种基于线性 RNN、仅用合成数据预训练的单变量时序基础模型。它在零样本评估中达到当前最优水平，能够匹配基于真实数据训练的模型，且显著提升效率，为时序基础模型提供了更高效、可复现的替代路径。

## 2. 方法论

- **核心思想**：利用线性 RNN 的高效序列建模能力，通过大规模、多样化的合成数据预训练，从而避免对真实数据集的依赖，同时获得可迁移的时序表示。
- **关键架构**：
  - 采用 **GatedDeltaProduct** 架构，作为线性 RNN 的核心模块。
  - 引入 **状态编织（state-weaving）** 机制，使模型能够跨不同序列长度进行**完全并行化训练**。
  - 无需窗口化（windowing）或摘要（summarization）技术，即可保持稳健的时序状态追踪。
- **合成数据流水线**：
  - 统一多种生成器：随机微分方程（SDE）、高斯过程（GP）、音频合成等。
  - 加入新增强化方法：时变 TSMixup、微分、积分等。
- **训练方式**：仅使用合成数据预训练，不接触任何真实时序数据。
- 注：原文提供内容未包含具体公式或算法伪代码，此处以文字概述。

## 3. 实验设计

- **基准数据集**：论文在 **Gift-Eval** 基准上进行零样本评测。
- **评估场景**：零样本（zero-shot）长期预测，评估模型对未见数据的泛化能力。
- **对比方法**：与现有零样本时序预测方法对比，包括基于真实数据训练的模型；摘要未列出具体基线名称。
- **主要结果**：
  - TempoPFN 在 Gift-Eval 上达到 **state-of-the-art** 性能。
  - 效果与使用真实数据训练的模型相当，但效率明显高于已有基线。
- 注：由于仅提供摘要级信息，无法获得具体对比方法列表、MSE/MAE 等详细数值。

## 4. 资源与算力

- **论文提供内容中未明确说明**使用的 GPU 型号、数量、训练时长、参数量等算力信息。
- 仅能推断其优势在于**高效性**——线性 RNN 与完全并行化训练降低了计算成本，但具体数值无从得知。

## 5. 实验数量与充分性

- 从现有摘要看，论文主要进行了 **Gift-Eval 单一基准**上的零样本评估。
- **未提及**消融实验、多数据集交叉验证、不同预测长度分析等细节。
- **充分性评价**：
  - 优点：Gift-Eval 是挑战性基准，SOTA 结果能说明模型核心能力。
  - 不足：单一基准难以全面验证模型在多样时间序列领域的泛化性；缺少对合成数据流水线各组件的消融分析，也缺少与更多真实数据基础模型的对比细节。
  - 另外，该论文在来源标注中为 **ICLR-2026-Rejected-Public**，说明其可能仍存在评审指出的研究缺点。

## 6. 主要结论与发现

- 完全基于合成数据预训练的线性 RNN，可以成为零样本时序预测的**强有力选择**。
- TempoPFN 在零样本长期预测上达到 SOTA，**性能可与使用真实数据训练的模型匹敌**，同时计算效率更高。
- 多样化的合成数据生成器与增强方法，是模型泛化能力的重要支撑。
- 研究强调**可复现性**，并将完整数据生成流水线与训练代码开源。

## 7. 优点

- **纯合成预训练**：摆脱对真实数据的依赖，数据获取成本低、可无限生成、可复现性强。
- **架构高效**：线性 RNN + GatedDeltaProduct + 状态编织，实现跨序列长度的全并行训练，无需窗口化/摘要，状态建模更完整。
- **数据流水线设计新颖**：统一 SDE、GP、音频合成等多种生成器，并引入时变 TSMixup、微分/积分等增强，显著提高合成数据多样性。
- **结果有说服力**：在挑战性基准上达到 SOTA，且优于已有纯合成方法，证明合成数据预训练的潜力。
- **开源贡献**：公开数据流水线与代码，推动社区复现与后续研究。

## 8. 不足与局限

- **模型适用范围**：目前仅针对**单变量**时间序列，未覆盖多变量场景，应用范围受限。
- **实验覆盖不足**：仅报告 Gift-Eval 一个基准，缺少对更多领域（如金融、医疗、能源）和不同预测长度的系统性验证。
- **消融分析缺失**：未说明合成数据流水线各组件（如不同生成器、增强策略、状态编织）对性能的单独贡献。
- **对比细节有限**：摘要未列出具体基线模型与数值，难以全面评估相对优势。
- **算力信息缺失**：没有提供训练成本、模型规模等量化数据，影响对“高效”程度的客观判断。
- **评审状态**：论文在 ICLR 2026 被拒，可能仍存在理论或实验上的不足，需谨慎看待其声称的全面优势。

（完）
