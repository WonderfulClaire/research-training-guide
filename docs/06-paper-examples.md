# 06 · 优秀论文范文精读

> 写不出来，往往是因为看得太少。这里精选 10 篇信号处理/语音领域的标杆论文，先整体推荐，再按"标题 → 结论"每个写作模块告诉你：读哪几篇、看它的哪一节、具体学什么。

## 读范文的三个层次

1. **抄结构**：看它每一节先写什么后写什么、贡献怎么列、图表怎么摆。
2. **抄句式**：把它表达动机/对比/结果的英文句型记下来（配合 [07 句式库](./07-academic-english.md)）。
3. **抄思路**：看它如何把一个想法讲成"问题 → 方法 → 证据"的完整故事。

> ✅ **抄结构和句式不算抄袭，抄内容才算。** 双盲评审与 IEEE 都会查重，严禁照抄文字与图表。

## 精选范文库（10 篇 · 点开就能读）

| 论文 | 领域 | 会议/期刊 | 为什么值得学（重点看哪） | 链接 |
|---|---|---|---|---|
| **Attention Is All You Need** | 奠基 | NeurIPS 2017 | 摘要如何一句话立住"全新架构"；方法如何用图+公式讲清 self-attention | [arXiv](https://arxiv.org/abs/1706.03762) |
| **Conformer** | 语音识别 | Interspeech 2020 | 引言的动机推导（CNN 强局部、Transformer 强全局→融合）+ 方法模块图 | [arXiv](https://arxiv.org/abs/2005.08100) |
| **Conv-TasNet** | 语音分离 | TASLP 2019 | 方法一张图讲清 encoder–separator–decoder；实验用 SI-SNR 数字"超越理想掩蔽" | [arXiv](https://arxiv.org/abs/1809.07454) |
| **Dual-Path RNN (DPRNN)** | 语音分离 | ICASSP 2020 | 用极简结构讲清一个巧思；消融怎么证明每步有用（典型 4 页佳作） | [arXiv](https://arxiv.org/abs/1910.06379) |
| **SepFormer** | 语音分离 | ICASSP 2021 | 引言如何在有限篇幅快速定位 gap；相关工作如何按"路线"归类 | [arXiv](https://arxiv.org/abs/2010.13154) |
| **wav2vec 2.0** | 自监督 | NeurIPS 2020 | 摘要如何讲"少量标注也能强"的卖点；背景如何梳理自监督这条线 | [arXiv](https://arxiv.org/abs/2006.11477) |
| **HiFi-GAN** | 语音合成 | NeurIPS 2020 | 方法如何用生成器/多尺度判别器结构图讲清设计；实验同时报音质与速度 | [arXiv](https://arxiv.org/abs/2010.05646) |
| **FullSubNet** | 语音增强 | ICASSP 2021 | 标题如何塞进机制+实时约束+任务；实验用公认挑战赛与指标站住结果 | [arXiv](https://arxiv.org/abs/2010.15508) |
| **Tacotron 2** | 语音合成 | ICASSP 2018 | 引言如何交代动机与前作不足；方法如何把两阶段系统讲清楚 | [arXiv](https://arxiv.org/abs/1712.05884) |
| **Whisper** | 大规模 ASR | OpenAI 2022 | 摘要/引言如何讲"数据规模驱动"的叙事；实验如何用多数据集证明鲁棒性 | [arXiv](https://arxiv.org/abs/2212.04356) |

> 若某链接打不开，复制论文的**确切英文标题**去 [Google Scholar](https://scholar.google.com) 或 [IEEE Xplore](https://ieeexplore.ieee.org) 搜索即可命中。

## 分模块范文对照（重点看这里）

### 标题 Title
- **读**：Conv-TasNet（好记名字 + 强主张）、Conformer（机制本质 + 任务）、FullSubNet（机制 + real-time 约束 + 任务）。
- **观察**：范文都给方法起了短名字方便被引用、标题里能读出任务、点出一个亮点。
- **套路**：`[方法名]: [机制/亮点] for [任务]`。

### 摘要 Abstract
- **读**：Conv-TasNet（数字碾压 baseline）、wav2vec 2.0（少标注也能强）、Whisper（大规模数据驱动叙事）。
- **观察**：好摘要几乎同一个骨架——① 任务与痛点 ② 方法核心（We propose … which …）③ 最强结果（一个具体数字）④ 结论意义。
- **启发**：Conv-TasNet 把"超越理想时频掩蔽"这个反直觉强结果放进摘要——**把你最硬的数字提前**。

### 引言 Introduction
- **读**：Conformer（动机推导教科书级）、SepFormer（有限篇幅快速定位 gap）、Tacotron 2（交代前作不足）。
- **观察 Conformer 引言的推进逻辑**：
  1. Transformer 擅长全局依赖，但局部建模弱；
  2. CNN 擅长局部，但缺全局视野；
  3. **Gap：两者优势没被结合**；
  4. **本文：把卷积塞进 Transformer，兼得两者** → 引出方法；
  5. 编号列出贡献。
- **黄金模板**：`背景 → 前作不足(gap) → 我们的做法 → 编号贡献`。

### 相关工作 Related Work
- **读**：wav2vec 2.0、SepFormer 的 related work / background。
- **范文做法**：按"研究路线"分组（时频域/时域/自监督）、每组结尾点出"与本文的不同"、只引最相关代表作。
- **句式**：`Prior work can be broadly grouped into three lines: …` / `Unlike [A], which relies on …, our method instead …`

### 方法 Proposed Method
- **读**：Conv-TasNet（一张图讲清 encoder–separator–decoder）、Conformer（模块图+公式）、HiFi-GAN（生成器/多判别器结构图）。
- **固定顺序**：① 问题形式化（定义符号，全文统一）② 总览图（10 秒看懂系统）③ 逐模块讲（公式编号 + 一句直觉）④ 亮点前置（参数量小/复杂度低主动说）。

### 实验 Experiments
- **读**：Conv-TasNet（主表 + 消融）、FullSubNet（DNS Challenge 标准评测）、Whisper（多数据集零样本）。
- **必备拼图**：数据集（公认公开集）、指标（领域公认并注明）、基线（近 3 年 SOTA + 经典）、主表（加粗最优，配参数量列）、消融（逐个去模块）、分析（收敛曲线/案例/失败样例）。
- **范文的诚实**：会报参数量、会在不占优的指标上如实标注。只挑有利指标、换测试集比、不报方差——审稿人一眼看穿。

### 结论 Conclusion
- **读**：Conformer、Conv-TasNet 的结论。
- **观察**：几乎都是一段、三件事——重述核心贡献、点出最强结果、诚实给局限与未来工作，**绝不引入新结果**。
- **技巧**：别复读摘要。把"我们做了 X"升级成"我们证明了 X 能带来 Y，这说明 Z"。

## 去哪找更多范文（自己扩充）

| 渠道 | 用途 | 链接 |
|---|---|---|
| **Papers With Code · Speech** | 按任务看 SOTA 排行榜，每条带论文+代码 | https://paperswithcode.com/area/speech |
| **IEEE Xplore · ICASSP 论文集** | 直接翻往年录用论文，最贴近目标会议写法 | https://ieeexplore.ieee.org/xpl/conhome/1000002/all-proceedings |
| **Semantic Scholar** | 按标题搜，看高被引"施引文献"顺藤摸瓜 | https://www.semanticscholar.org/ |
| **arXiv · eess.AS** | 音频/语音最新预印本，掌握当前谁在做什么 | https://arxiv.org/list/eess.AS/recent |

> 💡 想要**你自己方向**（CV / NLP / 生物信息…）的范文库？欢迎照本章格式提 PR 补充，见 [CONTRIBUTING](../CONTRIBUTING.md)。

**相关**：[03 会议论文](./03-conference-paper.md) · [07 句式库](./07-academic-english.md)
