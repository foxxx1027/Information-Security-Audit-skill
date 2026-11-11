# 2.6-错误处理与信息泄露 —— 技能说明

## 本子域审计范围

报错堆栈、目录浏览、源码备份、.git、env 配置文件、调试接口泄露信息。

## 技能清单（3 个）

| 集合 | 技能 | 一句话说明 | 归类理由 |
|---|---|---|---|
| 渗透测试方法论 | `wahh-info-leak-inference`<br>[信息泄露与推论挖掘](../../../skills/pentest-methodology/wahh-info-leak-inference/SKILL.md) | 错误消息当探测器反推逻辑，凡可区分反馈皆情报信道 | 错误信息与侧信道泄露挖掘 |
| 密码工程 | `stallings-fail-direction-audit`<br>[fail方向声明与静默失效](../../../skills/crypto-engineering/stallings-fail-direction-audit/SKILL.md) | 每条校验显式声明 fail-open/close，SPF 静默失效最危险 | fail方向审计属失效处理 |
| 密码工程 | `stallings-transparency-audit-clauses`<br>[透明性与可审计性治理](../../../skills/crypto-engineering/stallings-transparency-audit-clauses/SKILL.md) | 常数生成规则/公开设计/第三方分析/黑盒定价四条验收条款 | 透明性审计条款归信息泄露 |

**来源分布**：渗透测试方法论×1、密码工程×2
