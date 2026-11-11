# 2.8-安全配置 —— 技能说明

## 本子域审计范围

安全响应头 CSP、HSTS、X-Frame-Options；中间件默认配置、多余模块、管理后台暴露。

## 技能清单（6 个）

| 集合 | 技能 | 一句话说明 | 归类理由 |
|---|---|---|---|
| Web应用防御 | `whitehat-resource-quota-audit`<br>[资源配额滥用审计](../../../skills/webapp-defense/whitehat-resource-quota-audit/SKILL.md) | DoS=对有限资源的无限制滥用：列全部有限资源逐项问匿名能否无限触发 | DoS资源滥用防护归安全配置类 |
| 代码审计 | `caudit-horizontal-depth-pillars`<br>[两支柱体系：横向细化与纵深防御](../../../skills/code-audit/caudit-horizontal-depth-pillars/SKILL.md) | 横向细化靠规则量抬攻击成本有停止条件，纵深按上层失效推演，木桶原理定投入 | 防御规则层次配比与投入基线 |
| 密码工程 | `stallings-capability-negotiation-baseline`<br>[能力协商确定性与弱副本木桶](../../../skills/crypto-engineering/stallings-capability-negotiation-baseline/SKILL.md) | 未知能力有确定规则、最低集只升不降、弱副本拉低整体 | 能力协商基线属安全配置 |
| 密码工程 | `stallings-extension-point-criticality`<br>[演进接口：扩展点与解耦](../../../skills/crypto-engineering/stallings-extension-point-criticality/SKILL.md) | 可选扩展+critical 显式拒绝语义实现前向兼容演进 | 扩展点治理属安全配置 |
| 密码工程 | `stallings-policy-gradual-rollout`<br>[策略灰度与遥测回路](../../../skills/crypto-engineering/stallings-policy-gradual-rollout/SKILL.md) | 档位序列+百分比灰度，升级挂度量阈值而非日历日期 | 策略灰度上线属安全配置 |
| 密码工程 | `stallings-protocol-migration-governance`<br>[兼容过渡与协议演进治理](../../../skills/crypto-engineering/stallings-protocol-migration-governance/SKILL.md) | 双清单分账、兼容层带退役表、签名策略封死降级回退 | 协议升级治理属配置演进 |

**来源分布**：Web应用防御×1、代码审计×1、密码工程×4
