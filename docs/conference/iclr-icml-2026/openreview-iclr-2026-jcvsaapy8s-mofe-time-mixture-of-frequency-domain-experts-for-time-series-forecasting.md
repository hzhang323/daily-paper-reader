---
title: "MoFE-Time: Mixture of Frequency Domain Experts for Time-Series Forecasting"
title_zh: MoFE-Time：面向时间序列预测的频域专家混合模型
authors: "Yiwen Liu, Chenyu Zhang, Junjie Song, Siqi Chen, Lingming Zeng, Dapeng Li, Sun Yin, Zihan Wang, Ye Tong, Yuji Cao"
date: 2025-09-16
pdf: "https://openreview.net/pdf?id=jCvsaAPY8s"
tags: ["query:time-series"]
score: 9.0
evidence: 混合频域专家模型用于时间序列预测
tldr: 现有时间序列基础模型多直接套用Transformer，未充分利用时域与频域联合特征。本文提出MoFE-Time，在专家混合框架下融合时间与频域表示，设计频域-时间单元作为注意力模块后的专家，并通过路由机制动态组合专家。该模型在复杂时间序列预测上具有更优性能，为时序基础模型的设计提供了时频融合新思路。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 现有时序基础模型对时频特征联合建模不足，限制复杂序列预测性能。
method: 在MoE框架中设计频域和时间单元作为专家，路由机制动态集成时频表征。
result: 在复杂时序预测任务上展示了优于vanilla Transformer的效果。
conclusion: 时频统一建模能增强时序基础模型的预测能力。
---

## Abstract
Time series forecasting is a fundamental task with broad applications across various domains. Recently, inspired by the success of large language models (LLMs), foundation models for time series gained significant attention. However, most of existing approaches directly adopt vanilla transformers, which underexplore the joint modeling of temporal and frequency characteristics, resulting in limited performance on complex time series. To address this, we propose MoFE-Time, a novel time series forecasting foundation model that integrates temporal and frequency-domain representations within a Mixture of Experts (MoE) framework. Specifically, we design Frequency and Time Cells (FTC) as experts following attention modules, and employ an MoE routing mechanism to construct multidimensional sparse representations of input signals. Extensive experiments on six public benchmarks demonstrate that MoFE-Time achieves new state-of-the-art results. Furthermore, we construct a proprietary real-world dataset, NEV-sales, to evaluate the model's practical effectiveness. MoFE-Time consistently outperforms competitive baselines on this dataset, demonstrating its potential for real-world commercial applications.

---

## 论文详细总结（自动生成）

好的，以下是对论文 **MoFE-Time: Mixture of Frequency Domain Experts for Time-Series Forecasting** 的详细中文总结。

> 说明：由于论文 PDF 原文未完整提取（仅有元数据及摘要），以下内容基于摘要、元数据信息及可推导的论文结构进行归纳；涉及实验细节、算力等未明确信息将如实指出。

---

## 一、核心问题与整体含义（研究动机与背景）

- **研究背景**：时间序列预测是气象、金融、能源、销售等多个领域的基础性任务。近年来，受大语言模型（LLM）成功的启发，时间序列领域的“基础模型”（Foundation Models）研究逐渐兴起，业界希望构建可泛化、可迁移的时序预测模型。
- **核心问题**：现有大多数时间序列基础模型直接套用 Vanilla Transformer 结构，**未充分利用时域与频域的联合特征**。现实中的复杂时间序列往往同时包含趋势、季节性和多种周期成分，**单一时域建模**难以充分捕捉隐藏在频域中的规律，导致预测性能受限。
- **研究意义**：论文提出 MoFE-Time，尝试在 **MoE（混合专家模型）** 框架下将时域与频域表示统一建模，弥补现有时序基础模型在时频联合建模上的不足，为时序基础模型设计提供新的思路。

---

## 二、论文提出的方法论

- **核心思想**：在 MoE 框架中融合**时间域**与**频率域**两种表征，利用路由机制动态组合不同的“专家”，以构建输入信号的**多维稀疏表示**，从而提高复杂时间序列的预测能力。

- **关键技术设计**：
  - **Frequency and Time Cells（FTC）**：论文将“频域单元”和“时域单元”设计为专家模块，放置在**注意力模块之后**，作为 Transformer 架构中的增强组件。
  - **MoE 路由机制**：通过可学习的路由网络，对不同输入 token 或序列片段动态分配不同的专家权重，从而自适应地选择时域或频域建模路径。
  - **稀疏表示**：MoE 结构天然具备稀疏激活特性，这使得模型在推理时仅激活部分专家路径，既提升表达能力，又保持计算效率相对可控。

