# 03 · 会议论文写作（含 ICASSP）

> 会议论文的精髓：在**有限篇幅**内，把"一个新想法 + 初步验证"讲成一个完整、可信、好读的故事。本章以信号处理顶会 **ICASSP** 为主线（4 页双栏、双盲），方法论对多数计算机/工科会议通用。

## 一、会议论文的定位

会议看重 **创新性想法 + 初步验证**，周期短、迭代快；期刊看重完整性与充分实验（见 [04](./04-journal-paper.md)）。会议论文录用后通常被 IEEE Xplore / ACM DL 收录，EI/Scopus 检索。

以 ICASSP 为例的硬约束：

| 项目 | 要求 |
|---|---|
| 篇幅 | 正文最多 **4 页**（双栏），参考文献通常不计入但也要克制 |
| 模板 | IEEE 双栏（IEEEtran），**别自己拼样式** |
| 评审 | **双盲**（审稿人不知道你是谁，你也不知道审稿人） |
| 图表 | 矢量优先（PDF/EPS），位图 ≥ 300 dpi |
| 提交 | 需通过 **IEEE PDF eXpress** 校验后再上传投稿系统 |

> ⚠️ 确切的截稿日、页数政策、是否双盲，**每年以官方 Author Kit 为准**。相关官方入口见文末。

## 二、逐节写作精讲

> 推荐写作顺序：**方法 → 实验 → 引言 → 摘要 → 结论 → 相关工作 → 标题**。先把最难讲清的方法写出来，其它都是它的"包装"。

### 1. 标题 Title
用 12–15 个词说清 **方法 + 任务 + 亮点**，让审稿人 3 秒懂你在做什么。

- ✅ 含具体方法/模型名、含任务、突出增益或特性（real-time / lightweight）。
- ❌ 空泛（"A New Method for Audio"）、过度营销（"Revolutionary…"）、堆未解释的缩写。
- 套路：**`[方法名]: [机制/亮点] for [任务]`**
- 例：*Lightweight Dual-Path Conformer for Real-Time Monaural Speech Enhancement*
- 📖 范文参考：Conv-TasNet、Conformer、FullSubNet（见 [06 范文精读](./06-paper-examples.md)）。

### 2. 摘要 Abstract
150–250 词、单段。固定骨架：**背景/问题 → 现有不足 → 你的方法 → 主要结果 → 结论意义**。

```
Background: Speech enhancement in low-SNR conditions remains challenging due to ...
Method:     We propose a ..., which leverages ... to ...
Result:     Experiments on ... show an improvement of X% over the best baseline in ...
```

- **把你最硬的那个数字提前到摘要**（如 "SI-SNR +X dB"），别写 "significantly better"。
- 双盲：别写 "In our previous work we…"，改用 "Prior work [1] showed…" 并匿名化引用。

### 3. 引言 Introduction
审稿人最先精读的部分。黄金结构：**背景 → 前作不足(gap) → 我们的做法 → 编号贡献**。

1. 研究背景与重要性（为什么值得做）。
2. 问题陈述与现有方法的不足（具体、可引用，别泛泛）。
3. 本文做法（顺势引出方法）。
4. **用编号列表列出 3–4 条贡献**（ICASSP 评审最看重）。
5. 一句话带过论文结构。

```
Motivation:   Recently, ... has attracted growing attention because ...
Gap:          However, existing approaches struggle to ..., mainly because ...
Contribution: The main contributions of this work are: (i) ... (ii) ... (iii) ...
```

> 贡献要写成"我们做了什么 + 带来什么"，每条都要在正文有对应证据。
> 📖 范文参考：Conformer 的引言动机推导堪称教科书级。

### 4. 相关工作 Related Work
按 **"研究路线/主题"** 而非"一篇一句"来组织，每组结尾点出与本文的不同。

```
Categorize:   Prior studies can be broadly divided into three lines: ..., ..., and ...
Differentiate: Unlike [A] that focuses on ..., our method addresses ... by ...
```

- 只引最相关的代表作，别写成致谢名单。
- 双盲期引用自己用匿名编号，录用后补全称。

### 5. ��法 Proposed Method
论文的心脏。固定顺序：

