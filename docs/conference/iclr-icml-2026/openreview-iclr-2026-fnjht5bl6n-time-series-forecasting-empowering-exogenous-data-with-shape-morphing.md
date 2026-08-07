---
title: "Time Series Forecasting: Empowering Exogenous Data with Shape Morphing"
title_zh: 时间序列预测：利用形状变形增强外生数据
authors: "Ramón Christen, Renan de Luca Avila, Robin Matter, Oswaldo L V Costa, Edy Portmann"
date: 2025-09-16
pdf: "https://openreview.net/pdf?id=FNJhT5bL6n"
tags: ["query:time-series"]
score: 9.0
evidence: 利用形状变形捕捉外生变量的时间显著性以改进预测
tldr: 外生变量对目标序列的预测价值往往随时间变化，仅在特定区间内有效，而现有跨通道Transformer未能充分利用这种时间显著性。提出一种形状变形方法，对外生输入进行形态变换以对齐其有效时段，在多元输入单目标预测任务中提升预测表现。实验表明该方法优于简单线性模型与通道依赖Transformer。该工作为带外生变量的时间序列预测提供了新思路。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 外生变量具有时间显著性，仅在某些区间有效，现有模型难以捕捉这种时变相关性，导致预测受限。
method: 提出形状变形方法，对外生变量进行形态变换以匹配其时间显著性，增强目标序列预测的信息利用。
result: 在带外生变量的时间序列预测任务中，该方法相比通道独立线性模型与Transformer基线取得更优性能。
conclusion: 形状变形能有效利用外生变量的时变信息，为多通道预测提供通用且高效的手段。
---

## Abstract
Time series forecasting often relies on patterns extracted from historical target dynamics, yet exogenous variables can provide valuable additional signal. Importantly, such variables are typically informative only in specific intervals and irrelevant elsewhere. We refer to this phenomenon as temporal saliency of exogenous variables, i.e., the time-varying relevance of external inputs for predicting the target series. In this paper, we tackle the "forecasting with exogenous variables" problem, where the model receives multiple input channels but predicts only one target variable. Recent studies have shown that channel-dependent Transformer architectures might be outperformed by simple channel-independent linear models, suggesting that current cross-attention mechanisms suffer to fully profit from exogenous information. To address this, we propose a morphing framework that adaptively reshapes exogenous time series before forecasting. For each channel and time step, a morphing function computes a ratio from the local relationship between the exogenous input and the target series and amplifies useful intervals accordingly. We instantiate morphing functions with interpretable information-theoretic metrics such as correlation, covariance, entropy, and mutual information, and evaluate them in ablation studies for long-horizon forecasting and state-of-the-art Transformer-based architectures. Results show that morphing is capable to yield significant improvements in certain dataset–model combinations. These findings highlight morphing as a simple yet effective way to enhance the utility of exogenous information and close part of the performance gap between linear and Transformer-based forecasting methods.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 核心问题与整体含义（研究动机和背景）

- **研究背景**：时间序列预测通常依赖目标变量自身的历史动态模式，但外生变量（exogenous variables）往往能为预测提供有价值的补充信号。
- **核心现象**：外生变量并非在所有时间点都有用，而是仅在特定时间区间内具有信息量，在其他区间则与目标变量无关。论文将这一现象称为**外生变量的时间显著性（temporal saliency）**，即外部输入对预测目标序列的时变相关性。
- **关键矛盾**：现有研究显示，通道依赖（channel-dependent）的 Transformer 架构在多元输入单目标预测任务中，性能可能反而不如简单的通道独立（channel-independent）线性模型。这表明当前的交叉注意力机制未能充分提取和利用外生信息。
- **研究意义**：如何有效利用外生变量的时变显著性，是提升时间序列预测性能的关键挑战，也是连接线性模型与复杂 Transformer 模型性能差距的重要切入点。

## 2. 论文提出的方法论

- **核心思想**：提出一种**形状变形（morphing）框架**，在预测之前对外生时间序列进行自适应形状重塑，以放大外生变量中真正有用的时间区间，抑制无关区间的干扰。
- **实现机制**：
  - 对于每一个输入通道和每一个时间步，定义一个**变形函数（morphing function）**。
  - 该函数通过计算外生输入与目标序列之间的**局部关系**（local relationship），得到一个加权比例（ratio）。
  - 据此对外生输入进行缩放或加权，从而**放大有效区间**、压制无效区间，使得外生信息与目标序列的时间显著性对齐。
