---
title: SEGMENTED CONFIDENCE SEQUENCES AND MULTISCALE ADAPTIVE CONFIDENCE SEGMENTS FOR ANOMALY DETECTION IN NONSTATIONARY TIME SERIES
title_zh: 分段置信序列与多尺度自适应置信段：非平稳时间序列的异常检测
authors: "Aditi Gautam, Muyan Li"
date: 2025-09-04
pdf: "https://openreview.net/pdf?id=9qXMe8XKvN"
tags: ["query:time-series"]
score: 9.0
evidence: 非平稳时间序列的异常检测自适应阈值方法
tldr: 针对非平稳时间序列中统计特性漂移导致静态阈值失效的问题，提出分段置信序列（SCS）与多尺度自适应置信段（MACS）两种自适应阈值框架。通过在线学习与分段原则实现局部上下文敏感的阈值调整，并在控制误报率的前提下提升异常检测鲁棒性。实验验证了该方法在概念漂移和制度切换场景下的有效性，为基础设施监控等领域的实时异常检测提供了可靠工具。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 传统静态阈值在非平稳环境下因漂移而失效，难以适应制度切换和多尺度变化。
method: 提出分段置信序列(SCS)和多尺度自适应置信段(MACS)，结合在线学习与分段原理生成局部自适应阈值。
result: 实验表明该方法能维持误报率保证并适应非平稳特性，优于传统阈值方法。
conclusion: 为制造、IT和基础设施监测中的非平稳时间序列异常检测提供了可靠的在线自适应方案。
---

## Abstract
As time series data become increasingly prevalent in domains such as manufacturing, IT, and infrastructure monitoring, anomaly detection must adapt to nonstationary environments where statistical properties shift over time. Traditional static thresholds are easily rendered obsolete by regime shifts, concept drift, or multi-scale changes. To address these challenges, we introduce and empirically evaluate two novel adaptive thresholding frameworks: Segmented Confidence Sequences (SCS) and Multi-Scale Adaptive Confidence Segments (MACS). Both leverage statistical online learning and segmentation principles for local, contextually sensitive adaptation, maintaining guarantees on false alarm rates even under evolving distributions. Our experiments across Wafer Manufacturing benchmark datasets show significant F1-score improvement compared to traditional percentile and rolling quantile approaches. This work demonstrates that robust, statistically principled adaptive thresholds enable reliable, interpretable, and timely detection of diverse real-world anomalies.

---

## 论文详细总结（自动生成）

# SEGMENTED CONFIDENCE SEQUENCES AND MULTISCALE ADAPTIVE CONFIDENCE SEGMENTS FOR ANOMALY DETECTION IN NONSTATIONARY TIME SERIES — 论文总结

## 1. 核心问题与研究动机

- **背景**：时间序列数据在制造、IT、基础设施监控等领域日益普及，异常检测需求迫切。现实中的系统往往处于**非平稳环境**，数据统计特性（如均值、方差、分布形态）会随时间发生漂移。
- **核心困难**：传统静态阈值（如固定百分位数）在概念漂移（Concept Drift）、制度切换（Regime Shift）或多尺度变化面前会迅速失效，导致误报率失控或漏检率上升。
- **研究目标**：设计一种能够适应非平稳环境的**自适应阈值框架**，在统计特性不断演变的情况下保持对误报率的可控保证，同时提升异常检测的F1分数。

## 2. 方法论

- **总体思路**：将**统计在线学习**与**分段原则（Segmentation）** 相结合，不依赖全局固定阈值，而是在局部时间窗口内构建上下文敏感的置信边界。
- **Segmented Confidence Sequences (SCS) 分段置信序列**：
  - 核心思想：将流式时间序列划分为若干段（Segment），在每一段上利用置信序列（Confidence Sequence）理论在线构建逐点置信边界，作为异常判定阈值。
  - 关键机制：通过分段，使阈值能跟随局部统计特性的变化；置信序列保证在任意停止时间下误报率有理论上的上界。
