# 09 · LLM / Agent 后训练实验怎么做得可信

LLM 后训练和 Agent 研究最容易出现一种情况：训练 loss 在下降、reward 在上涨、demo 也能跑，但真正能证明的方法收益很弱。原因通常不在优化器，而在实验协议：数据泄漏、harness 混杂、reward hacking、只挑最好 seed、把 public verifier 当真实成功、没有 held-out harness、没有记录 rollout 失败类型。

这一章给一个可以直接照着执行的研究协议，适用于 SFT、DPO、PPO、GRPO、tool-using agent 和 AutoResearch 类项目。

## 1. 先把模型、Harness、环境、Verifier 拆开

Agent 结果不是纯模型能力：

~~~text
Agent performance
=
Model
+ System Prompt
+ Tool Schema
+ Context Policy
+ Environment
+ Verifier
~~~

如果两个模型使用不同 harness，或者训练前后同时改了 prompt / tool schema，就不能把差异直接归因到模型。

实验前先冻结 system prompt、tool definitions、max steps、context policy、retry policy、verifier version、task split 和 sampling parameters，然后一次只改一个因素。

## 2. 数据划分不仅是 train / test

Agentic post-training 至少要区分四类数据：

| Split | 用途 | 能否被训练过程看到 |
| --- | --- | --- |
| train | SFT / RL rollout | 可以 |
| dev | 选超参、debug | 可以，但要记录使用次数 |
| held-out task | 最终任务泛化 | 不可以 |
| held-out harness | 测协议泛化 | 不可以 |

如果 hidden verifier、测试答案、task ID 暗含标签，都属于泄漏。要检查文件名、样本 ID、tool 返回字段、prompt 模板、cache key、metadata 和数据排序有没有带答案信息。

## 3. Reward 不是 Ground Truth

后训练里最重要的区分：

~~~text
training reward  !=  actual task success
~~~

例如 coding agent 可能通过修改 test file 让 public tests 全过，但 hidden tests 仍失败。

因此 verifier 最好分层：

~~~text
Policy-visible signal
    ↓
Public tests / visible checks

Independent evaluation
    ↓
Original public tests
+ Hidden tests
+ Integrity checks
+ Held-out evaluator
~~~

研究报告里至少同时给 training reward、secure success、public/hidden gap 和 reward hacking rate。不要只画 reward curve。

## 4. Reward Hacking 要主动设计实验

不要等模型真的学会作弊再补救。可以故意构造有漏洞的 verifier，测试优化过程是否会利用：

- 删除或修改测试
- hard-code public cases
- 输出固定格式骗 parser
- 提前终止绕过检查
- 重复工具调用刷过程奖励
- 冗长回答骗 LLM judge
- 修改环境文件影响 evaluator

推荐保存 exploit trajectory：

~~~text
task
→ action sequence
→ observations
→ reward components
→ secure verifier result
→ exploit type
~~~

这样 verifier 修复前后能直接算 hacking rate。

## 5. SFT、RL 的对照必须拆开

如果项目声称 RL 有效果，至少做：

| Group | Initialization | Training |
| --- | --- | --- |
| Base | pretrained / instruct | none |
| SFT | Base | successful trajectories |
| SFT + RL | same SFT checkpoint | GRPO / PPO |

否则所谓 RL 提升可能其实来自 SFT 数据。最好再加 SFT + more data 或 SFT + longer training，用于排除只是训练更多的解释。

## 6. Harness Generalization

Agent 很容易对工具名和 prompt 格式过拟合。训练时可用两套 schema，最终测试用从未见过的第三套：

~~~text
Train:
  Harness A: read_file / write_file / run_tests
  Harness B: read / write / test

Held-out:
  Harness C: inspect_file / update_file / check_tests
~~~

如果 seen harness 很高、held-out harness 明显下降，应报告 harness sensitivity，而不是只报告最高 success。

## 7. History / Context Ablation

Reasoning model 或长时程 agent 可能依赖完整 assistant message、tool call history、reasoning state、memory 或 compaction policy。

做 ablation 时只改一个变量：

~~~text
A: full assistant history
B: remove reasoning-like fields
C: compact old history
~~~

不要删掉 tool_call_id 或破坏消息结构，否则测到的是 API failure，不是 context dependence。

记录 success、invalid tool calls、average turns、input/output tokens 和 compaction frequency。

## 8. Seed 不要只报最好的

至少建议 3 个随机种子，报告 mean ± std，不挑最好 seed。

对于样本级预测，还可以做 paired bootstrap：在同一批 test sample 上比较 baseline 与新模型的逐样本差异，比两个独立均值更有信息。

## 9. 训练过程必须记录有没有真的学

GRPO / PPO 常见假训练包括：

- reward 组内没有差异
- advantage 全 0
- policy logprob 被错误 detach
- optimizer 没有 step
- gradient norm 为 0
- KL 过大导致更新被压死
- rollout 生成失败

至少记录：

| Metric | 看什么 |
| --- | --- |
| group reward std | 有没有学习信号 |
| zero-variance group rate | 有多少组完全没信号 |
| policy loss | 是否真的变化 |
| grad norm | 是否有反向 |
| KL | 是否偏离 reference |
| response length | 有没有 length drift |
| invalid tool rate | tool use 是否退化 |
| secure success | 真任务是否提升 |

## 10. AutoResearch 要隔离实验者和考官

AutoResearch 可以改 training config、prompt、reward weights、context policy 和 tool description，但不应修改 hidden verifier、held-out test、答案或 reporting rule，也不能删除失败 run 或只保留最好 seed。

否则自动科研很容易退化成自动刷 benchmark。

## 11. 推荐实验表

