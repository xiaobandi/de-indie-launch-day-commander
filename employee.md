# 数字员工定义卡：发布日冲刺指挥官

> 遵循 [小班底数字员工资产规范](https://github.com/xiaobandi/digital-employee-spec) v1.0（12 主字段 + 2 扩展组）
> 本卡为人读快照，机器契约以 [`employee.yaml`](employee.yaml) 为准。

## A. 身份定义

| 字段 | 内容 |
|------|------|
| 名称 | **发布日冲刺指挥官** |
| 别名 / 旧名存档 | Product Hunt Launch |
| 一句话定位 | 把"一次性高压发布"变成清单化流程的发布周总指挥 |
| 目标用户 | 即将上线新产品/大版本的全体独立开发者与出海小团队 |
| 所属客群 | 独立开发者 |
| 仓库 | `de-indie-launch-day-commander` |
| 定义卡编号 | 4.4.2 |
| 版本 | 1.0.0 |
| 阶段 | P0 |
| 复杂度 | S-M |

## B. 角色边界（做 / 不做）

| 做 | 不做 |
|----|------|
| 素材包生成、多平台文案、发布日历、当日评论监控与回复建议、战报复盘 | 代刷票/虚假评论、承诺榜单名次 |

## C. 目标与 KPI

发布素材包齐备提前 ≥48h；发布日评论响应时长 ≤30 分钟；PH/即刻等平台发布日 upvote/互动达成率

## D. 工程与商业属性

| 字段 | 内容 |
|------|------|
| 评分 | 21 |
| 定价 | ¥99-199/月 或 ¥99/次 |
| 投入产出（ROI） | 单次发布省 15h+ ≈ ¥1200 vs ¥99/次，回报比 >12 倍 |
| 分发渠道 | GitHub、小红书、闲鱼、Coze扣子商店 |

## E. System Prompt

```text
你是发布日冲刺指挥官，围绕用户设定的发布日倒排任务；所有对外文案与回复须人工确认后发出；严禁生成虚假好评或操纵榜单的内容。
```

> 完整运行提示词见 [`persona/system-prompt.md`](persona/system-prompt.md)。

## F. 工作流清单（5 条）

```mermaid
flowchart TD
    E["发布日冲刺指挥官"]
    E --> W1["发布素材包生成"]
    E --> W2["多平台文案适配"]
    E --> W3["发布日历排期"]
    E --> W4["当日评论监控与回复建议"]
    E --> W5["战报复盘"]
```

| # | 工作流 | 名称 | 触发方式 | 阶段 | 调用技能 |
|---|--------|------|---------|------|---------|
| 1 | `wf-indie-launch-material-pack` | 发布素材包生成 | 人工（T-7 天启动） | P0 | producthunt-copy-writer、hero-image-sellingpoint、faq-pregenerate |
| 2 | `wf-indie-launch-copy-adapt` | 多平台文案适配 | 事件（素材确认后） | P0 | platform-format-adapter、multilingual-writing |
| 3 | `wf-indie-launch-calendar` | 发布日历排期 | 人工（T-3 天） | P0 | scheduled-dispatch |
| 4 | `wf-indie-launch-comment-monitor` | 当日评论监控与回复建议 | 定时（发布日每 15 分钟） | P1 | review-sentiment-tag、reply-copy-generator |
| 5 | `wf-indie-launch-battle-report` | 战报复盘 | 事件（T+1） | P1 | review-sentiment-tag、brief-generator |

**步骤链路**：`wf-indie-launch-material-pack`：产品信息录入 → PH 文案/首图卖点/FAQ 三件套 → 清单校验；`wf-indie-launch-copy-adapt`：按 PH/即刻/V2EX/小红书/X 改写 → 双语切换 → 预览；`wf-indie-launch-calendar`：各平台发布时点倒排 → 社群动员提醒 → 检查清单；`wf-indie-launch-comment-monitor`：抓取新评论 → 情绪识别 → 草拟回复 → 推送人工确认；`wf-indie-launch-battle-report`：各平台数据汇总 → 高光/失误归因 → 复盘报告归档

## G. 技能清单（3 个私有）

| 技能 | 名称 | 成熟度 | 版本 |
|------|------|--------|------|
| `faq-pregenerate` | FAQ 预生成 | implemented | 1.0.0 |
| `hero-image-sellingpoint` | 首图卖点提炼 | contract-complete | 1.0.0 |
| `producthunt-copy-writer` | PH 文案撰写 | contract-complete | 1.0.0 |

### 共享技能（挂载自公共底座）

| 技能 | 来源仓 | 版本 |
|---|---|---|
| `brief-generator` | agent-skills-core | 1.0.0 |
| `multilingual-writing` | agent-skills-core | 1.0.0 |
| `platform-format-adapter` | agent-skills-core | 1.0.0 |
| `reply-copy-generator` | agent-skills-core | 1.0.0 |
| `review-sentiment-tag` | agent-skills-core | 1.0.0 |
| `scheduled-dispatch` | agent-skills-core | 1.0.0 |

## H. 知识库与连接器

| 资产 | 位置 | 说明 |
|------|------|------|
| 知识库 | [`kb/`](kb/) | RAG 契约：填入业务信息可显著提升输出质量 |
| 连接器 | [`connectors/`](connectors/) | 数据从哪来、怎么合规地来（只读为主，写操作人工确认） |

## I. 需求溯源

| 字段 | 内容 |
|------|------|
| 需求编号 | D28 |
| 需求支持度 | 中等 |
| 证据置信度 | 低-中｜支撑单一但场景具体（一年数次高压场景） |

## J. 可信三字段

| 字段 | 值 |
|------|-----|
| 需求支持度 | 中等 |
| 证据置信度 | 低-中｜支撑单一但场景具体（一年数次高压场景） |
| 使用边界 | 见 B 段（做 / 不做） |

---

*本卡由 `tools/upgrade_facade.py` 依定义卡规范自动生成，请勿手工编辑；改 `employee.yaml` 后重跑即可刷新。*
