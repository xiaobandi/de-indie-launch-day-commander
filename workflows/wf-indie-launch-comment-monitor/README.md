# 当日评论监控与回复建议

> 抓取新评论 → 情绪识别 → 草拟回复 → 推送人工确认

工作流 `wf-indie-launch-comment-monitor`　·　归属 发布日冲刺指挥官　·　触发 定时（发布日每 15 分钟）　·　
复杂度 M　·　阶段 P1

## 调用链

- `评论情绪识别`（review-sentiment-tag）
- `回复话术生成`（reply-copy-generator）

## 文档

- [`WORKFLOW.md`](WORKFLOW.md) — 完整编排、闸门、降级与验收标准
- [`tests/cases.yaml`](tests/cases.yaml) — 端到端 / 闸门 / 降级用例

## 一句话试用

```text
帮我跑 发布日冲刺指挥官 的「当日评论监控与回复建议」：<你的输入>
```
