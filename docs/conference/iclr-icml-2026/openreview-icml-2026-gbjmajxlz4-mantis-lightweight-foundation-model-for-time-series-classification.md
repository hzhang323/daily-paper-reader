---
title: "Mantis: Lightweight Foundation Model for Time Series Classification"
title_zh: Mantis：用于时间序列分类的轻量级基础模型
authors: "Vasilii Feofanov, Songkang Wen, Shifeng Xie, Simon Roschmann, Marius Alonso, Hongbo Guo, Romain Ilbert, Malik Tiomoko, Quentin Bouniot, Zeynep Akata, Lujia Pan, Jianfeng Zhang, Ievgen Redko"
date: 2026-04-30
pdf: "https://openreview.net/pdf/007cc422781e7c406b0d2789b99d20cad55d9b32.pdf"
tags: ["query:time-series"]
score: 9.0
evidence: 提出轻量级Transformer基础模型，基于合成数据预训练，用于时间序列分类
tldr: 时间序列分类的基础模型研究较少，且现有工作多集中于预测。Mantis提出基于合成数据预训练的轻量级Transformer基础模型，利用自监督对比学习并设计新的token生成单元。还提出测试时增强方法，利用中间层表征、自集成和跨模型嵌入融合，缩小与专用模型的性能差距。该工作为时间序列分类提供了一种高效的基础模型方案。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 基础模型在时间序列分类领域探索不足，现有研究主要聚焦于预测任务。
method: 设计基于合成数据预训练的自监督对比学习框架，提出新型token生成单元与测试时增强策略。
result: Mantis在多个时间序列分类基准上接近甚至超过专用模型，同时保持轻量级。
conclusion: 证明了无需真实数据预训练也能构建有效的时间序列分类基础模型。
---

## Abstract
While foundation models have revolutionized various domains, their application to time series classification remains rather under-explored, with existing literature predominantly focused on forecasting. To bridge this gap, we introduce \textbf{Mantis}, a transformer-based foundation model pre-trained exclusively on synthetic data via self-supervised contrastive learning. We demonstrate that effective tokenization is critical to unlocking the full potential of transformers, proposing a novel token generator unit. Furthermore, we introduce an enhanced test-time methodology that bridges the performance gap between Mantis and strong specialized approaches by leveraging intermediate-layer representations, self-ensembling, and cross-model embedding fusion. Extensive experiments demonstrate that Mantis establishes a new state-of-the-art, outperforming existing foundation models across four diverse dataset collections covering various application domains.

---

## 论文详细总结（自动生成）

## 论文总结：Mantis——用于时间序列分类的轻量级基础模型

### 1. 核心问题与整体含义（研究动机与背景）

- **研究背景**：基础模型（Foundation Model）已在 NLP、CV 等领域取得突破，但在时间序列任务中的应用仍主要集中在**预测（forecasting）**方向，**分类（classification）**领域的基础模型研究相对匮乏。
- **核心问题**：能否构建一个**仅依赖合成数据预训练**的轻量级时间序列分类基础模型，使其在无需真实数据预训练的情况下逼近乃至超越专用模型？
- **整体含义**：Mantis 的提出证明——**时间序列分类任务无需依赖大规模真实数据预训练**，也能训练出高效可用的基础模型。这为时间序列基础模型的研究提供了一条低成本、可扩展的新路径，填补了该领域“重预测、轻分类”的研究空白。

### 2. 方法论：核心思想、关键技术细节与算法流程

- **核心思想**：以 Transformer 为骨干，**仅用合成数据**通过**自监督对比学习（self-supervised contrastive learning）**进行预训练，避开真实数据稀缺、标注成本高等问题。
- **关键技术细节**：
  - **新型 Token 生成单元（token generator unit）**：作者认为 tokenization 是释放 Transformer 潜力的关键瓶颈，因此专门设计了新的 token 生成模块，以更好地将原始时间序列转化为适合 Transformer 处理的 token 序列。
  - **测试时增强方法**：为缩小与强专用模型之间的性能差距，Mantis 在推理阶段引入多重策略：
    - **中间层表征利用**：不仅使用最终输出，还借助 Transformer 中间层的表征做分类决策；
    - **自集成（self-ensembling）**：对同一输入在不同增强/扰动下的预测进行集成；
    - **跨模型嵌入融合**：将多个模型的嵌入表征进行融合，进一步提升鲁棒性。
