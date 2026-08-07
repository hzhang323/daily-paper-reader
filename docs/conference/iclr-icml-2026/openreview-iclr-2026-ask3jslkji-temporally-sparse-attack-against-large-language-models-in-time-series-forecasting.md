---
title: Temporally Sparse Attack against Large Language Models in Time Series Forecasting
title_zh: 针对大语言模型时间序列预测的时间稀疏攻击
authors: "Fuqiang Liu, Sicong Jiang"
date: 2025-09-20
pdf: "https://openreview.net/pdf?id=ASK3jSLkJi"
tags: ["query:time-series"]
score: 7.0
evidence: 针对基于LLM的时间序列预测进行时间稀疏扰动攻击与分析
tldr: 大语言模型在零样本时间序列预测中表现出潜力，但现有攻击方法需要扰动整个序列，不符合实际场景。该文提出时间稀疏攻击，限制扰动的时刻数量，将攻击建模为基数约束优化，并设计基于子空间追踪的高效算法。实验表明仅修改少量时间点就能显著降低LLM预测性能。该工作为评估和提升LLM时序预测的鲁棒性提供了重要参考。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: LLM时间序列预测对输入扰动敏感，而现有攻击方法需要改动整个序列，实用性差，需要稀疏攻击方法。
method: 提出时间稀疏攻击（TSA），将攻击形式化为基数约束优化问题，并用子空间追踪算法求解，仅扰动有限时间点。
result: 实验显示在极少时间点扰动即可显著破坏LLM预测，揭示了其脆弱性。
conclusion: TSA为鲁棒LLM时序预测研究提供了评估工具，也提示需要防御稀疏扰动。
---

## Abstract
Large Language Models (LLMs) have recently demonstrated strong potential in zero-shot time series forecasting by leveraging their ability to capture complex temporal patterns through the next-token prediction mechanism. However, recent studies indicate that LLM-based forecasters are highly sensitive to small input perturbations. Existing attack methods, though, typically require modifying the entire time series, which is impractical in real-world scenarios. To address this limitation, we propose a Temporally Sparse Attack (TSA) against LLM-based time series forecasting. We formulate the attack as a Cardinality-Constrained Optimization Problem (CCOP) and introduce a Subspace Pursuit (SP)--based algorithm that restricts perturbations to a limited subset of time steps, enabling efficient and effective attacks. Extensive experiments on state-of-the-art LLM-based forecasters, including LLMTime (GPT-3.5, GPT-4, LLaMa, and Mistral), TimeGPT, and TimeLLM, across six diverse datasets, demonstrate that perturbing as little as 10% of the input can substantially degrade forecasting accuracy. These results highlight a critical vulnerability of current LLM-based forecasters to low-dimensional adversarial attacks.

---

## 论文详细总结（自动生成）

# 针对大语言模型时间序列预测的时间稀疏攻击（Temporally Sparse Attack, TSA）——论文总结

## 1. 核心问题与研究动机

- **背景**：大语言模型（LLM）通过 next-token prediction 机制可以捕捉复杂的时间依赖模式，在零样本时间序列预测中展现出较强潜力。
- **已有问题**：现有研究表明，基于 LLM 的预测器对输入的小幅扰动非常敏感；但已有攻击方法通常需要**修改整条时间序列**，这在真实场景中不现实。
- **核心问题**：能否在**仅扰动少量时间步**的条件下，依然显著破坏 LLM 的预测性能？
- **整体含义**：本文提出 **时间稀疏攻击（TSA）**，将攻击建模为**基数约束优化问题**，通过**子空间追踪**高效求解，证明 LLM 时间序列预测器存在“低维对抗脆弱性”——只需攻击 10% 的输入时间点即可大幅降低预测精度。

## 2. 方法论

- **核心思想**：限制被扰动的时间点数量，而不是限制扰动幅度或扰动总量；即要求攻击向量在时间维上具有稀疏性。
- **问题建模**：将攻击形式化为 **Cardinality-Constrained Optimization Problem（CCOP）**：
  - 目标：在给定扰动预算下，最大化 LLM 预测误差；
  - 约束：被扰动的时间步数量不超过某个阈值 K。
