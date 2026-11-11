# 2.2-访问授权 —— 技能说明

## 本子域审计范围

越权（IDOR）、横向/纵向权限绕过、角色隔离、菜单与接口权限一致性、垂直权限绕过。

## 技能清单（5 个）

| 集合 | 技能 | 一句话说明 | 归类理由 |
|---|---|---|---|
| 代码审计 | `caudit-api-blindspot-priority`<br>[API盲区优先级与三准则](../../../skills/code-audit/caudit-api-blindspot-priority/SKILL.md) | 按密度与覆盖率成反比定律枚举盲区接口，鉴权、字段最小化、常规漏洞三准则排序 | 接口未授权居首，盲区即攻击面 |
| 代码审计 | `caudit-privilege-delta-dataflow`<br>[权限差数据流通道审计](../../../skills/code-audit/caudit-privilege-delta-dataflow/SKILL.md) | 枚举低权可写高权必读的必达通道字段，逐字段按高权端语境编码并盲打验证 | 低权写高权必读的越权通道枚举 |
| 渗透测试方法论 | `wahh-authz-differential-testing`<br>[访问控制差分测试](../../../skills/pentest-methodology/wahh-authz-differential-testing/SKILL.md) | 建主体×对象×动作授权矩阵，双账户重放测垂直/水平/上下文越权 | 授权矩阵差分实验设计 |
| 渗透测试方法论 | `wahh-client-state-untrusted`<br>[客户端状态不可信](../../../skills/pentest-methodology/wahh-client-state-untrusted/SKILL.md) | 五类载体三步测试，加密不改不可信本质，须证服务端缺校验 | 误信客户端控件是授权缺陷前提 |
| 渗透测试方法论 | `wahh-insecure-authz-antipatterns`<br>[不安全授权反模式](../../../skills/pentest-methodology/wahh-insecure-authz-antipatterns/SKILL.md) | 参数型/头部型/位置型三型形态学，配识别信号快速定性 | 不安全授权实现形态学 |

**来源分布**：代码审计×2、渗透测试方法论×3
