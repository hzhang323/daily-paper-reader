---
title: "MMTS-Bench: A Comprehensive Benchmark for Multimodal Time Series Understanding and Reasoning"
title_zh: MMTS-Bench：一个全面的多模态时间序列理解与推理基准
authors: "Yao Yin, Zhenyu Xiao, Musheng Li, Yiwen Liu, Sutong Nan, Yiting He, Ruiqi Wang, Zhenwei Zhang, Yuantao Gu"
date: 2025-09-14
pdf: "https://openreview.net/pdf?id=PMKpyXk0FO"
tags: ["query:time-series"]
score: 9.0
evidence: 提供全面的多模态时间序列评估基准，测评LLM的时间序列理解与推理能力
tldr: 本文指出现有LLM在时间序列任务上的评估基准零散且缺乏系统性，为此提出MMTS-Bench，一个覆盖特征分析、时间推理和跨模态对齐等任务的多模态时间序列基准。基准包含2424个时间序列问答对，分为Base、InWild、Match和Align四个子集，并通过渐进式真实场景问答框架和模块化合成数据构建。评测了闭源、开源LLM及现有时间序列模型，为多模态时间序列理解与推理提供了标准化评估工具。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 现有时间序列基准对各类LLM在时间序列任务上的评估零散且缺乏系统性，难以全面衡量模型能力。
method: 构建包含2424个时间序列问答对的多模态基准MMTS-Bench，涵盖特征分析、时间推理和跨模态对齐等任务，分四个子集设计。
result: 对闭源与开源LLM及现有时间序列模型进行广泛评测，揭示其在时间序列理解与推理上的性能表现。
conclusion: MMTS-Bench为多模态时间序列任务提供了系统化评估基准，推动LLM在时间序列领域的应用。
---

## Abstract
Time series data are central to domains such as finance, healthcare, and cloud computing, yet existing benchmarks for evaluating various large language models (LLMs) on temporal tasks remain scattered and unsystematic. To bridge this gap, we introduce MMTS-Bench, a comprehensive multimodal benchmark built upon a hierarchical taxonomy of time-series tasks, spanning feature analysis, temporal reasoning, and cross-modal alignment. MMTS-Bench comprises 2,424 time series question answering (TSQA) pairs across 4 subsets: Base, InWild, Match, and Align, generated through a progressive real-world QA framework and modular synthetic data construction. We conduct extensive evaluations on closed-source, open-source LLMs and existing time series adapted large language models (TS-LLMs), revealing that: (1) TS-LLMs significantly lag behind general-purpose LLMs in cross-domain generalization, (2) LLMs show weaknesses in local tasks compared to global tasks, and (3) chain-of-thought (CoT) reasoning and multimodal integration substantially improve performance. MMTS-Bench not only provides a rigorous evaluation framework but also offers clear directions for advancing LLMs toward robust, interpretable, and generalizable time-series reasoning.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义（研究动机和背景）

- **背景**：时间序列数据在金融、医疗、云计算等领域至关重要，但现有用于评估大语言模型（LLM）在时序任务上能力的基准测试零散且缺乏系统性，难以全面衡量不同模型的表现。
- **核心问题**：缺乏一个统一、全面、可扩展的基准来系统评估 LLM 在多模态时间序列理解与推理任务上的能力，尤其是跨模态对齐、特征分析和时间推理等维度。
- **整体含义**：该论文旨在填补这一空白，通过提出标准化基准，为 LLM 在时间序列领域的应用提供可靠的评估工具和发展方向。

---

### 2. 论文提出的方法论：核心思想、关键技术细节

- **核心思想**：构建一个基于**层级任务分类法**的多模态时间序列基准（MMTS-Bench），覆盖从低层次的特征分析到高层次的时间推理和跨模态对齐任务。
- **基准构成**：包含 **2,424 个时间序列问答（TSQA）对**，分为四个子集：
  - **Base**：基础任务子集。
  - **InWild**：真实场景任务子集。
  - **Match**：匹配/对齐任务子集。
  - **Align**：跨模态对齐任务子集。
- **数据构建方法**：
  - 采用**渐进式真实场景问答框架**（progressive real-world QA framework）生成贴近实际应用的问题。
  - 结合**模块化合成数据构建**（modular synthetic data construction）精确控制任务难度和模态组合。
