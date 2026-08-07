---
title: "CaTS-Bench: Can Language Models Describe Numeric Time Series?"
title_zh: CaTS-Bench：语言模型能否描述数值时间序列？
authors: "Luca Zhou, Pratham Yashwante, Marshall Fisher, Alessio Sampieri, Zihao Zhou, Fabio Galasso, Rose Yu"
date: 2025-09-16
pdf: "https://openreview.net/pdf?id=Ksvv8x00eo"
tags: ["query:time-series"]
score: 8.0
evidence: 首个大规模真实世界上下文感知时间序列描述基准，涵盖11个数据集和问答任务
tldr: 时间序列描述任务需要数值推理、趋势理解和上下文理解，但现有基准多基于合成数据且忽略元数据和图像。CaTS-Bench构建了首个大规模真实世界上下文感知时间序列描述基准，涵盖11个数据集、约465k训练时间戳，每个样本包含数值序列、元数据、折线图和描述。该基准以描述和问答任务形式评估语言模型对时间序列的理解能力，为相关研究提供标准化评测资源。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 现有时间序列描述基准缺乏真实世界数据、上下文元数据以及视觉信息，评估不够全面。
method: 构建大规模真实世界时间序列描述基准，融合数值序列、元数据和折线图，设计描述与问答任务。
result: 提供了约465k训练和105k测试时间戳的标准化评测集合，支持对LLM时间序列理解能力的评估。
conclusion: 为时间序列描述任务提供了高质量基准，推动语言模型在时间序列理解领域的发展。
---

## Abstract
Time series captioning, the task of describing numeric time series in natural language, requires numerical reasoning, trend interpretation, and contextual understanding. Existing benchmarks, however, often rely on synthetic data or overly simplistic captions, and typically neglect metadata and visual representations. To close this gap, we introduce **CaTS-Bench**, the first large-scale, real-world benchmark for **C**ontext-**a**ware **T**ime **S**eries captioning. CaTS-Bench is derived from *11* diverse datasets reframed as captioning and Q&A tasks, comprising roughly *465k* training and *105k* test timestamps. Each sample includes a numeric series segment, contextual metadata, a line-chart image, and a caption. A key contribution of this work is the scalable pipeline used to generate reference captions: while most references are produced by an oracle LLM and verified through factual checks, human indistinguishability studies, and diversity analyses, we also provide a human-revisited subset of *579* test captions, refined from LLM outputs to ensure accuracy and human-like style. Beyond captioning, CaTS-Bench offers *460* multiple-choice questions targeting deeper aspects of time series reasoning. We further propose new tailored evaluation metrics and benchmark leading VLMs, highlighting both their strengths and persistent limitations. Together, these contributions establish CaTS-Bench and its captioning pipeline as a reliable and extensible foundation for future research at the intersection of time series analysis and foundation models.

---

## 论文详细总结（自动生成）

好的，以下是对论文《CaTS-Bench: Can Language Models Describe Numeric Time Series?》的详细中文总结：

---

## 一、论文的核心问题与整体含义

本论文关注的是**时间序列描述（Time Series Captioning）**任务，即让模型用自然语言来描述数值时间序列。这一任务要求模型具备数值推理能力、趋势理解能力和上下文理解能力。

**研究动机与背景：**
- 时间序列数据在金融、医疗、气候等领域广泛应用，将其转化为自然语言描述有助于非专业用户理解数据，也能辅助决策。
- 现有时间序列描述基准存在明显不足：依赖于合成数据，描述过于简单，通常忽略元数据（如领域标签）和可视化信息（如折线图），无法全面评估语言模型在真实场景中的表现。
- 大型语言模型（LLM）和视觉语言模型（VLM）的快速发展，为时间序列描述提供了新的可能，但缺乏高质量、大规模、真实世界的评测基准来验证其能力。

**核心问题：** 语言模型能否准确、完整地描述数值时间序列？它们在哪些方面表现良好，哪些方面存在局限？

---

## 二、论文提出的方法论

论文的核心贡献是构建了 **CaTS-Bench**（Context-aware Time Series Captioning Benchmark），一个大规模真实世界上下文感知时间序列描述基准。

**1. 数据构建与样本结构**
- 数据来源：从 **11个不同的真实世界数据集** 中提取数据，重构为描述（captioning）和问答（Q&A）两类任务。
- 数据规模：包含约 **465k 训练时间戳** 和 **105k 测试时间戳**。
- 每个样本包含四个核心组件：
  - 数值时间序列片段
  - 上下文元数据（contextual metadata）
  - 折线图图像（line-chart image）
  - 自然语言描述（caption）

**2. 参考描述生成管线**
论文提出了一种**可扩展的参考描述生成管线**，这是其关键方法论贡献：
- 大多数参考描述由 **oracle LLM** 生成；
- 随后通过**事实核查（factual checks）**、**人类不可区分性研究（human indistinguishability studies）** 和 **多样性分析（diversity analyses）** 进行验证；
- 此外，论文提供了一个 **579 个测试描述** 的**人工修订子集**，确保描述准确性和人类风格。

