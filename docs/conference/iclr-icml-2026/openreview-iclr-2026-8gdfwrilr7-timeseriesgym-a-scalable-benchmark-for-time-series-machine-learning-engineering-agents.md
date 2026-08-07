---
title: "TimeSeriesGym: A Scalable Benchmark for (Time Series) Machine Learning Engineering Agents"
title_zh: TimeSeriesGym：面向时间序列机器学习工程智能体的可扩展基准
authors: "Yifu Cai, Xinyu Li, Mononito Goswami, Michał Wiliński, Gus Welter, Artur Dubrawski"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=8gdfWRilR7"
tags: ["query:time-series"]
score: 9.0
evidence: 提出可扩展的基准框架，用于评估AI智能体在时间序列机器学习工程挑战上的表现
tldr: 现有面向时间序列的AI智能体基准缺乏可扩展性，只关注模型构建且评估工件有限。TimeSeriesGym提出一个可扩展的基准框架，从多个领域和任务来源构建时间序列机器学习工程挑战，并兼顾隔离能力评估和整体流程评价。该基准能让智能体评估更贴近机器学习工程实践，为时间序列智能体研究提供标准化测试平台。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 现有时间序列智能体基准缺乏可扩展性，任务单一且评估工件有限，难以反映真实ML工程实践。
method: 构建TimeSeriesGym基准，沿任务来源多样性和能力评估两个维度扩展，覆盖多个领域与任务。
result: 该基准能够对智能体的时间序列ML工程能力进行更全面、可扩展的评估。
conclusion: 为时间序列ML工程智能体的研究提供了更具实践意义的标准化评测平台。
---

## Abstract
We introduce TimeSeriesGym, a scalable benchmarking framework for evaluating Artificial Intelligence (AI) agents on time series machine learning engineering challenges. Existing benchmarks lack scalability, focus narrowly on model building in well-defined settings, and evaluate only a limited set of research artifacts (e.g., CSV submission files). To make AI agent benchmarking more relevant to the practice of machine learning engineering, our framework scales along two critical dimensions. First, recognizing that effective ML engineering requires a range of diverse skills, TimeSeriesGym incorporates challenges from diverse sources spanning multiple domains and tasks. We design challenges to evaluate both isolated capabilities (including data handling, understanding research repositories, and code translation) and their combinations, and rather than addressing each challenge independently, we develop tools that support designing multiple challenges at scale. Second, we implement evaluation mechanisms for multiple research artifacts, including submission files, code, and models, using precise numeric measures and _optionally_ LLM-based qualitative assessments. This strategy complements objective evaluation with subjective assessment when appropriate. Although our initial focus is on time series applications, our framework can be readily extended to other data modalities, broadly enhancing the comprehensiveness and practical utility of agentic AI evaluation. We [open-source](https://anonymous.4open.science/r/TimeSeriesGym-9CF6/) our benchmarking framework to facilitate future research on the ML engineering capabilities of AI agents.

---

## 论文详细总结（自动生成）

好的，以下是根据您提供的论文元数据与摘要内容生成的中文总结：

## TimeSeriesGym：面向时间序列机器学习工程智能体的可扩展基准

### 1. 核心问题与整体含义
- **研究动机**：现有面向时间序列领域的人工智能（AI）智能体基准存在多重缺陷——缺乏可扩展性、任务设计狭隘地聚焦于定义良好环境下的模型构建、并且仅评估有限的科研产物（如CSV提交文件）。这使得智能体评测难以反映真实机器学习（ML）工程实践的复杂性与多样性。
- **核心问题**：如何构建一个既全面又可扩展的基准框架，以评估AI智能体在真实ML工程挑战中的综合能力，并提升代理评估对实际ML工程实践的指导意义。

### 2. 方法论
- **核心思想**：框架沿两个关键维度进行扩展，以实现对时间序列ML工程智能体的系统性评估。
  - **维度一 (任务来源多样性)**：认识到有效的ML工程需要多种技能，TimeSeriesGym整合了来自多个领域与任务来源的挑战。挑战设计既评估孤立能力（如数据操作、研究代码库理解、代码翻译），也评估能力的组合；同时开发工具以支持大规模设计多样化挑战，而非独立处理每个挑战。
  - **维度二 (评估工件多样性)**：实现针对多种研究产出（提交文件、代码、模型）的评估机制，采用精确的数值度量，并可选用基于LLM的定性评估。该方法在适当时结合客观评估与主观评估，以互补方式全面衡量智能体表现。
- **关键技术细节**：框架设计为易于扩展到其他数据模态，不仅限于时间序列，从而增强代理AI评估的全面性和实用性。

### 3. 实验设计
- **数据集/场景来源**：文中提及挑战整合自“多个领域和任务”，但未明确列出具体领域名称。
- **基准构成**：TimeSeriesGym本身即为基准框架，涵盖数据操作、代码库理解、代码翻译及模型构建等多种挑战类型。
- **对比方法**：文摘未提及与任何基线或现有方法进行定量对比。

### 4. 资源与算力
- **未明确说明**：文摘中未提及所使用的GPU型号、数量、训练时长或任何计算资源相关信息。

### 5. 实验数量与充分性
- **实验数量**：文摘中未提供具体的实验组数、消融研究数量或不同数据集上的测试结果数据。
- **充分性评估**：由于缺乏具体实验结果和对比数据，无法从文摘层面评估实验的充分性、客观性或公平性。但框架本身的设计逻辑具有系统性和层次感，其评估机制的双轨制（数值+LLM定性）为客观性和全面性提供了结构保障。

### 6. 主要结论与发现
- TimeSeriesGym提供了一个可扩展的基准测试框架，能够对AI智能体在时间序列ML工程方面的能力进行更全面、更贴近实践的可扩展评估。
- 该框架将基准评估从单一的模型构建和CSV提交，拓展至多样化任务源及多形态科研工件，为时间序列智能体研究提供了更富有实践意义的标准化测试平台。
- 框架被开源，以促进未来AI智能体ML工程能力的研究。

### 7. 优点
- **高实践相关性**：针对真实ML工程场景设计，强调技能组合及多工件交付，而非单一模型构建，使评估结果对实际应用更具参考价值。
- **双向可扩展性**：沿任务来源和评估工件两个维度扩展，兼顾隔离能力评测与整体流程评价，体现了分层级、系统化的评测思路。
- **评估机制多元**：将精确数值度量与可选的LLM定性评估结合，在客观性和主观性之间取得平衡，能够捕捉单一指标难以衡量的质量维度。
- **泛化潜力强**：框架设计不止于时间序列，可推广至其他数据模态，具有广泛的应用前景。

### 8. 不足与局限
- **实验细节缺失**：文摘内容不包含具体实验设置、基线对比或性能数据，难以据此判断框架实际运行效果及鲁棒性。
- **评估主观性风险**：虽然LLM定性评估是“可选”机制，但若大范围使用，其评估结果可能引入偏差，稳定性也需进一步验证（如提示敏感性、模型自偏置等）。
- **初始覆盖范围有限**：尽管框架可扩展，但当前重点仍以时间序列领域为主，对其他模态边界条件的探索尚待推进。
- **信息来源局限**：本总结仅基于论文摘要与元数据，未涵盖完整论文中的数据集统计细节、算力消耗及负面结果分析，故部分结论可能存在信息不完整。

（完）