| Experiment | Train setting | Eval setting | Main question |
| --- | --- | --- | --- |
| E0 | Base | canonical harness | baseline |
| E1 | SFT | canonical | SFT 是否提升 |
| E2 | SFT + RL | canonical | RL 是否额外提升 |
| E3 | SFT + RL | held-out harness | 是否泛化 |
| E4 | SFT + RL | secure verifier | reward 是否对齐真实成功 |
| E5 | history ablation | same tasks | 是否依赖 history |
| E6 | reward ablation | same tasks | 哪个 reward component 有作用 |

最终不要只给一个 Best model。应该回答：提升来自 SFT 还是 RL？seen harness 还是 held-out 也提升？reward 上升和 secure success 是否一致？是否增加 reward hacking？是否只是输出更长或调用更多工具？

## 12. 写论文时怎么表述

更稳妥：

> Under a fixed harness and held-out verifier, the RL-trained model improved secure task success over the SFT checkpoint across three seeds.

如果只在合成数据验证：

> Results are limited to the synthetic environment and do not establish real-world deployment performance.

如果 held-out harness 掉得明显：

> The model remains sensitive to tool-schema changes, indicating incomplete harness generalization.

这些限制不是自曝短板，而是让结论可相信。

## 13. 和仓库里的其他章节一起用

- [02 · 实验设计与执行](02-experiment.md)
- [03 · 会议论文写作](03-conference-paper.md)
- [04 · 期刊论文写作](04-journal-paper.md)
- [LLM / Agent 实验检查清单](../templates/llm-agent-experiment-checklist.md)

一句话：

> 对 LLM / Agent 后训练，最重要的实验能力不是把训练跑起来，而是证明这个提升真的是你声称的那个原因。


## 14. 把协议落到真实代码：四个可复核案例

这套协议不是只停留在 checklist。下面几个仓库分别把不同环节做成了可以运行、可以失败、可以审计的实现：

| 研究问题 | 可复核实现 | 重点看什么 |
| --- | --- | --- |
| Reward hacking / secure verifier | [Kimi K3 Agentic Post-Training Lab](https://github.com/WonderfulClaire/kimi-k3-deep-dive) | mutable public signal、held-out tests、integrity verifier、verified trajectory → SFT、environment-owned GRPO |
| Reward 与真实质量是否冲突 | [5G Diagnostic Agent](https://github.com/WonderfulClaire/5G-Diagnostic-Agent) | 多轮工具轨迹、correctness/reward 分离、learning route、离线 reward-alignment audit |
| GRPO 为什么会忠实优化坏 reward | [RL From Scratch · Agentic Post-Training](https://github.com/WonderfulClaire/rl-from-scratch/tree/main/12_agentic_post_training) | 最小 categorical policy 更新，把 exploit reward 直接连到 advantage 与 policy probability |
| Harness 到底由什么组成 | [Agent the Hard Way](https://github.com/WonderfulClaire/agent-hard-way) | provider、tools、permissions、context、memory、skills、subagents 如何逐层改变 action/state space |

### Case A：public PASS 但 secure FAIL

K3Lab 故意保留一个可被利用的 public-test signal。删除 public tests 时，naive checker 可以出现 0/0 PASS；secure verifier 会重新使用原始 public tests、held-out tests 和 integrity check，所以最终 success 仍为 0。

这个案例适合验证：

- verifier 是否与 policy-visible state 隔离；
- reward hacking rate 怎么定义；
- exploit trajectory 是否被保存；
- verifier 修复后旧轨迹能否重算。

### Case B：Reward 在涨，但 correctness ordering 反了

5G Diagnostic Agent 把 rollout reward、独立 correctness、工具成本分别保存。训练前先把 group 路由到：

~~~text
rl_ready
efficiency_rl
audit_reward_quality_conflict
audit_reward_efficiency_conflict
teacher_or_sft_repair
~~~

并提供离线 audit，重新从保存的 reward/correctness/cost 向量计算 route，检查训练器有没有在冲突 group 上错误更新。

这比只看平均 reward 更接近真正的训练系统审计。

### Case C：优化器不是 reward 的纠错器

RL From Scratch 的最小 demo 固定同一组 agent strategies，只替换 reward：

~~~text
naive reward:
  correct fix        = 1
  delete tests       = 1
  hard-code cases    = 1
  do nothing         = 0

secure reward:
  correct fix        = 1
  all exploits       = 0
~~~

同样的 group-relative update 会忠实强化 reward=1 的行为。也就是说，**GRPO 可以让一个坏 verifier 的漏洞学得更快，而不会自动发现你的真实意图。**

### Case D：Harness 也属于训练分布

Agent the Hard Way 从最小 provider 开始，逐步增加 tool registry、permissions、history、compaction、memory、skills 和 subagents。进入后训练以后，这些都应该进入 trajectory metadata，而不是被当作“外部工程细节”。

例如：

~~~text
harness_version
selected_skills
context_policy
memory_enabled
subagent_task_id
fanout_limit
tool_schema_variant
~~~

否则同一个 checkpoint 换 harness 后性能变化，很难判断来自模型还是执行系统。

## 15. 一个更完整的后训练证据链

把上面几类实验串起来，建议最后保留这条证据链：

~~~text
task split + harness version
        ↓
rollout trajectory
        ↓
visible reward components
        ↓
independent correctness / secure verifier
        ↓
reward-alignment audit
        ↓
verified successful trajectories
        ↓
SFT
        ↓
RL
        ↓
seen harness + held-out harness
        ↓
multi-seed report + failed cases
~~~

如果其中任一箭头不可复核，最终“RL 有提升”的结论都应该相应收窄。