- **Multi-Scale Adaptive Confidence Segments (MACS) 多尺度自适应置信段**：
  - 核心思想：在SCS基础上引入**多尺度**视角，同时考虑不同长度时间窗口下的统计特征，以适应不同持续时间的异常模式。
  - 关键机制：多个尺度并行构建置信段，最终联合形成自适应阈值，兼顾短期波动与长期趋势变化。
- **误报率保证**：两种方法均从统计推断理论出发，在分布变化的情况下仍维持对假阳性率的理论保证，而非仅靠经验调参。
- **算法流程（文字说明）**：接收流式数据 → 在线估计当前窗口的分布特征 → 根据置信序列理论构造该窗口的自适应阈值区间 → 将观测值与阈值比较判断是否异常 → 随着新数据到来滚动更新分段与阈值。

## 3. 实验设计

- **数据集**：使用了 **Wafer Manufacturing benchmark datasets**（晶圆制造基准数据集），该数据集来自真实工业场景中的非平稳时间序列异常检测任务。
- **对比方法**：
  - 传统百分位阈值法（Percentile approach）
  - 滚动分位数法（Rolling quantile approach）
  - 以及所提出的 SCS 与 MACS
- **评估指标**：主要报告 **F1-score**，兼顾精确率与召回率。

## 4. 资源与算力

- **原文未明确说明**所使用的GPU型号、数量、训练时长等算力信息。
- 从方法性质推断（统计在线学习与分段推断），计算开销通常远低于深度学习模型，但该推测在原文中并未给出具体量化数据。

## 5. 实验数量与充分性

- 实验在晶圆制造基准数据集上进行了评估，对比了传统百分位与滚动分位数方法。
- **充分性评估**：
  - ✅ 优点是使用了真实工业基准数据，具备一定的实践参考价值。
  - ⚠️ 不足是**实验覆盖较窄**——仅有一个领域（晶圆制造）的数据集，未涵盖IT监控、金融、传感器网络等其他常见非平稳时间序列场景。
  - ⚠️ 未提及消融实验（如SCS单独 vs MACS单独 vs 两者结合），也未见对参数敏感性、不同漂移类型（突变 vs 渐变）的系统性测试。

## 6. 主要结论与发现

- 所提出的 SCS 与 MACS 在晶圆制造基准数据集上，相较传统百分位和滚动分位数阈值方法取得了**显著的F1-score提升**。
- 两种方法在非平稳环境下能够**保持误报率保证**，验证了统计原则性自适应阈值的有效性。
- 研究表明：结合统计在线学习与分段原则的自适应阈值方法，能够在概念漂移和制度切换场景下提供**可靠、可解释、及时**的异常检测能力。

## 7. 优点

- **理论保证强**：置信序列方法提供了误报率上限的理论支撑，相比纯启发式阈值更具统计学严谨性。
- **适应性好**：分段与多尺度机制天然适配非平稳、制度切换场景，打破静态阈值局限。
- **可解释性**：阈值生成过程的统计原理清晰，便于在实际运维中理解和部署。
- **计算友好**：基于在线学习与分段推断，避免大规模训练，适合实时推理场景。
- **实践导向**：选用的晶圆制造数据集来自真实工业场景，既有学术意义也有应用价值。

## 8. 不足与局限

- **实验验证范围有限**：仅报告单一领域数据集的结果，缺乏对通用性的多数据集验证；对非平稳的“类型”（概念漂移、季节变化、突发性制度切换等）没有细分评估。
- **对比方法偏弱**：仅与传统的百分位/滚动分位数对比，未与近年其他自适应检测方法（如基于在线高斯过程、贝叶斯变点检测、深度异常检测等）进行比较，说服力有限。
- **缺少超参数敏感性分析**：分段长度、多尺度窗口大小等关键超参数的敏感性未知，影响方法的易用性。
- **算力与效率未量化**：未给出实际运行时间或资源消耗数据，无法判断其在极大规模流式场景下的可行性。
- **理论细节未充分展开**：从摘要可见误报率保证这一关键论点的存在，但具体推导、前提条件（如对漂移幅度的假设）并未在论文正文中加以展开说明。

（完）
