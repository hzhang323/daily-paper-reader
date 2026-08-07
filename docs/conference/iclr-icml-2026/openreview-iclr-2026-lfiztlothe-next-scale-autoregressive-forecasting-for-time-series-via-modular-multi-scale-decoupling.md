---
title: Next-Scale Autoregressive Forecasting for Time Series via Modular Multi-Scale Decoupling
title_zh: 通过模块化多尺度解耦实现时间序列的下一尺度自回归预测
authors: "Fanda Fan, Kuiye Ding, LiMing Mao, Xiaorui Wang, Yao Wang, Ruijie Jian, Luqi Gong, Zhenghua Lu, Chunjie Luo, Jianfeng Zhan"
date: 2025-09-20
pdf: "https://openreview.net/pdf?id=LFiztLOThe"
tags: ["query:time-series"]
score: 9.0
evidence: 多尺度自回归时间序列预测
tldr: 针对现有深度时间序列预测模型多尺度处理局限、输入输出尺度不一致的问题，本文提出模块化尺度自回归框架MSAR，通过逐尺度对齐建模解耦异质时间模式，并采用尺度间自回归，使粗尺度预测引导细尺度生成。实验表明，MSAR在多个公开数据集上带来一致的准确率提升，且不依赖特定模型结构，具有良好的通用性。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 现有深度预测模型多采用单尺度建模，或仅对输入多尺度而输出仍为单尺度，导致预测能力受限。
method: 提出MSAR模块化尺度自回归框架，逐尺度对齐输入输出并利用粗尺度预测指导细尺度生成。
result: 在多个真实数据集上验证了MSAR在多种预测任务中均取得一致性能提升。
conclusion: 多尺度解耦与尺度间自回归能有效提升时间序列预测精度。
---

## Abstract
Time series forecasting underpins critical applications in finance, energy, healthcare, and transportation. Although deep models have achieved strong results, most adopt single-scale modeling or restrict multiscale processing to the input side, causing a misalignment between multiscale inputs and single-scale outputs and limiting predictive power. We introduce the Modular Scale-wise Autoregressive Framework (MSAR), a model-agnostic design that forecasts progressively across multiple temporal resolutions. MSAR offers three advantages: (1) scale-wise aligned modeling, which disentangles heterogeneous temporal patterns by aligning inputs and outputs at each scale; (2) scale-wise autoregression, where coarse-scale predictions guide finer-scale forecasting through hierarchical information flow; and (3) a modular architecture, enabling seamless integration with diverse backbones such as CNNs, MLPs, and Transformers. Extensive experiments across a broad set of datasets and forecasting models demonstrate that MSAR achieves consistent improvements in both accuracy and inference efficiency, validating the effectiveness of scale-aligned autoregression for multiscale time series forecasting.

---

## 论文详细总结（自动生成）

### 1. 核心问题与研究动机

时间序列预测在金融、能源、医疗和交通等关键领域具有重要应用价值。现有深度预测模型虽已取得较好效果，但仍存在以下核心局限：

- **单尺度建模**：大多数深度模型仅在单一时间分辨率上建模，难以同时捕捉短期波动与长期趋势。
- **输入-输出尺度错配**：部分方法虽然对输入进行多尺度处理，但输出仍为单尺度预测，导致多尺度输入与单尺度输出之间的错位，限制了模型的预测能力。
- **缺乏跨尺度信息传递**：不同时间尺度上的异质时间模式（如季节性、趋势性、噪声性成分）未被显式解耦和关联。

### 2. 方法论：MSAR 框架

论文提出 **模块化尺度自回归框架（Modular Scale-wise Autoregressive Framework, MSAR）** ，其核心思想是将预测任务分解为多个时间尺度上的渐进式预测。

关键设计包含三个方面：

- **尺度对齐建模（Scale-wise Aligned Modeling）**：在每个时间尺度上对齐输入与输出，使不同尺度的异质时序模式被独立建模和分离，避免模式间相互干扰。
- **尺度间自回归（Scale-wise Autoregression）**：引入尺度间的层级信息流，粗尺度（低分辨率）预测结果作为条件指导细尺度（高分辨率）预测生成，形成从粗到细的自回归生成过程。该方法不同于传统时间步维度上的自回归，而是创新地在"尺度"维度上推进预测。
- **模块化架构（Modular Architecture）**：MSAR 不依赖特定模型结构，可无缝集成多种主流时序预测骨干网络，包括 CNN、MLP 和 Transformer。