- **可解释性设计**：
  - 变形函数使用具有信息论可解释性的指标进行实例化，包括：
    - 相关（correlation）
    - 协方差（covariance）
    - 熵（entropy）
    - 互信息（mutual information）
  - 这些指标用于量化外生变量与目标序列之间的时变依赖强度，从而驱动形态变换。
- **适用范围**：该方法可以作为独立模块嵌入到不同的预测架构之中，文中将其与先进的 Transformer 架构结合进行验证。

## 3. 实验设计

- **任务设定**：多元输入通道、单一目标变量预测，即“带外生变量的时间序列预测（forecasting with exogenous variables）”。
- **实验场景**：长时程预测（long-horizon forecasting）场景。
- **对比方法**：
  - 简单通道独立线性模型（channel-independent linear model）
  - 通道依赖 Transformer（channel-dependent Transformer）
  - 加入形状变形模块的 Transformer 架构
- **模块评估**：对多种变形函数实例（相关性、协方差、熵、互信息）进行**消融研究（ablation studies）**，以比较不同信息论指标的相对效果。
- **Benchmark**：摘要中未明确列出具体数据集名称，仅提及“certain dataset–model combinations”，说明在多个数据集与模型组合上进行了验证。

## 4. 资源与算力

- **文中未明确说明**：论文摘要和所提供的元数据中均未提及使用的 GPU 型号、GPU 数量、训练时长、参数量或总体算力开销。
- 因此无法评估其计算资源需求和训练成本，这一点属于信息缺失。

## 5. 实验数量与充分性

- **实验规模**：
  - 研究包含多组消融实验，覆盖 4 种不同的变形函数实现（相关性、协方差、熵、互信息）。
  - 实验跨越多个数据集和多种模型架构组合，并应用于长时程预测场景。
- **充分性评价**：
  - **优点**：消融设计覆盖了多种信息论指标，有助于理解不同变形函数的贡献差异；跨数据集-模型组合的评估增强了结论的广度。
  - **不足**：
    - 摘要中未给出数据集的具体名称、数量及规模，难以准确判断实验覆盖的领域广度和任务多样性。
    - 改进仅在“特定的数据集-模型组合”中出现，说明优势并非普遍一致，泛化性存疑。
    - 未报告统计显著性检验、方差或多次运行的结果，无法判断改进的稳定性。
    - 缺少与更多类型的基线（如其他通道依赖模型、非线性方法）的对比，公平性难以全面评估。

## 6. 主要结论与发现

- 形状变形框架能够在某些数据集与模型组合中带来**显著的预测性能提升**。
- 变形方法有效增强了外生变量信息的利用效率，说明当前交叉注意力机制确实存在对外生时间显著性利用不足的问题。
- 该方法能够部分弥合**线性模型与基于 Transformer 的预测方法之间的性能差距**。
- 整体而言，形状变形是一种**简单而有效**的途径，可以提升外生信息在时间序列预测中的实用性。

## 7. 优点

- **方法简单直观**：变形函数以局部关系为基础，概念清晰，易于实现和嵌入现有架构。
- **可解释性强**：使用相关性、协方差、熵、互信息等经典信息论指标，使得模型行为具有可解释性，便于分析外生变量的实际贡献。
- **通用性好**：作为一种模块化的预处理/特征增强手段，可适配多种预测主干网络，而不局限于特定架构。
- **问题定位准确**：聚焦于外生变量时间显著性这一此前较少被明确讨论的问题，切中现有交叉注意力机制的短板。
- **计算开销可能较低**：基于统计指标而非额外引入大量可学习参数，理论上具有较高计算效率（尽管文中未提供具体数据）。

## 8. 不足与局限

- **改进非普适**：性能提升仅在特定数据集-模型组合中出现，说明方法存在适用范围限制，尚未表现出普遍一致性。
- **实验细节不足**：摘要中未列出具体数据集、数据规模、任务类型、评估指标、实验重复次数等关键信息，降低了研究的可复现性和说服力。
- **算力信息缺失**：未提供任何关于训练资源、硬件配置和运行时间的信息，不利于实际应用中的成本评估。
- **基线覆盖有限**：主要与线性模型和 Transformer 对比，缺乏与其他先进预测方法（如 N-BEATS、N-HiTS、PatchTST、iTransformer 等）的比较。
- **变形函数的局限**：所采用的信息论指标主要捕捉线性或静态依赖关系，对于非线性、滞后效应或高维交互可能表达能力不足。
- **任务范围窄**：仅处理多元输入单目标预测，未扩展到多目标联合预测或更一般的多元预测场景。

（完）