- **求解算法**：采用压缩感知/稀疏恢复中常用的 **Subspace Pursuit（SP）** 算法进行求解。
  - 初始化：选择当前对预测误差影响最大的 K 个时间步作为初始支撑集；
  - 迭代：根据梯度或相关性信息扩展候选时间步集合；
  - 更新：在候选集上求解最小二乘/优化子问题；
  - 剪枝：只保留 K 个最重要的时间步；
  - 重复直到收敛或达到最大迭代次数。
- **实际效果**：该算法可在保证攻击稀疏性的同时，高效逼近最优稀疏扰动，避免穷举搜索。

## 3. 实验设计

- **攻击目标模型**：
  - LLMTime（使用 GPT-3.5、GPT-4、LLaMa、Mistral 作为底层大模型）；
  - TimeGPT；
  - TimeLLM。
- **数据集**：使用了 **6 个不同领域/类型的数据集**，但摘要中未给出具体数据集名称。
- **基准与对比**：
  - 主要验证 TSA 在不同模型、不同数据集上能否以稀疏扰动显著降低预测精度；
  - 摘要未明确列出与 dense attack、随机扰动、其他稀疏攻击方法的具体对比细节。
- **关键实验结论**：仅扰动 **10% 的输入时间点** 即可显著降低多个 LLM 预测器的预测准确性。

## 4. 资源与算力

- 摘要和提供的元数据中**未明确说明**使用的 GPU 型号、数量、训练/推理时长、以及具体计算成本。
- 因此，无法从现有信息评估该方法的计算开销和实际部署成本。

## 5. 实验数量与充分性

- **实验规模**：覆盖 6 个数据集和 6 类 LLM 预测器配置（LLMTime 的 4 种底层模型 + TimeGPT + TimeLLM），整体覆盖面较广。
- **充分性分析**：
  - 优点：模型种类较多，包含 API 型模型和开源模型，数据集多样化；
  - 不足：摘要中缺少对扰动比率、攻击成功率、运行时间、防御基线等维度的系统分析；
  - 公平性：未提供细节说明是否统一了时序数据预处理、预测长度、扰动范围等实验条件，因此**公平性难以完全验证**；
  - 缺少更全面的消融实验，例如不同 K 值的影响、不同优化初始化的稳定性、以及对抗防御实验。

## 6. 主要结论

- 基于 LLM 的时间序列预测器虽然性能强大，但**对低维/稀疏对抗扰动非常脆弱**；
- 攻击者无需控制整条历史序列，只需要修改少量时间点即可造成预测精度显著下降；
- TSA 为评估 LLM 时序预测鲁棒性提供了一种高效、实用的攻击工具；
- 该结果提示未来需要针对稀疏扰动设计有效的防御机制。

## 7. 优点

- **问题设置更贴近现实**：稀疏攻击比全序列扰动更具实际威胁和可操作性；
- **方法高效**：将稀疏攻击建模为 CCOP，并用 Subspace Pursuit 求解，避免了穷举和全维度优化；
- **验证面较广**：同时涵盖 GPT-3.5/GPT-4、LLaMa、Mistral、TimeGPT、TimeLLM 等主流 LLM 预测器；
- **结论清晰**：指出了“低维对抗攻击”这一新的安全威胁，为后续鲁棒性研究提供了有价值的切入点。

## 8. 不足与局限

- **信息不完整**：由于可获得的材料仅为摘要和元数据，缺少完整论文细节，如具体数据集、攻击参数、实验配置等；
- **缺乏基线对比细节**：未明确与全序列攻击、随机稀疏扰动、其他稀疏优化方法进行系统对比；
- **缺少防御研究**：论文仅提出攻击方法，没有讨论缓解方案或对抗训练策略；
- **评估指标单一**：主要关注预测精度下降，未涉及模型不确定性、对抗样本可迁移性、攻击隐蔽性等；
- **应用限制**：未讨论在真实在线预测系统中的攻击代价、时间步可篡改性限制，以及不同时间序列粒度下的适用性；
- **来源状态**：根据元数据，该论文来源标注为 `ICLR-2026-Rejected-Public`，可能未经顶级会议最终接收，因此在引用结论时应谨慎看待。

（完）
