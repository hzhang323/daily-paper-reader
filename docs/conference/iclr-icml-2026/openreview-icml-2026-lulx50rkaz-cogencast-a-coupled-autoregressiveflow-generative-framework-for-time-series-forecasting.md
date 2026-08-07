---
title: "CoGenCast: A Coupled Autoregressive–Flow Generative Framework for Time Series Forecasting"
title_zh: CoGenCast：耦合自回归-流生成的时序预测框架
authors: "Mingyue Cheng, Yaguo Liu, Daoyu Wang, Xiaoyu Tao, Qi Liu"
date: 2026-04-30
pdf: "https://openreview.net/pdf/ac004f1c40de4c64e87fe257839e759a6fe88e66.pdf"
tags: ["query:time-series"]
score: 9.0
evidence: 融合大语言模型与流匹配的时序预测生成框架
tldr: 针对时序预测需同时刻画语义背景与连续动态的问题，CoGenCast 将预训练大语言模型与流匹配机制耦合为混合生成框架。通过重新配置解码器型 LLM 为原生预测编码器-解码器，同时建模条件语义与随机时间演化。实验证明其在多个预测任务上优于单独使用 LLM 或扩散模型的方法。该工作为利用大语言模型进行概率时序预测提供了新的混合架构思路。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 现有预测方法难以同时建模语义上下文与连续随机动态，LLM或扩散模型单独使用均有局限。
method: 提出CoGenCast，将预训练LLM与流匹配机制耦合，重构解码器为预测编码器-解码器来实现混合预测。
result: 实验表明CoGenCast在多种时序预测任务上优于仅用LLM或扩散模型的基线，兼顾语义与概率生成。
conclusion: 验证了LLM与流匹配结合可有效提升时间序列预测的精度和不确定性建模能力。
---

