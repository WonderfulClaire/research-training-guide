# 04 · 期刊论文写作

> 如果说会议论文是"精彩的短片"，期刊论文就是"完整的长篇电影"。它要求更系统的论证、更充分的实验、更深入的分析——以及一场你必须打赢的仗：**审稿回复（rebuttal）**。

## 一、期刊 vs 会议：到底差在哪

| 维度 | 会议论文 | 期刊论文 |
|---|---|---|
| 核心 | 新想法 + 初步验证 | 完整系统 + 充分论证 |
| 篇幅 | 短（如 4 页） | 长（十几到几十页），可含附录 |
| 实验 | 够证明想法即可 | 全面、多数据集、深入分析 |
| 相关工作 | 精简 | 系统、成体系的综述式回顾 |
| 周期 | 短（4–6 个月） | 长（半年到两年，多轮修改） |
| 评审 | 常一轮、双盲、有时有 rebuttal | 多轮 major/minor revision |
| 结果 | Accept / Reject | Accept / Minor / Major / Reject |

**常见路径**：先投会议快速发布核心想法 → 扩展成期刊版（extended version），补充完整实验、更多分析、更系统的相关工作。注意扩展版通常要求**相对会议版有实质性新增内容**（常见门槛是 30%+ 新内容），且要在文中声明与会议版的关系。

## 二、期刊论文的结构（比会议更完整）

典型 IMRaD 结构，各部分比会议版更厚：

1. **Abstract / Introduction** —— 同会议逻辑（见 [03](./03-conference-paper.md)），但引言可更从容地铺陈背景与动机。
2. **Related Work** —— 系统的文献综述，梳理整个领域的脉络与流派，不只是"划定位置"。
3. **Method** —— 完整的方法论，含所有细节、推导、复杂度分析，让人能复现。
4. **Experiments** —— 多数据集、多指标、充分消融、敏感性分析、失败案例、可视化。
5. **Discussion**（期刊常单列）—— 结果意味着什么、为什么有效、局限、适用边界。这是期刊区别于会议的深度所在。
6. **Conclusion** —— 总结贡献与未来工作。
7. **Appendix / Supplementary** —— 额外证明、超参、更多实验。

> 期刊审稿人尤其看重 **Discussion**：会议论文可以"展示结果就走"，期刊论文要"解释清楚现象背后的道理"。

## 三、选刊（Target Journal）：投对地方赢一半

选刊错误会导致 desk reject 或长期拖延。评估维度：

| 维度 | 怎么看 |
|---|---|
| **范围（Scope）** | 你的主题是否属于该刊 Aims & Scope？看它近期发了哪些相似论文。 |
| **档次与影响力** | 影响因子（IF）、中科院分区、CCF 分级、领域口碑，综合看别唯 IF。 |
| **审稿周期** | 有些刊快（几个月），有些慢（一年以上）。看官网或 [SciRev](https://scirev.org) 等社区反馈。 |
| **开放获取（OA）** | 是否收 APC（版面费）？金色 OA 通常要付费，注意预算。 |
| **读者群** | 你希望谁读到？投到你目标读者常看的刊。 |

**警惕掠夺性期刊（Predatory Journal）**：承诺"快速录用+收高额费用"、编委名单可疑、疯狂约稿的，多半是坑。可查 [DOAJ](https://doaj.org)（正规 OA 白名单）反向验证。

**信号处理 / 音频领域常见目标刊**（示例，非排名）：
- IEEE/ACM Transactions on Audio, Speech, and Language Processing (TASLP)
- IEEE Transactions on Signal Processing (TSP)
- IEEE Signal Processing Letters（短文，快）
- Speech Communication、EURASIP Journal on Audio, Speech, and Music Processing

> 用 [JournalFinder](https://journalfinder.elsevier.com) / [Journal Suggester](https://journalsuggester.springer.com) 等工具，把你的摘要贴进去，可辅助匹配候选刊。

## 四、审稿回复（Rebuttal / Response to Reviewers）：决定生死的一战

收到 Major/Minor revision **是好消息**——意味着有机会。回复信写得好坏，直接决定能否被接受。

### 黄金原则

1. **逐条回应，一条都不漏**。把每位审稿人的每个意见单独列出，紧跟你的回复。
2. **礼貌、专业、感恩**。开头感谢审稿人，即使意见很尖锐也别对抗。
3. **能改就改，改了要指明位置**。"We have revised … (see Section 3.2, page 5, highlighted in blue)"。
4. **不同意也要有理有据**。用数据、文献、逻辑说明，而不是嘴硬。可以部分让步 + 解释。
5. **正文用不同颜色标出修改**，方便审稿人快速核对（配合 [latexdiff](https://github.com/ftilmann/latexdiff)）。

### 回复模板（片段）

```
We thank the reviewers for their careful reading and constructive comments,
which have greatly helped us improve the manuscript. Below we address each
point individually. Reviewers' comments are in black; our responses are in blue.
Changes in the revised manuscript are highlighted in blue.

------------------------------------------------------------
Reviewer #1
------------------------------------------------------------
Comment 1.1: "The ablation study is insufficient ..."

Response: We thank the reviewer for this valuable suggestion. We have added
a new ablation study in Section 4.3 (Table 3), which shows that removing the
sub-band module degrades SI-SNR by 1.2 dB, confirming its contribution. The
relevant text is highlighted in blue on page 6.
```

> 完整可套用版本见 [审稿回复模板](../templates/rebuttal-template.md)。

### 应对不同意见的话术

| 场景 | 得体回应 |
|---|---|
| 要求补实验（合理） | 照做，并在信里贴出新结果表。 |
| 要求补实验（不合理/超范围） | 解释为何超出本文范围，可作为 future work，并补充力所能及的部分。 |
| 指出错误（真错了） | 大方承认并致谢，改正。 |
| 质疑创新性 | 明确对比最接近的工作，强调你的独特贡献与证据。 |
| 两位审稿人意见冲突 | 分别回应，说明你如何权衡，必要时请编辑裁决。 |

## 五、投稿到录用的流程

```
选刊 → 按 Author Guidelines 排版 → 写 Cover Letter → 在线投稿系统提交
  → (可能) desk review → 送审 → 收到审稿意见
  → Major/Minor Revision → 修改 + 写 rebuttal → 再次提交
  → (可能多轮) → Accept → 校样(proof) → 出版
```

**Cover Letter** 要点：一句话说清论文贡献、为什么适合该刊、声明无一稿多投与利益冲突、（若有）推荐/回避审稿人。

## 本章 Checklist

- [ ] 论文范围与目标刊的 Aims & Scope 匹配。
- [ ] 结构完整，含系统的相关工作与深入的 Discussion。
- [ ] 实验充分：多数据集、多指标、消融、分析。
- [ ] （若为会议扩展版）有实质性新增内容并已声明关系。
- [ ] Cover Letter 说清贡献与适配性。
- [ ] 收到 revision 后逐条回应、礼貌专业、改动标色。

**相关**：[03 会议论文](./03-conference-paper.md) · [rebuttal 模板](../templates/rebuttal-template.md) · [下一站 → 05 专利写作](./05-patent.md)