- **整体流程（文字化算法过程）**：
  1. 输入时间序列，经嵌入层或 patch 化处理后送入 Transformer 编码器；
  2. 注意力模块提取全局时域依赖关系；
  3. 将注意力输出送入 FTC 专家层，分别从时域和频域视角进一步提取特征；
  4. 路由网络根据输入特征动态分配专家组合权重；
  5. 将加权后的专家输出融合，形成多维稀疏表示；
  6. 最后经预测头输出未来时间步的预测值。

---

## 三、实验设计

- **公开基准数据集**：论文在 **六个公开 benchmark** 上进行评估，覆盖典型的时间序列预测任务场景（具体数据集名称在摘要中未逐一列出，需查阅原文确认，通常包括 ETTh1/ETTh2/ETTm1/ETTm2、Electricity、Traffic、Weather 等常用基准）。
- **私有真实数据集**：论文构建了 **NEV-sales（新能源汽车销售）** 数据集，用于检验模型在真实商业场景中的实用价值。
- **对比方法**：
  - 基线包括 **Vanilla Transformer** 及其他竞争性时序预测模型；
  - 对比重点在于证明 MoFE-Time 优于直接堆叠 Transformer 结构的现有基础模型；
  - 具体基线名单（如 PatchTST、TimesNet、iTransformer、TimeGPT 等）在摘要中未明确，需见原文实验部分。

---

## 四、资源与算力

- **论文摘要未给出任何算力相关信息**，包括：
  - GPU 型号与数量；
  - 训练总时长；
  - 模型参数量级；
  - 显存消耗等。
- 若需要评估资源效率，需查阅原文实验设置部分；当前提取文本无法支持相关阐述。

---

## 五、实验数量与充分性

- **实验数量**：
  - 公开基准实验：6 个数据集；
  - 私有数据集实验：1 个（NEV-sales）；
  - 摘要声称“达到新的 SOTA 结果”，但未展示具体消融实验数量。
- **充分性分析**：
  - 从覆盖面来看，6 个公开基准 + 1 个真实商业数据集的设计是合理的，能兼顾泛化性和实用性检验；
  - 但**摘要中未展示消融研究结果的明确描述**（例如是否有移除频域专家、移除 MoE 路由等的对照实验），因此完整实验是否充分，需以正文为准；
  - 从公平性角度，若不采用相同训练预算、相同 patch 尺寸、相同预测长度等统一设置，对比可能存在偏差——论文是否做到这一点需查阅原文实验协议。

---

## 六、主要结论与发现

- MoFE-Time 在 **六个公开时间序列基准** 上取得新的 **State-of-the-Art（SOTA）** 效果；
- 在 **NEV-sales 私有数据集** 上，MoFE-Time 一致优于多个有竞争力的基线方法，验证了其在真实商业场景中的实用潜力；
- 核心结论：**将时域与频域统一建模、并通过 MoE 机制动态组合专家，能够显著增强时序基础模型的预测能力**，优于单纯引入 Transformer 结构的做法。

---

## 七、优点

- **方法新颖**：将时频联合建模引入 MoE 框架，避免了仅堆叠 Transformer 的简单套路，方向具有创新性。
- **架构合理**：在注意力模块之后放置 FTC 专家，使模型既能提取全局依赖，又能细化时域/频域局部特征，具备结构上的清晰逻辑。
- **可解释性与稀疏性**：MoE 路由机制天然产生稀疏激活，有助于模型根据输入特性自适应选择建模路径，具备一定的可解释性。
- **应用导向**：除公开基准外，专门构建新能源汽车销售数据验证实际商业价值，体现了从学术研究到产业落地的意识。
- **结果强**：多数据集上取得 SOTA，结论具有说服力。

---

## 八、不足与局限

- **实验细节披露不充分**：从摘要级信息来看，未列出具体对比基线的数量和名称、消融组数、预测长度设置、超参数选择等，无法完全判断实验的完备性与公平性。
- **算力资源未披露**：缺少训练成本说明，难以评估模型在实际部署中的资源门槛。
- **NEV-sales 数据集可复现性风险**：该数据集为私有数据，外部研究者无法直接复现实验，可能影响验证的透明性。
- **泛化边界未知**：论文未明确讨论模型在极长序列、多变量强耦合场景或缺失数据条件下的表现，适用边界仍需更多测试支撑。
- **隐私与行业偏差**：NEV-sales 属于特定行业场景，结论向其他行业（如金融、医疗）推广时存在一定偏差风险。

---

（完）