**3. 问答任务设计**
- 除了描述生成，CaTS-Bench 还提供 **460 个多项选择题**，旨在测试时间序列推理的更深层能力（如趋势判断、异常检测、模式识别等）。

**4. 评估指标**
- 论文提出了**新的定制化评估指标（tailored evaluation metrics）**，以更准确地衡量时间序列描述的质量。

---

## 三、实验设计

**1. 数据集与场景**
- 基准涵盖 **11个多样性真实世界数据集**，覆盖不同领域的时间序列数据，确保评估的广泛性和代表性。
- 每个数据集被重新构建为描述任务和问答任务，样本包含多模态信息（数值+元数据+图像）。

**2. Benchmark 特性**
- **大规模**：465k 训练 + 105k 测试时间戳；
- **真实世界**：基于真实数据，而非合成数据；
- **上下文感知**：包含元数据和折线图，模拟实际应用场景；
- **多任务**：同时支持描述生成和问答两种评估范式。

**3. 对比方法**
- 论文评估了**领先的视觉语言模型（VLMs）**，以此检验当前最先进模型在时间序列描述上的能力边界。具体模型名称和配置在摘要中未详细列出，但强调了其评估范围覆盖了代表性VLM。

---

## 四、资源与算力

论文摘要和元数据中**未明确报告**使用的GPU型号、数量、训练时长等算力信息。仅能确认训练集规模为465k时间戳，评估涉及多个VLM，但具体计算资源消耗未说明。如需了解详细的硬件配置、训练时间和成本，需查阅论文全文的实验设置部分。

---

## 五、实验数量与充分性

**实验内容：**
- 大规模基准构建实验（465k训练 / 105k测试时间戳）；
- 参考描述的事实核查、人类不可区分性研究、多样性分析；
- 579条人工修订描述子集的质量评估；
- 460个多选题的问答任务评估；
- 对多个领先VLM的系统性基准测试；
- 新指标的有效性验证。

**充分性与客观性评估：**
- 数据规模大、覆盖11个真实数据集，实验基础较为扎实；
- 采用多种验证手段（事实核查、人工区分性测试、多样性分析）增强参考描述的可靠性；
- 引入人工修订子集作为质量控制，提高了评估的客观性；
- 多任务设计（描述+问答）提供了多维度评估视角。
- **可能的不足**：由于摘要信息较简略，无法确认是否包含消融实验、不同模型规模对比、以及与现有基准的直接对比等详细实验设计；整体实验的公平性和完备性需阅读全文后综合判断。

---

## 六、论文的主要结论与发现

1. **CaTS-Bench 成功填补了空白**：它是首个大规模、真实世界、上下文感知的时间序列描述基准，克服了现有基准依赖合成数据和忽略上下文信息的局限。
2. **构建了可靠的基准基础设施**：所提出的参考描述生成管线具有可扩展性，结合多种验证机制，能够产出高质量、类人的描述，为社区提供了标准化评测资源。
3. **揭示了VLM的能力与局限**：对领先VLM的评估显示，当前模型在时间序列描述任务上既有明显优势，也存在**持续的局限性**（如数值精确性、长期趋势理解、跨领域泛化等），表明该任务仍有较大提升空间。
4. **提供了多任务评估框架**：描述+问答的双任务设计，推动了对时间序列理解能力的全方位评估。

---

## 七、优点

- **真实世界大规模数据**：基于11个真实数据集，克服了合成数据的局限，更具应用价值。
- **上下文感知多模态设计**：同时融合数值序列、元数据和折线图，更贴近实际应用场景，全面评估模型的综合理解能力。
- **可扩展的参考描述生成管线**：利用oracle LLM生成+多层次验证，既能规模化生产描述，又保证了质量，这是方法论上的重要亮点。
- **人工修订子集**：579条人工精修描述为评估提供了更高质量的参照标准，增强基准可靠性。
- **多任务评估**：描述生成+问答（460题）双轨设计，覆盖了不同层次的时间序列理解能力。
- **定制化评估指标**：提出新的评价方法，更贴合时间序列描述任务的特性。

---

## 八、不足与局限

- **算力资源未报告**：未说明训练和评估所用的具体计算资源，不利于复现和成本评估。
- **基准依赖LLM生成描述**：尽管经过事实核查和人工修订，但大部分参考描述仍由LLM生成，可能存在模型固有偏见或风格偏差，影响评估的绝对客观性。
- **数据集多样性仍有局限**：虽然涵盖11个数据集，但相对于时间序列应用的广阔领域（如医疗、金融、气象），覆盖仍有限，可能影响结论的普适性。
- **VLM评估范围未详述**：摘要未列出具体涉及的VLM型号，无法判断评估的广度和代表性；也缺少与现有基准的定量对比。
- **指标的新颖性需进一步验证**：提出的定制化评估指标是否有充分的理论依据和实证支持，摘要中未提供细节，其有效性和可比性有待验证。
- **人类评估样本量有限**：579条人工修订子集相较于105k测试集占比较小，人工修订的覆盖面可能不够广泛。
- **语言和领域偏差**：基准主要以英文描述为主，且在特定领域数据上构建，对非英语场景和不同文化背景的适用性需进一步探讨。

---

（完）
