# 08 · GitHub 科研工具箱

> 精选的开源科研工具，覆盖调研到成稿的全流程。均为真实、活跃的开源项目。用对工具，能省下大量重复劳动，把精力留给真正的创新。

## 📚 文献管理与检索

| 工具 | 说明 | 链接 |
|---|---|---|
| **Zotero** ⭐必装 | 开源文献管理神器，一键抓取网页/PDF 元数据，配 Better BibTeX 直接导出 BibTeX | https://github.com/zotero/zotero |
| **JabRef** | 基于 BibTeX 的跨平台文献库管理，适合纯 LaTeX 工作流，条目干净可控 | https://github.com/JabRef/jabref |
| **Better BibTeX** | Zotero 插件，生成稳定 citation key（如 `vaswani2017attention`），避免引用错乱 | https://github.com/retorquere/zotero-better-bibtex |
| **arxiv-sanity-lite** | 轻量 arXiv 检索/排序/相似论文推荐，追最新进展比刷列表高效 | https://github.com/karpathy/arxiv-sanity-lite |
| **paperswithcode** | 论文+代码+榜单一站式，找 SOTA 基线和可复现实现 | https://github.com/paperswithcode/paperswithcode |
| **S2ORC** | AllenAI 大规模学术语料，做文献计量/自动综述的底层数据 | https://github.com/allenai/S2ORC |

## ✍️ 写作与 AI 助手

| 工具 | 说明 | 链接 |
|---|---|---|
| **gpt_academic** 🔥 | 面向科研的中文润色/翻译/批注/代码解释，把中文草稿改成学术英文初稿 | https://github.com/binary-husky/gpt_academic |
| **ChatPaper** | 论文提炼、领域综述自动生成，快速吃透一个方向后再动笔 | https://github.com/kaixindelele/ChatPaper |
| **AI Scientist** | SakanaAI 自动化科研实验框架，了解"AI 如何写论文"很有启发（别直接抄） | https://github.com/SakanaAI/AI-Scientist |
| **gpt-researcher** | 多步联网检索+报告生成，写相关工作、找 gap 时做初步调研 | https://github.com/assafelovic/gpt-researcher |

## Σ 排版与 LaTeX

| 工具 | 说明 | 链接 |
|---|---|---|
| **Pandoc** ⭐必装 | 文档格式互转（md→docx→tex），先用 Markdown 写再转 LaTeX 很顺手 | https://github.com/jgm/pandoc |
| **latexdiff** | 逐行高亮标出修订前后差异，rebuttal/Camera-ready 改稿必备 | https://github.com/ftilmann/latexdiff |
| **Typst** | 新式排版语言，比 LaTeX 快且易学，适合做草稿 | https://github.com/typst/typst |
| **Tectonic** | 自包含 LaTeX 引擎，无需装完整 TeX Live 即可编译，环境干净 | https://github.com/tectonic-typesetting/tectonic |
| **PGF/TikZ** | LaTeX 矢量绘图，论文里的结构图、网络图用它画最专业 | https://github.com/pgf-tikz/pgf |

## 📊 图表与可视化

| 工具 | 说明 | 链接 |
|---|---|---|
| **matplotlib** ⭐必装 | Python 绘图基石，论文所有曲线/柱图/消融图，配 style 调成会议风 | https://github.com/matplotlib/matplotlib |
| **seaborn** | 基于 matplotlib 的统计图表，配色和默认样式更学术 | https://github.com/mwaskom/seaborn |
| **plotly.py** | 交互式图表，做可旋转 3D 特征图、在线补充材料 | https://github.com/plotly/plotly.py |

## 🧠 知识管理与智能体

| 工具 | 说明 | 链接 |
|---|---|---|
| **Obsidian** | 本地优先的笔记/知识库，管理研究素材与文献笔记 | https://github.com/obsidianmd/obsidian-releases |
| **LangChain** | 搭自己的论文助手/检索增强链，把写作流程自动化 | https://github.com/langchain-ai/langchain |
| **LlamaIndex** | 把文献/笔记做成可检索索引，喂给大模型做定向问答 | https://github.com/run-llama/llama_index |
| **awesome-deep-learning** | 深度学习资源总索引，找教程/代码/数据集入口 | https://github.com/ChristosChristofidis/awesome-deep-learning |

## 🔬 可复现与实验追踪

| 工具 | 说明 | 链接 |
|---|---|---|
| **Weights & Biases** | 实验追踪、超参扫描、结果可视化 | https://github.com/wandb/wandb |
| **MLflow** | 开源实验管理与模型追踪 | https://github.com/mlflow/mlflow |
| **DVC** | 数据版本控制，让数据集/模型像代码一样可版本化 | https://github.com/iterative/dvc |
| **Hydra** | 优雅管理配置与多组实验参数 | https://github.com/facebookresearch/hydra |

> 💡 工具是手段不是目的。选 2–3 个真正融入你工作流的坚持用，比每个都浅尝辄止有价值。欢迎按方向补充你的私藏工具，见 [CONTRIBUTING](../CONTRIBUTING.md)。

**相关**：[01 调研](./01-literature-review.md) · [02 实验](./02-experiment.md)
