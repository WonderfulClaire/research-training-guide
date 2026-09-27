# LLM / Agent Post-Training Experiment Checklist

用于 SFT / DPO / PPO / GRPO / tool-using agent / AutoResearch 项目。

## Before training

- [ ] 明确 task success 的定义
- [ ] training reward 与 final evaluation metric 分开
- [ ] train / dev / held-out task 已隔离
- [ ] held-out verifier 不进入 prompt
- [ ] 样本 ID / 文件名 / metadata 无标签泄漏
- [ ] system prompt 固定并版本化
- [ ] tool schema 固定并版本化
- [ ] context / memory / compaction policy 固定
- [ ] max steps / retry policy 固定
- [ ] generation parameters 固定
- [ ] Base / SFT / SFT+RL checkpoint 来源明确

## Reward audit

- [ ] 每个 reward component 单独记录
- [ ] 有 secure final-state verifier
- [ ] public verifier 不是唯一最终指标
- [ ] 设计至少一个 reward-hacking adversarial case
- [ ] 检查模型能否修改 tests / evaluator / answer key
- [ ] 保存 exploit trajectory
- [ ] 记录 hacking rate

## Training diagnostics

- [ ] group reward std
- [ ] zero-variance group rate
- [ ] policy loss
- [ ] gradient norm
- [ ] KL to reference
- [ ] response length
- [ ] truncation rate
- [ ] invalid tool-call rate
- [ ] average tool steps
- [ ] optimizer step count

## Evaluation

- [ ] 至少 3 个随机种子
- [ ] 不只报告最好 seed
- [ ] same-harness evaluation
- [ ] held-out harness evaluation
- [ ] secure success
- [ ] public/hidden gap
- [ ] reward-hacking rate
- [ ] token / latency / tool-call cost
- [ ] failure-type breakdown

## Ablations

- [ ] Base vs SFT
- [ ] SFT vs SFT+RL
- [ ] reward components
- [ ] history/context policy
- [ ] tool-schema / harness
- [ ] training data amount
- [ ] decoding budget / max steps

## AutoResearch boundary

- [ ] 可以改 training config
- [ ] 可以改 prompt / reward weights
- [ ] 不可以改 hidden verifier
- [ ] 不可以改 held-out data
- [ ] 不可以删除失败 run
- [ ] 不可以只保留最好 seed

## Before making a claim

- [ ] 提升能否由更多训练步数解释
- [ ] 提升能否由更多 SFT 数据解释
- [ ] 提升能否由 harness 改动解释
- [ ] reward 上涨是否伴随 secure success 上涨
- [ ] 是否出现更长输出或更多工具调用
- [ ] 是否只在 synthetic data 成立
- [ ] 是否清楚写出 limitation