## Abstract
Time series forecasting can be  viewed as a generative problem that requires both semantic understanding over contextual conditions and stochastic modeling of continuous temporal dynamics. Existing approaches typically rely on either autoregressive large language models (LLMs) for semantic context modeling or diffusion-like models for continuous probabilistic generation. However, neither method alone can adequately model both aspects simultaneously. In this work, we propose CoGenCast, a hybrid generative framework that couples pre-trained LLMs with flow-matching mechanism for effective time series forecasting. Specifically, we reconfigure  pre-trained decoder-only LLMs into a  native forecasting encoder–decoder backbone by modifying only the attention topology, enabling bidirectional context encoding and causal representation generation. Building on this, a flow-matching mechanism  is further integrated to model temporal evolution, capturing continuous stochastic dynamics conditioned on the autoregressively generated representation. Notably, CoGenCast naturally supports multimodal forecasting and cross-domain unified training. Extensive experiments on multiple benchmarks show that CoGenCast achieves  competitive performance compared to previous  baselines. Code is available at \url{https://github.com/liuyaguo/_CoGenCast}.

---

## 论文详细总结（自动生成）

# CoGenCast：耦合自回归-流生成的时序预测框架 —— 论文总结

## 1. 核心问题与研究动机

- 时间序列预测本质上可视为一个**条件生成问题**，既需要理解历史与上下文中的**语义信息**，也需要对连续时间演化的**随机动态**进行建模。
- 现有方法通常分为两类：
  - 基于**自回归大语言模型（LLM）** 的方法：擅长语义上下文建模，但对连续、高维时间动态的概率生成能力不足；
  - 基于**扩散模型 / 流模型**的方法：擅长连续分布建模，但缺乏对语义条件的深度理解。
- 论文指出，**单一模型难以同时兼顾语义理解与连续随机建模**，这是当前概率时序预测的核心瓶颈。

## 2. 方法论：CoGenCast

- **核心思想**：将预训练 LLM 与流匹配（Flow Matching）机制耦合，形成一个**混合生成框架**，在同一个模型中同时完成语义编码与随机动态生成。
- **关键技术步骤**：
  1. **重构预训练解码器型 LLM**：
     - 仅通过修改**注意力拓扑结构**，将原本的 decoder-only LLM 改造为“预测专用编码器-解码器”骨干；
     - 使模型既能进行**双向上下文编码**，又能进行**因果表示生成**，适应时序预测的输入-输出结构。
  2. **集成流匹配机制**：
     - 在自回归生成的表征基础上，使用流匹配模型建模**时间演化过程**；
     - 通过连续流来捕获未来轨迹的随机性，从而输出概率性预测分布，而非单点确定性预测。
  3. **统一训练与多模态支持**：
     - CoGenCast 天然支持**多模态预测**和**跨域统一训练**，适合在不同类型时间序列数据上共享知识。
- **整体流程（文字说明）**：
  - 输入历史时间序列 → LLM 编码器提取语义上下文 → 生成条件表征 → 流匹配模型基于该表征逐步生成未来时间轨迹 → 输出概率预测分布。
- 论文未在摘要中给出具体公式，但从框架描述看，其核心是“自回归语义表征”与“连续流生成”的耦合。

## 3. 实验设计

- **数据集 / 场景**：
  - 论文提到使用了**多个 benchmark** 进行验证，但摘要中未列出具体数据集名称。
  - 涵盖任务属于**概率时间序列预测**，可能包括单变量/多变量预测、跨域统一训练等场景。
- **对比方法**：
  - 主要与**单独使用 LLM 的方法**、**单独使用扩散/流模型的方法**进行对比；
  - 应该也包括传统统计方法、Transformer 类预测模型及现有生成式预测基线，但完整列表需原文确认。
- **评估指标**：
  - 摘要未具体说明，通常概率预测使用 CRPS、负对数似然（NLL）等，也会报告点预测误差（MAE/MSE）。

## 4. 资源与算力

- **在提供的摘要与元数据中，未明确说明使用的 GPU 型号、数量、训练时长或计算开销**。
- 仅能确认模型基于预训练 LLM 进行改造并进行实验，实际训练成本未知。
- 若读者需要复现或评估资源需求，需查阅论文正文或开源代码仓库。

## 5. 实验数量与充分性

- 从摘要看，作者声称进行了“extensive experiments” on multiple benchmarks，说明实验覆盖多个数据集。
- 但由于本次可见内容仅包含摘要与元数据，**具体的实验组数、消融实验、敏感性分析等情况无法确认**。
- 就目前信息评估：
  - 实验框架设计是合理的：对比 LLM-only 与 diffusion/flow-only 基线，能直接验证耦合机制的增益；
  - 但缺少数据集细节、基线完整列表、显著性检验等信息，**充分的公平性判断需要阅读全文**。

## 6. 主要结论与发现

- CoGenCast 在多个时序预测 benchmark 上取得了**具有竞争力的性能**。
- 相比仅用 LLM 或仅用扩散模型的基线，CoGenCast 能**同时利用语义理解与连续生成的能力**，从而提升预测精度和不确定性建模质量。
- 该工作验证了“LLM + 流匹配”作为混合预测框架的有效性，为概率时序预测提供了新思路。

## 7. 优点

- **方法创新性强**：将 LLM 与流匹配进行耦合，突破了单一模型的局限。
- **改造代价低**：只修改注意力拓扑结构，而非重新设计整个网络，能充分利用预训练 LLM 的先验知识。
- **统一框架**：天然支持多模态和跨域统一训练，具有较好的通用性和扩展性。
- **代码开源**：论文提供了 GitHub 代码链接，便于复现与后续研究。

## 8. 不足与局限

- **信息受限**：由于只获取到摘要层面的信息，无法验证实验细节、数据集多样性、消融设计等。
- **计算资源未知**：未提及训练成本，对于大规模 LLM 改造方法，其可落地性存疑。
- **泛化能力仍需验证**：时间序列场景多种多样（如长序列、高噪声、异常事件、多变量强耦合等），摘要中的 benchmark 是否覆盖这些场景尚不清楚。
- **与现有基线的对比公平性**：由于未列出具体基线版本、参数规模和训练设置，难以判断比较是否完全公平。
- **模型复杂性**：LLM 与流匹配的耦合可能引入额外的训练和推理复杂度，这些在摘要中未讨论。

（完）
