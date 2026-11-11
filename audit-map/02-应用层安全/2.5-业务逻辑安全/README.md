# 2.5-业务逻辑安全 —— 技能说明

## 本子域审计范围

业务流程绕过、竞态条件、金额/数量篡改、优惠券重复使用、订单篡改、风控绕过（扫描器很难发现，必须人工）。

## 技能清单（8 个）

| 集合 | 技能 | 一句话说明 | 归类理由 |
|---|---|---|---|
| Web应用防御 | `whitehat-abuse-feature-model`<br>[反滥用特征三维架构](../../../skills/webapp-defense/whitehat-abuse-feature-model/SKILL.md) | 按内容/行为/主体三维正交设计风控特征，交叉验证降误杀并定期重估衰减 | 风控反滥用体系设计，属业务风控域 |
| Web应用防御 | `whitehat-business-logic-four-questions`<br>[业务逻辑审查四问](../../../skills/webapp-defense/whitehat-business-logic-four-questions/SKILL.md) | 状态变更触发权/覆盖面/校验挂边/重认证四问审查订单支付等流程漏洞 | 流程绕过与风控反制类逻辑漏洞审查 |
| Web应用防御 | `whitehat-delayed-enforcement`<br>[延迟处置纪律](../../../skills/webapp-defense/whitehat-delayed-enforcement/SKILL.md) | 识别与处置解耦：延迟封禁/分批打压防规则被二分探测，检测逻辑留服务端 | 风控处置时序对抗探测的策略 |
| 代码审计 | `caudit-logic-vuln-audit`<br>[逻辑漏洞应然实然对照法](../../../skills/code-audit/caudit-logic-vuln-audit/SKILL.md) | 先建业务状态机与不变量应然模型，通读源码提取实然逐项diff，偏差即候选漏洞 | 应然实然对照挖掘业务逻辑漏洞 |
| 代码审计 | `caudit-payment-invariants`<br>[支付三不变量](../../../skills/code-audit/caudit-payment-invariants/SKILL.md) | 金额服务端真值、数值下限、原子幂等三不变量核对资金流程，另查回调再改写 | 资金流程三条不变量逐条核对 |
| 代码审计 | `caudit-server-side-state-truth`<br>[业务状态真值三问](../../../skills/code-audit/caudit-server-side-state-truth/SKILL.md) | 对资格次数额度身份问真值存哪、迁移是否原子、裁决可否伪造，删Cookie即验收 | 资格次数身份等状态真值三问 |
| 渗透测试方法论 | `wahh-logic-flaw-assumption-breaking`<br>[逻辑缺陷假设攻破法](../../../skills/pentest-methodology/wahh-logic-flaw-assumption-breaking/SKILL.md) | 枚举开发者隐含假设逐条构造违背，无签名漏洞的系统挖法 | 业务逻辑假设违背挖掘 |
| 渗透测试方法论 | `wahh-logic-target-zones-transactions`<br>[逻辑靶区与交易模式](../../../skills/pentest-methodology/wahh-logic-target-zones-transactions/SKILL.md) | 四类优先靶区收敛逻辑测试，交易不变量违背模式起手 | 逻辑测试选靶与交易靶区 |

**来源分布**：Web应用防御×3、代码审计×3、渗透测试方法论×2
