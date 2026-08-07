---
title: "TKG-LLM: Temporal Knowledge Graph as Enhanced Prompt Learning with LLM for Time Series Forecasting"
title_zh: TKG-LLM：利用时序知识图谱增强提示学习的大语言模型时间序列预测
authors: "Ke Li, Chao Xu, Huang Jiajia"
date: 2025-09-12
pdf: "https://openreview.net/pdf?id=8OrJvzPdUm"
tags: ["query:time-series"]
score: 9.0
evidence: 利用时序知识图谱增强大语言模型的时间序列预测
tldr: 针对大语言模型在时间序列预测中难以捕获时间依赖与特征关联的问题，本文提出TKG-LLM，创新地构建时间知识图谱，并通过增强提示学习将图谱知识注入LLM，从而弥补自注意力机制在时序建模上的不足。实验结果表明，TKG-LLM在多个预测基准上取得最优精度，验证了外部时序知识增强LLM预测能力的有效性。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 现有LLM直接处理时间序列时只能捕捉token顺序，无法充分建模时间依赖与特征关联，导致预测精度受限。
method: 提出TKG-LLM，构建时间知识图谱并将其与提示学习融合，增强LLM对时间依赖和特征相关性的建模。
result: 在多个时间序列预测基准上验证了TKG-LLM优于现有LLM预测方法。
conclusion: 借助时序知识图谱可显著强化LLM对时间序列结构的理解与预测。
---

## Abstract
Large Language Models (LLMs) based on Transformer have shown advantages in various domains by their powerful representation learning and context understanding capabilities. Recently, researchers have begun to explore their applications in time series forecasting. Although existing methods can achieve cross-modality embedding of time series into LLMs, the self-attention in LLMs is essentially “token-to-token”. Position encoding can only reflect the sequential relationships between tokens, and the model cannot capture the temporal dependencies and correlations between features, thus not achieving excellent forecasting accuracy. Therefore, we propose the Temporal Knowledge Graph with LLM (TKG-LLM), which innovatively designs the TKG to capture the temporal structural information. We first build the TKG containing temporal edges to capture dependencies between time series and feature edges to capture relationships between features. Next, we apply the Graph Convolution Network  (GCN) to encode the graph, generating node embeddings rich in temporal structural information. Finally, we fuse the time series embeddings with the graph node embeddings to enhance representational capabilities and utilize the enhanced embeddings for dynamic prompt selection to improve forecasting performance. Additionally, to better capture the multi-scale characteristics of time series and thereby improve the accuracy of forecasts. The time series is decomposed into three components: trend, season, and residual through Wavelet Decomposition (Daubechies 4) into TKG-LLM to capture multi-scale temporal features and sudden changes accurately. We demonstrate through visualizing experimental results that Wavelet Decomposition exhibits superior performance when dealing with non-stationary time series. Our empirical experiments on multiple benchmark datasets demonstrate that the proposed TKG-LLM achieves superior forecasting performance compared to baselines. Furthermore, our ablation experiment results verify the effectiveness of using the Temporal Knowledge Graph as enhanced prompt learning.

---

## 论文详细总结（自动生成）

## TKG-LLM：利用时序知识图谱增强提示学习的大语言模型时间序列预测

### 1. 核心问题与整体含义（研究动机与背景）
- **背景**：基于 Transformer 的大语言模型（LLM）凭借强大的表征学习与上下文理解能力，在多个领域表现出色，研究者开始探索其在时间序列预测中的应用。
- **核心问题**：LLM 的自注意力机制本质上是“token 到 token”的交互，位置编码只能反映 token 之间的顺序关系，无法充分捕获时间序列中的**时间依赖**和**特征间相关性**，导致直接跨模态嵌入时间序列的预测精度有限。
- **整体含义**：为弥补 LLM 在时序建模上的不足，论文提出引入外部时序知识图谱（TKG），通过增强提示学习将结构化时序知识注入 LLM，从而提升时间序列预测性能。

