---
title: "Filter before Plug: One-for-All Framework for Covariate-Aware Forecasting with Time Series Foundation Models"
title_zh: 先滤后插：基于时间序列基础模型的外生变量感知预测通用框架
authors: "Yuxuan Chen, Tao Luo, Lingfeng Zhang, Chengxiang Wang, Feng Qian, Zhijun Yu"
date: 2025-09-19
pdf: "https://openreview.net/pdf?id=1O2A5TnFWl"
tags: ["query:time-series"]
score: 9.0
evidence: 基于时间序列基础模型的外生变量感知预测
tldr: 针对时间序列基础模型忽略外生协变量且现有插件模块缺乏通用性的问题，本文提出FLUG框架，设计基于Hurst指数引导的内生序列滤波器，将外生成分与内生序列分离后再输入基础模型。该框架为One-for-All设计，可与多种基础模型灵活结合。实验表明，FLUG在多个真实数据集上显著提升了协变量感知时间序列预测的精度，展示了通用插件式增强的有效性。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 现有时间序列基础模型忽略外生协变量，而现有插件模块依赖特定架构，缺乏通用性。
method: 提出FLUG通用框架，用Hurst指数引导的内生序列滤波器分离外生成分，让基础模型专注内生依赖。
result: 在多个数据集上验证了该框架与多种基础模型耦合时均能提升协变量感知预测性能。
conclusion: 独立训练模块与基础模型组合可高效处理含外生变量的预测任务。
---

## Abstract
Time series forecasting plays a critical role in numerous real-world applications. Recent advances in Time Series Foundation Models (TSFMs) have achieved strong performance by modeling historical dependencies; however, they frequently neglect the impact of exogenous covariates. Existing methods either train from scratch, losing the advantages of TSFMs, or design plugin modules that are tightly coupled with specific architectures. To address these limitations, we propose FLUG, a One-for-All framework where independently trained modules complement TSFMs. We design an Endogenous Series Filter (EFit) module guided by the Hurst Exponent to separate exogenous components from the time series, thereby enabling TSFMs to focus on modeling and forecasting endogenous patterns. In parallel, we introduce a Covariate Plugin (CPin) module that employs Multi-Scale Patchify fusion and a Causal-Aware Masking strategy based on Gradient Reversal Layer to capture the exogenous information of the target variable. By decomposing endogenous and exogenous dependencies, FLUG enables integration of covariate information across a variety of TSFMs. To supplement existing publicly available covariate time series data, we curate and release four additional datasets. Extensive experiments on real-world business and supplementary data demonstrate the framework’s effectiveness and scalability.

---

## 论文详细总结（自动生成）

# 论文总结：Filter before Plug: One-for-All Framework for Covariate-Aware Forecasting with Time Series Foundation Models

## 1. 核心问题与整体含义

- **背景**：时间序列基础模型（TSFM）在建模历史依赖方面表现出色，但**普遍忽略外生协变量**（exogenous covariates）的影响，限制了其在真实业务预测中的效果。
- **现有方法的两难**：
  - 从头训练协变量感知模型会丢失 TSFM 的预训练优势；
  - 已有的插件（plugin）模块往往与特定模型架构紧密耦合，缺乏通用性。
- **本文目标**：提出一个 **One-for-All** 通用框架 FLUG，让独立训练的模块能与任意 TSFM 组合，从而低成本地为 TSFM 补充外生变量感知能力，提升预测精度。

## 2. 方法论

- **核心思想**：将目标序列中的**内生依赖**与**外生影响**分离——先“滤掉”外生成分，让 TSFM 专注于内生模式建模；同时用并行模块显式捕获外生信息，最后融合预测。
- **两大关键模块**：
  - **Endogenous Series Filter（EFit）**：基于 **Hurst 指数（Hurst Exponent）** 引导的内生序列滤波器，从原始时间序列中分离出外生成分与内生成分，使 TSFM 输入更“干净”。
  - **Covariate Plugin（CPin）**：使用 **Multi-Scale Patchify fusion**（多尺度分块融合）和基于 **Gradient Reversal Layer（GRL）** 的 **Causal-Aware Masking**（因果感知掩码）策略，捕获外生协变量对目标变量的影响。
