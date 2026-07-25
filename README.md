<div align="center">

# 🧭 科研训练指南 · Research Training Guide

**从调研、实验到写作的完整科研训练手册 —— 论文（会议 / 期刊）与专利一网打尽。**

*A hands-on guide to the full research lifecycle: literature review → experiments → writing (conference / journal papers & patents).*

[![License: CC BY 4.0](https://img.shields.io/badge/License-CC%20BY%204.0-lightgrey.svg)](./LICENSE)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](./CONTRIBUTING.md)
[![Language](https://img.shields.io/badge/lang-中文-red.svg)](#)
[![Made for researchers](https://img.shields.io/badge/made%20for-researchers-blue.svg)](#)

</div>

---

## 这是什么

一份写给**研究生、青年研究者、以及第一次投稿/申请专利的人**的科研训练手册。它不只教你"怎么写论文"，而是把科研当成一条**完整的流水线**来训练：

> **选题调研 → 实验设计与执行 → 成果转化（会议论文 / 期刊论文 / 专利）**

内容以中文为主，句式与范例保留英文，覆盖信号处理、机器学习等方向，方法论对多数理工科通用。所有工具链接、范文链接均为真实可查资源。

## 为什么做这个

- 大部分科研技能是"师徒制口口相传"的暗知识，新人踩坑全靠运气。这份指南试图把这些暗知识**显式化、结构化、可复用**。
- 市面上要么是零散博客，要么是厚重教材。这里追求**能直接上手照做**：每章都有 Checklist、模板句式、Do/Don't 和可下载模板。
- 论文和专利常被割裂对待，但它们其实**同源异用**——本指南专门讲清两者的差异与衔接策略（尤其是"发表会破坏专利新颖性"这个致命坑）。

## 目录

| 阶段 | 章节 | 你会学到 |
|---|---|---|
| 🗺️ 总览 | [00 · 科研全流程总览](./docs/00-overview.md) | 一张图看懂科研从 0 到发表/授权的全过程 |
| 🔍 调研 | [01 · 文献调研与选题](./docs/01-literature-review.md) | 检索技巧、读论文三遍法、文献管理、如何找到好问题 |
| 🧪 实验 | [02 · 实验设计与执行](./docs/02-experiment.md) | 对照与消融、可复现性、baseline 与指标、实验工程化 |
| ✍️ 写作 | [03 · 会议论文写作（含 ICASSP）](./docs/03-conference-paper.md) | 逐节精讲、双盲规范、4 页会议论文的取舍 |
| ✍️ 写作 | [04 · 期刊论文写作](./docs/04-journal-paper.md) | 会议 vs 期刊、选刊、审稿回复（rebuttal）实战 |
| 📜 写作 | [05 · 专利写作](./docs/05-patent.md) | 三性、文件结构、权利要求撰写、论文 vs 专利 |
| 📖 素材 | [06 · 优秀论文范文精读](./docs/06-paper-examples.md) | 10 篇标杆论文，按写作模块逐节对照学 |
| 🗣️ 素材 | [07 · 学术英语与句式库](./docs/07-academic-english.md) | 分场景可直接抄用的高频句式 |
| 🧰 素材 | [08 · GitHub 科研工具箱](./docs/08-tools.md) | 文献/写作/排版/绘图/智能体精选开源工具 |

### 📎 可下载模板（[templates/](./templates)）

- [IEEE 会议论文 LaTeX 骨架](./templates/ieee-conference-skeleton.tex)
- [文献综述对比矩阵](./templates/literature-review-matrix.md)
- [实验记录日志模板](./templates/experiment-log.md)
- [发明专利申请模板](./templates/patent-application-template.md)
- [审稿回复（Rebuttal）模板](./templates/rebuttal-template.md)
- [投稿前检查清单](./templates/submission-checklist.md)

## 怎么用这份指南

**如果你是完全新手**：按 `00 → 01 → 02 → 03` 顺序读一遍，建立全局认知，再动手做自己的项目。

**如果你手上已有课题**：直接跳到对应阶段。比如"实验做完了要写论文"就看 `03`（会议）或 `04`（期刊）；"想把成果保护起来"就看 `05`（专利）。

**如果你想投 ICASSP**：`03` 是为你准备的，配合 `06` 范文精读 + `07` 句式库 + `templates/` 的 LaTeX 骨架和检查清单。

> 💡 **一句最重要的提醒**：如果你的成果既想发论文又想申专利，**一定先申请专利（或抢占申请日）再投稿**。论文一旦公开就会破坏专利新颖性，顺序错了专利就废了。详见 [05 · 专利写作](./docs/05-patent.md)。

## 路线图（Roadmap）

- [x] 科研全流程总览
- [x] 调研 / 实验 / 会议论文 / 期刊论文 / 专利 五大核心章
- [x] 范文精读、句式库、工具箱
- [x] 六套可下载模板
- [ ] 更多学科方向的范文库（CV / NLP / 生物信息 / 材料…）
- [ ] 英文版 README 与章节
- [ ] 审稿人视角：如何审一篇论文（reviewer 训练）
- [ ] 学术道德与 AI 使用规范专章

欢迎通过 Issue / PR 一起补全，尤其欢迎补充**你所在领域的范文和踩坑经验**。

## 贡献

非常欢迎贡献！无论是修正错别字、补充某个方向的范文、还是新增一整章，都请看 [CONTRIBUTING.md](./CONTRIBUTING.md)。

## 免责声明

- 本指南内容为**通用最佳实践**，不能替代各会议/期刊的官方 Author Kit、投稿系统说明，以及专利法律法规。投稿或申请前请以**官方当年文件**和**专业代理机构 / 律师意见**为准。
- 所有外部链接为编写时的公开资源，若失效请提 Issue。
- 学范文请**学结构、学句式、学讲故事的思路**；严禁照抄文字与图表，学术不端后果严重。

## 许可

本项目采用 [Creative Commons Attribution 4.0 International (CC BY 4.0)](./LICENSE) 许可。你可以自由分享和改编，只需署名。

---

<div align="center">
<sub>如果这份指南帮到了你，欢迎点一个 ⭐ Star，让更多科研新人看到。</sub>
</div>