### 2. 方法论
- **核心思想**：构建包含“时间边”和“特征边”的时序知识图谱（TKG），利用图卷积网络（GCN）编码图谱，生成富含时序结构信息的节点嵌入，再与时间序列嵌入融合，并基于增强嵌入进行动态提示选择，最终输入 LLM 进行预测。
- **关键技术细节**：
  - **时序知识图谱构建**：时间边捕获时间序列之间的依赖关系；特征边捕获特征之间的关联关系。
  - **图编码**：使用 GCN 对 TKG 编码，得到携带时序结构信息的节点表示。
  - **嵌入融合**：将时间序列嵌入与图节点嵌入融合，增强整体表征能力。
  - **动态提示选择**：利用增强后的嵌入动态选择提示，提高预测性能。
  - **多尺度分解**：通过小波分解（Daubechies 4）将时间序列分解为趋势、季节、残差三个分量，分别输入模型，以捕获多尺度时序特征和突变。
- **算法流程（文字描述）**：
  1. 对原始时间序列进行小波分解，得到趋势、季节、残差分量；
  2. 构建 TKG（时间边 + 特征边）；
  3. 用 GCN 编码 TKG，得到节点嵌入；
  4. 将各分量的时间序列嵌入与对应节点嵌入融合；
  5. 使用融合嵌入动态选择提示；
  6. 将增强后的输入送入 LLM，输出预测结果。

### 3. 实验设计
- **数据集 / 场景**：使用了多个基准数据集（论文未逐一列出具体名称，但提及 multiple benchmark datasets）。
- **Benchmark**：与现有 LLM 时间序列预测方法作为基线进行对比。
- **对比方法**：文中未详细列出具体基线名称，但指出 TKG-LLM 相比基线取得了更优的预测精度。
- **消融实验**：验证了 TKG 作为增强提示学习的有效性（ablation experiment results verify the effectiveness of using TKG as enhanced prompt learning）。

### 4. 资源与算力
- 论文提供的内容中**未明确说明**使用的 GPU 型号、数量、训练时长等算力资源信息。仅提及实验在多个基准数据集上进行，但未给出硬件与训练成本细节。

### 5. 实验数量与充分性
- **实验数量**：包含多个基准数据集上的主要对比实验，以及消融实验；另外通过可视化实验展示小波分解对非平稳时间序列的处理优势。
- **充分性评估**：
  - 主要实验覆盖了多个数据集和基线对比，能初步证明方法有效性。
  - 消融实验说明了 TKG 组件的贡献，但未展示全部组件（如 GCN、动态提示、小波分解）的独立消融效果。
  - 论文未列出具体数据集、评估指标和基线名称，客观性与可复现性信息不足。
  - 总体来看，实验设计方向合理，但细节披露有限，充分性有待加强。

### 6. 主要结论与发现
- TKG-LLM 在多个时间序列预测基准上优于现有 LLM 预测方法。
- 借助时序知识图谱可显著强化 LLM 对时间序列结构的理解与预测能力。
- 小波分解在处理非平稳时间序列时表现出色，有助于捕获多尺度特征和突变。

### 7. 优点
- **创新性**：将时序知识图谱与 LLM 提示学习结合，弥补了自注意力机制在时序建模上的缺陷。
- **结构建模**：通过时间边和特征边显式建模时间依赖与特征关联，增强了 LLM 对时间序列结构的感知。
- **多尺度处理**：使用小波分解将序列分解为趋势、季节、残差，兼顾平稳和非平稳成分。
- **动态提示**：基于增强嵌入进行动态提示选择，使提示更贴合输入序列。
- **实验验证**：通过可视化说明小波分解在非平稳序列上的优势，并通过消融实验验证核心组件有效性。

### 8. 不足与局限
- **细节不完整**：未提供数据集名称、评估指标、基线方法列表，难以复现和横向比较。
- **算力信息缺失**：未说明 GPU 配置和训练成本，影响工程实用性的评估。
- **消融实验不全面**：未分别验证 GCN、动态提示、小波分解等各模块的独立贡献。
- **泛化性存疑**：未讨论 TKG 构建的计算开销，以及对长序列、高维特征或不同领域数据的适应能力。
- **应用限制**：构建 TKG 需要额外设计时间边和特征边，对数据先验依赖较强，可能限制其在无明确特征关系场景下的应用。

（完）