- **工作流程**（文字描述）：
  1. 输入历史目标序列 + 外生协变量序列；
  2. EFit 根据 Hurst 指数特征将序列分解为内生部分与外生部分；
  3. 内生部分输入 TSFM 进行基础时序依赖建模；
  4. CPin 对外生协变量做多尺度分块与因果掩码处理，提取外生表征；
  5. 将 TSFM 输出与 CPin 输出融合，生成最终预测。
- **通用性来源**：EFit 与 CPin 是**独立训练的模块**，与 TSFM 主体解耦，因此可即插即用地适配多种 TSFM 架构。

## 3. 实验设计

- **数据集**：
  - 使用了**真实世界业务数据**；
  - 作者额外整理并发布了**四个公开可用的协变量时间序列数据集**，以补充现有公共数据的不足。
- **Benchmark**：论文将 FLUG 与多种不同的时间序列基础模型耦合进行测试，验证其插件式增强效果。但摘要中**未列出具体数据集名称、基线方法列表和评估指标**（如 MSE/MAE）。
- **对比方法**：由于摘要信息有限，无法确认具体对比对象；但可推测是“TSFM 原生模型（忽略协变量）”与“TSFM + FLUG”之间的对比，以及可能与其他协变量感知方法对比。

## 4. 资源与算力

- **未说明**：论文提供的摘要和元数据中**没有提及任何算力信息**，包括 GPU 型号、数量、训练时长、参数量或能耗等。

## 5. 实验数量与充分性

- **实验数量**：从摘要可见，实验覆盖了**多个真实数据集**和**多个基础模型**，并包含对框架有效性和可扩展性的验证；但没有提供具体实验组数、消融实验细节。
- **充分性与公平性**：
  - 多数据集 + 多 TSFM 基座的实验设计具备较强的说服力；
  - 然而，由于正文不可得，无法判断是否做了充分的消融实验（如 EFit 和 CPin 的独立贡献、不同 Hurst 阈值的影响）、是否与最新 SOTA 方法公平对比、是否报告统计置信区间等。
  - 结论声称“显著提升”，但缺少具体数值支撑。

## 6. 主要结论与发现

- FLUG 作为一种“先滤后插”的通用框架，能够有效解决 TSFM 忽略外生协变量的问题。
- **独立训练模块 + TSFM 组合**即可高效处理含外生变量的预测任务，无需重新训练基础模型。
- 实验验证了 FLUG 与多种 TSFM 结合时均能提升协变量感知预测的精度，展示出良好的**可扩展性**。

## 7. 优点

- **通用性好**：One-for-All 设计，插件模块与 TSFM 架构解耦，大幅降低适配成本。
- **方法新颖**：用 Hurst 指数引导内生序列滤波，结合 GRL 和因果掩码策略，从信号特性和因果角度双重设计，思路有理论支撑。
- **数据贡献**：发布了四个额外的协变量时间序列数据集，对后续研究有实用价值。
- **实验设计**：在真实业务数据和补充公开数据上验证，覆盖多种基础模型，增强了结论的可靠性。

## 8. 不足与局限

- **信息不完整**：当前可获得的摘要中缺少定量结果、具体数据集、基线列表、评估指标和消融实验，无法全面评估方法性能。
- **潜在方法风险**：
  - Hurst 指数对非平稳、非长记忆序列可能不适用，滤波效果可能随数据特性波动；
  - 分离内生/外生成分可能造成信息损失，尤其在二者高度耦合时；
  - CPin 的多尺度分块与 GRL 掩码可能增加计算复杂度和训练难度。
- **实验覆盖不足**：未提及跨领域（如交通、能源、金融等）的广泛验证，也未讨论长期预测或极端事件下的表现。
- **应用限制**：
  - 依赖于外生协变量的可获得性和质量；
  - 缺乏对部署成本、推理延迟的分析。

---

**注意**：以上总结基于论文摘要和元数据。由于提供的文本不含论文正文细节，部分内容（如具体公式、实验数据、算力）无法确认，相关推测已标注。

（完）