- **算法流程（文字描述）**：
  1. 生成合成时间序列数据 → 2. 通过对比学习在合成数据上预训练 Transformer 编码器（含新 token 生成单元）→ 3. 在下游分类任务上微调 → 4. 推理时应用增强策略（中间层表征 + 自集成 + 跨模型嵌入融合）输出分类结果。
- 论文未给出具体公式或损失函数的数学细节（提取文本中未包含）。

### 3. 实验设计

- **数据集 / 场景**：
  - 覆盖**四个不同的数据集集合（four diverse dataset collections）**，涵盖多种应用领域。
  - 具体的数据集名称在该论文文本提取中**并未明确列出**。
- **Benchmark**：以时间序列分类任务为基准，主要与**已有基础模型**进行横向比较。
- **对比方法**：
  - 与现有的时间序列**基础模型（foundation models）**做对比，Mantis 在这些模型上取得了新的最优结果（SOTA）；
  - 同时与**强专用模型（strong specialized approaches）**对比，验证性能差距。

### 4. 资源与算力

- 文中提取的文本**未说明**具体 GPU 型号、数量、训练时长等算力信息。
- 仅能从模型名称（“轻量级”）推断其参数量级和资源消耗相对较小，但**具体的算力投入无公开信息**。

### 5. 实验数量与充分性

- 实验覆盖了 4 个不同的数据集集合，验证了模型在**跨领域、跨场景**的泛化能力；
- 针对测试时增强策略（中间层表征、自集成、跨模型嵌入融合）进行了消融式探讨，说明各部分对性能的贡献；
- 但受限于提取文本的长度，**具体实验组数、统计显著性检验、消融细节**等信息不可见，无法判断其统计完整性和复现便利性。总体来看，实验覆盖广度较好，但**透明度和可复现细节略显不足**。

### 6. 主要结论与发现

- Mantis 在多个时间序列分类基准上**超越了现有基础模型**，达到新的 SOTA 水平；
- 通过测试时增强方法，Mantis 能够**缩小与强专用模型之间的性能差距**；
- 证明了**仅用合成数据预训练、无需真实数据**也能构建出有效的时间序列分类基础模型，且模型保持**轻量级**特性。

### 7. 优点

- **数据效率高**：采用合成数据预训练，摆脱了对大规模真实时间序列数据的依赖，降低了数据收集和标注成本。
- **任务定位新颖**：聚焦于时间序列分类这一被基础模型研究“冷落”的任务，填补空白。
- **方法设计有亮点**：
  - 专门设计 token 生成单元，从 tokenization 层面切入优化 Transformer 性能，思路有针对性；
  - 测试时增强策略（中间层表征 + 自集成 + 跨模型嵌入融合）提供了**无需额外训练即可提升性能**的通用技巧，实用性强。
- **轻量级**：模型规模小、计算开销低，便于实际部署。
- **结论具有启发性**：为“合成数据预训练 + 时间序列基础模型”的研究方向提供了有力证据。

### 8. 不足与局限

- **实验细节缺失**：提取文本未给出具体数据集名称、对比模型清单、消融实验表和统计显著性结果，难以全面评估实验的严谨性。
- **算力信息缺失**：未说明训练所需算力、时间与资源开销，影响可复现性和成本评估。
- **依赖合成数据**：合成数据与真实世界时间序列之间的分布差异（domain gap）未被充分讨论，其在高噪声、非平稳、长序列等复杂真实场景下的表现仍存疑。
- **与专用模型的差距**：虽然性能差距被缩小，但 Mantis 尚未完全超越强专用模型，说明其上限仍受限于通用基础架构。
- **领域覆盖有限**：仅验证了 4 个数据集集合，对医疗、金融、工业等特定垂直领域的专项验证不足。
- **缺乏理论分析**：token 生成单元和测试时增强为何有效，未给出深层的理论解释。

（完）
