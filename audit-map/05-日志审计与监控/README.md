# 05-日志审计与监控 · 日志、审计与监控 —— 技能说明

## 本目录审计范围

审计范围：操作日志、登录日志、异常访问日志；日志完整性、防篡改、留存时长、告警机制；是否存在日志缺失、无法溯源（OWASP 日志监控失效）。

## 技能清单（4 个）

| 集合 | 技能 | 一句话说明 | 归类理由 |
|---|---|---|---|
| Web应用防御 | `whitehat-evidence-preservation-logging`<br>[证据保全日志架构](../../skills/webapp-defense/whitehat-evidence-preservation-logging/SKILL.md) | 日志实时外送并与被攻系统隔离生命周期，响应先保全现场再止损 | 日志完整性与取证溯源保障 |
| 渗透测试方法论 | `wahh-detection-design`<br>[检测面设计](../../skills/pentest-methodology/wahh-detection-design/SKILL.md) | 信噪比权衡，基于本应用正常行为的上下文检测与日志设计 | 日志告警监控的检测设计 |
| 体系审核验证 | `isms-log-audit-trio`<br>[日志审计三件套](../../skills/system-audit-verification/isms-log-audit-trio/SKILL.md) | 字段完备、架构适配、跨系统联合三查，判定事后可调查能力 | 日志体系完备性与可调查性 |
| 合规测评 | `mlps-audit-log-offsite-retention`<br>[审计记录留存的异地化判据](../../skills/compliance-assessment/mlps-audit-log-offsite-retention/SKILL.md) | 本地日志可灭失而无异地日志基础设施即判不符合 | 审计日志留存异地化 |

**来源分布**：Web应用防御×1、渗透测试方法论×1、体系审核验证×1、合规测评×1

## 覆盖缺口

缺口提示：SIEM 规则调优、告警疲劳治理仅有间接覆盖；留存时长/防篡改的工程实现建议结合等保类技能（06）一起用。