- **任务分类**：任务分为三类层级：
  - 特征分析（低层次）
  - 时间推理（中层次）
  - 跨模态对齐（高层次）
- 注：文中未提供具体公式或算法伪代码，但方法强调结构化和模块化设计。

---

### 3. 实验设计：数据集 / 场景 / 基准 / 对比方法

- **数据集与场景**：
  - 使用自建的 **MMTS-Bench** 基准，包含 2,424 个 TSQA 对，覆盖金融、医疗、云计算等真实场景（InWild 子集）和合成场景（Base、Match、Align 子集）。
- **评估对象**：
  - **闭源 LLM**（如商业大模型）。
  - **开源 LLM**。
  - **现有时间序列适配大语言模型（TS-LLMs）**，即针对时序任务专门微调的模型。
- **对比维度**：
  - 模型在四个子集上的准确率/表现。
  - 跨领域泛化能力。
  - 局部任务 vs 全局任务的性能差异。
  - Chain-of-Thought（CoT）推理和多模态集成的影响。

---

### 4. 资源与算力

- **文中未明确提及**所使用的 GPU 型号、数量、训练/推理时长等具体算力信息。
- 仅可推测涉及多种 LLM 的推理评估，但具体硬件资源细节未被披露。

---

### 5. 实验数量与充分性

- **实验组数**：论文进行了**广泛评估**，覆盖闭源、开源 LLM 及 TS-LLM 三大类模型，结合 4 个子集的对比，隐含大量实验组合。但摘要中**未给出具体数值**（如模型数量、实验次数）。
- **充分性评价**：
  - **优点**：基准设计包含多任务、多子集、多种模型类型，覆盖面较广，任务层级设计使得评估更具系统性。
  - **不足**：
    - 未提供消融实验细节（如移除 CoT、去掉多模态输入对结果的影响）。
    - 未提供统计显著性分析或误差棒。
    - 对比方法中是否包含传统时间序列模型（非 LLM）尚不明确。
  - 总体而言，实验设计方向合理，但细节披露不够充分，客观性和公平性难以完全确认。

---

### 6. 论文的主要结论与发现

- **结论一**：**TS-LLM 在跨领域泛化上显著落后于通用 LLM**，提示专门化的时序模型可能过拟合特定分布。
- **结论二**：**LLM 在局部任务上表现弱于全局任务**，说明模型更擅长整体趋势理解而非细粒度局部特征提取。
- **结论三**：**Chain-of-Thought（CoT）推理和多模态集成能大幅提升性能**，验证了逐步推理和跨模态信息融合在时间序列推理中的价值。
- **整体**：MMTS-Bench 不仅可以作为标准化评估工具，还为构建**鲁棒、可解释、可泛化**的时间序列推理 LLM 提供了明确方向。

---

### 7. 优点：方法或实验设计上的亮点

- **系统性**：基于层级任务分类法，覆盖低中高三个层次的时间序列能力，避免以往基准的零散问题。
- **多模态设计**：引入跨模态对齐子集（Align），考察文本与序列数据的融合能力，贴合真实应用。
- **渐进式问答框架**：真实场景与合成数据结合，兼顾生态效度和任务可控性。
- **模型覆盖广**：同时评估闭源、开源和专门化 TS-LLM，对比维度全面。
- **实用发现**：对 CoT 和多模态集成的研究给出实证支持，对未来模型设计有直接指导意义。

---

### 8. 不足与局限

- **实验覆盖有限**：
  - 摘要中未披露具体模型数量、各子集样本量分布、难度梯度等信息。
  - 可能缺少对传统非 LLM 时序模型（如 ARIMA、LSTM）的对比，无法体现 LLM 的相对优势。
  - 未提及跨语言、跨领域（如工业、能源）的泛化测试。
- **偏差风险**：
  - 合成数据可能引入生成偏差，导致模型在真实场景（InWild）上的表现被高估或低估。
  - 未说明问答对是否经过人工验证，存在标注质量隐患。
- **应用限制**：
  - 基准的评估聚焦于问答形式，可能无法完全反映真实时序任务（如预测、异常检测）中的实用性。
  - 未讨论基准对模型大小的敏感性或评测成本。
  - 算力信息缺失，难以评估复现成本。
- **可解释性不足**：论文未提供对“为什么 CoT 有效”“为何 TS-LLM 泛化弱”的深层分析。

---

（完）