1. **问题形式化**：定义符号（`x` 观测、`s` 目标、`θ` 参数），全文统一。
2. **总览图**：用一张 block diagram 让读者 10 秒看懂系统。
3. **逐模块讲**：关键公式编号，并用一句话解释直觉，别只甩公式。
4. **亮点前置**：参数量小/复杂度低就主动说明（ICASSP 加分项）。

```
Formalize: Let x ∈ R^T denote the observed signal; our goal is to estimate s from x.
Explain:   Intuitively, the attention module lets the network focus on ...
```

### 6. 实验 Experiments
回答"你的贡献是否被验证"。必备拼图（详见 [02 实验章](./02-experiment.md)）：数据集、指标、基线、主结果表（加粗最优）、消融、深入分析。

```
Result: As shown in Table 1, our method outperforms ... by X dB in SI-SNR
        while using 30% fewer parameters.
```

- ❌ 别踩坑：只报有利指标、换测试集比较、不报方差/置信区间。

### 7. 结论 Conclusion
1 段即可：**重述核心贡献 → 主要发现 → 局限与未来工作**，**绝不引入新结果**。

```
Closing: We presented ..., demonstrating that ... . Future work includes extending ... to ...
```

- 别复读摘要。把"我们做了 X"升级成"我们证明了 X 能带来 Y，这说明 Z"。

### 8. 参考文献 References
用 **BibTeX + IEEEtran** 自动生成最稳。每条信息完整可检索；正文引用与列表一致，无孤儿引用；双盲期匿名化自身引用，Camera-ready 补回。

## 三、双盲（Double-blind）红线

| 要做 | 别做 |
|---|---|
| 用编号引用自己工作（"[1]"） | 写 "our prior work [1]" 暴露身份 |
| 致谢、基金先留空或写 anonymous | 在页眉/脚注/致谢写机构或姓名 |
| arXiv 预印本投稿时不附可识别链接 | 在 PDF 元数据里留作者名（PDF eXpress 会查） |

## 四、常见 desk reject 原因

超页、非双栏模板、PDF 含作者信息、图表不可读、与会议范围不符。**投稿前务必走一遍 [投稿检查清单](../templates/submission-checklist.md)。**

## 五、提交流程（通用）

1. **用官方模板写作** —— 下载 IEEEtran 模板，别自己拼样式。
2. **生成 PDF** —— LaTeX 最稳；Word 用户用官方 .doc 模板。
3. **PDF eXpress 校验** —— 上传校验合规（字体嵌入、无作者元数据），下载合规 PDF。
4. **投稿系统提交** —— 填领域、上传 PDF 与补充材料，确认双盲无误。

配套：[IEEE 会议论文 LaTeX 骨架](../templates/ieee-conference-skeleton.tex) 可直接改用。

## 📎 官方资源（投稿前逐个核对最新要求）

| 资源 | 说明 | 链接 |
|---|---|---|
| ICASSP 官网 | Author Kit、截稿日、双盲要求发布处（按年份，如 2027 会议） | https://2027.ieeeicassp.org/ |
| IEEE 模板选择器 | 官方 IEEEtran 双栏模板 | https://template-selector.ieee.org/ |
| IEEE PDF eXpress | 投稿前合规校验（强制） | https://ieee-pdf-express.org/ |
| IEEE 信号处理学会 | 会议总索引与政策 | https://signalprocessingsociety.org/ |

> 会议网址沿用 `年份.ieeeicassp.org` 规律；若打不开，到 IEEE SPS 或搜索引擎搜 "ICASSP 20XX Author Kit" 获取最新入口。**一切以官方当年页面为准。**

## 本章 Checklist

- [ ] 标题含方法+任务+亮点，摘要把最硬的数字前置。
- [ ] 引言用编号列出 3–4 条贡献，每条正文有证据。
- [ ] 方法有形式化 + 总览图 + 逐模块直觉解释。
- [ ] 实验含公平 baseline、消融、深入分析。
- [ ] 全文通过双盲检查，无身份泄漏。
- [ ] 用官方模板，PDF 过 eXpress 校验，未超页。

**相关**：[06 范文精读](./06-paper-examples.md) · [07 句式库](./07-academic-english.md) · [下一站 → 04 期刊论文](./04-journal-paper.md)