论文未在摘要中给出具体公式或算法的伪代码，但根据其描述可理解流程为：首先定义多个时间尺度（如小时、天、周），从最粗尺度开始进行预测，随后将粗尺度预测结果作为条件输入，逐级引导更细尺度的预测，直到完成最终分辨率的输出。

### 3. 实验设计

- **数据集**：摘要说明实验覆盖了"broad set of datasets"（多个真实世界数据集），但具体数据集名称、领域和规模未在摘要中列明。
- **Benchmark**：涉及多种预测任务场景，涵盖不同领域的时间序列数据。
- **对比方法**：以多种主流深度预测模型为骨干（CNN、MLP、Transformer 类模型），对比 MSAR 集成前后（即 backbone 基线 vs. 加入 MSAR 的版本）的性能差异。摘要未列出具体对比方法名称。

### 4. 资源与算力

论文摘要中 **未提及任何算力资源信息** ，包括 GPU 型号、数量、训练时长、显存占用等。需查阅论文全文的实验设置部分才能获取相关信息。

### 5. 实验数量与充分性评估

- 摘要声称进行了"Extensive experiments"（广泛实验），覆盖多个数据集和多种预测骨干模型。
- 但从摘要信息判断，实验评估维度可能包括：不同骨干网络的集成效果、多种数据集上的提升一致性、准确性（accuracy）和推理效率（inference efficiency）。
- **充分性评估**：从摘要角度看，实验覆盖面较广，且验证了模型无关性的关键主张。但实际实验数量（具体数据集个数、消融实验组数）和统计显著性检验结果在摘要中不可见。由于该论文为 ICLR-2026 被拒稿件，审稿人对实验充分性或公平性可能存在一定质疑（如 baseline 调参是否公平、消融是否全面等），最终结论需以全文为准。

### 6. 主要结论与发现

- MSAR 在多个真实数据集和多种预测模型上，一致性地提升了预测准确率（accuracy）。
- MSAR 同时提升了推断效率（inference efficiency），即多尺度自回归框架在计算上也具有优势。
- 验证了尺度对齐自回归（scale-aligned autoregression）对多尺度时序预测的有效性。
- MSAR 的模块化设计使其具备良好的通用性和即插即用能力。

### 7. 优点

- **模型无关性**：MSAR 是通用框架，可即插即用地与 CNN、MLP、Transformer 等主流模型结合，具备较强的实用推广价值。
- **创新视角**：将自回归的概念从时间步维度扩展到尺度维度，思路新颖，不同于以往仅在输入侧做多尺度的做法。
- **模式解耦**：通过逐尺度对齐输入输出，显式分离异质时间模式，有助于缓解复杂时序中不同成分之间的干扰。
- **效率优势**：不仅提升精度还提升推断效率，说明框架具备工程实用性。

### 8. 不足与局限

- **信息不完整**：摘要未提供具体数据集信息，无法判断实验是基于公开 benchmark（如 ETT、M4、Traffic 等）还是私有数据，验证其结论的推广性受限。
- **细节缺失**：尺度数量如何选择、不同尺度的定义方式、尺度间条件信息的融合机制等关键实现细节在摘要中不可得。
- **消融实验不透明**：摘要未提及是否对各组件（尺度对齐、尺度自回归、尺度数量）进行了系统消融，无法确认每个设计元素的独立贡献。
- **基线公平性**：在对多种 backbone 进行集成比较时，是否对每个 baseline 进行了同等程度的超参调优，摘要中无说明，存在比较偏倚的潜在风险。
- **理论分析缺失**：论文未从理论上解释为何尺度间自回归有效，缺乏收敛性或误差传播的分析（粗尺度预测误差如何向细尺度传播）。
- **应用边界不明**：多尺度自回归对时间序列的平稳性、季节性强度、采样频率等的适用范围在摘要中没有讨论。

（完）
