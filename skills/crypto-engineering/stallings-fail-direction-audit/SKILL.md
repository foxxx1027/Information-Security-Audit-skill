---
name: stallings-fail-direction-audit
description: |
  审计安全校验的默认行为时调用：每条校验显式声明 fail-open/fail-close，三态问句——配置为空时返回什么？规则不匹配时返回什么？组件崩溃时返回什么？SPF 教训：未部署=无防护，部署错误=静默失去防护还制造已部署错觉（比未部署更危险）；对照 IPsec 无匹配即丢；加密流需显式关闭信号（close_notify）。不适用于：不影响判定的纯观测组件。关键 trigger：fail open or fail closed、default deny vs allow、behavior on empty config、silent failure、规则不命中默认、组件挂了还放行吗。
source_book: Information-Security-Audit-Skill 技能库
source_chapter: 第19章 19.8.2；第20章 20.2；第17章 17.3.2；第1章 1.5
tags: [fail-safe-defaults, fail-open, silent-failure, configuration-audit, close-notify]
related_skills:
  - slug: stallings-design-principles-review-protocol
    relation: depends-on
  - slug: stallings-protocol-belief-analysis
    relation: contrasts-with
  - slug: stallings-policy-gradual-rollout
    relation: composes-with
---

# fail 方向声明与静默失效

## R — 原文 (Reading)

> "（1）如果未返回任何SPFTXTRR，则默认操作为接收邮件消息。（2）如果SPFTXTRR格式错误，则默认操作为接收邮件消息。"
>
> — 方法论出处，第19章 19.8.2 接收端 SPF（引文含 OCR 噪声，按原样保留）

---

## I — 方法论骨架 (Interpretation)

每条安全校验都有一个隐藏属性：**失效时往哪边倒**。不显式声明它，系统就会在三种异常态下各自为政。审计用三态问句逐条过：

1. **配置为空**时返回什么？（域未表态）
2. **规则不匹配/格式错误**时返回什么？（表态了但坏了）
3. **组件崩溃/依赖不可达**时返回什么？（机制本身失灵）

SPF 的教训展示了 fail-open 的完整后果链：无记录与格式错误都默认收信——**未部署=无防护，部署错误=静默失去防护还制造"已部署"的错觉**，后者比前者更危险，因为没人再去修。对照 IPsec 的出入站处理"无匹配即丢"（fail-close），两类失效方向在书内形成正反对照。判定规则：认证类校验（token、白名单、策略）必须 fail-close+告警；纯观测类可 fail-open 但要有失效时长上报回路。加密流另有第三种异常：静默断开——没有 close_notify 这类显式密码学关闭信号，截断攻击就不可区分于正常结束；可用性优先的通道是显式例外，须单独补偿（故障安全默认准则）。

---

## A1 — 书中的应用 (Past Application)

### 案例 1: SPF 的两条默认放行（第19章）
- **问题**: 接收端按 SPF 判定，域没发记录或记录写错时怎么办？
- **方法论的使用**: 三态问句直接命中——书内规则两条默认都是"接收邮件消息"（fail-open）。
- **结论**: 未部署的域等于无防护；已部署但写错的域静默失去防护且制造错觉；攻击者可从"未表态"的域名发信绕过。
- **结果**: 修复路径为显式声明方向+把配置错误纳入威胁模型+用 DMARC 报告回路监测收紧。

### 案例 2: IPsec 无匹配即丢（第20章）
- **问题**: 策略表查不到匹配项的包怎么处理？
- **方法论的使用**: 对照组——出入站处理均为"无匹配即丢弃"（fail-close），匹配 BYPASS 才放行且需显式配置。
- **结论**: 与 SPF 形成书内正反对照，证明失效方向是设计决策而非不可控的默认。
- **结果**: fail-close+显式例外成为 IPsec 策略引擎的语义基线。

### 案例 3: HTTPS 的静默关闭（第17章）
- **问题**: TCP 连接断了就算会话正常结束吗？
- **方法论的使用**: 第三态（组件/信道异常）——没有 close_notify 也没有 Connection:close 的"未声称的关闭"可能被攻击者利用（截断攻击：受害者无法区分对端结束与攻击者掐断）。
- **结论**: 正确关闭必须双方经警报协议交换 close_notify；"不完全关闭"仅允许在应用层确认已收到全部关心数据之后；静默断开一律按需告警的异常态处理。
- **结果**: 成为 HTTPS 客户端实现的安全要求。

---

## A2 — 触发场景 (Future Trigger) ★

### 用户会在什么情境下需要这个 skill?

1. 新中间件/策略引擎的默认行为设计评审（认证中心连不上时放行还是拒绝）。
2. 故障演练/混沌测试中评估安全组件的行为。
3. 排查"部署了但没生效"的静默失效事故。
4. 配置错误类安全事件的复盘定性。

### 语言信号 (用户的话里出现这些就应激活)

- "fail open 还是 fail closed / default deny vs default allow"
- "配置为空时什么行为 / behavior on empty config"
- "静默失效 / silent failure"
- "规则不命中默认怎么办 / default action when no rule matches"
- "依赖组件挂了还放行吗 / what happens when the dependency is down"

### 与相邻 skill 的区分

- 与 `stallings-two-phase-gated-access` 的区别: 那个定门的**结构**（几道门、何时开），本 skill 定每道门在**异常输入下的方向**——结构审计之后逐门做方向审计。
- 与 `stallings-design-principles-review-protocol` 的区别: 那个治理 13 条准则的张力登记，本 skill 把其中"故障安全默认"具体化为三态问句+对照案例库——通用准则 vs 专项审计法。
- 与 `stallings-policy-gradual-rollout` 的区别: 那个管策略收紧的过程控制，本 skill 管单点校验的失效方向——一个过程、一个状态。

---

## E — 可执行步骤 (Execution)

1. **列校验点清单**：写出系统全部安全校验点（认证、白名单、策略、签名/证书验证、加密流关闭）。
   - 完成标准: 清单成文，含每点的判定逻辑摘要。
2. **三态填表**：对每个校验点回答——配置为空/规则不匹配/依赖崩溃各返回什么，实测验证而非读代码猜测。
   - 完成标准: 三态表全覆盖且经实测抽查。
3. **定方向**：认证类强制 fail-close+告警；纯观测类可 fail-open 但建立失效时长上报回路。
   - 完成标准: 每点有显式方向声明与理由。
4. **修"配置为空=全放行"实现**：定性为与未部署同罪——改为拒绝启动、显式默认或强制初始化。
   - 完成标准: 空配置路径被消除或有拦截。
   - 判停条件: 纯观测、无阻断能力的组件（纯日志）可停在登记。
5. **核对显式关闭**：加密/会话流核对关闭信号（close_notify 类）；静默断开列入告警项。
   - 完成标准: 截断场景在客户端有告警或可区分。

---

## B — 边界 (Boundary) ★

### 不要在以下情况使用此 skill

- 把一切 fail-open 都定性为漏洞——可用性优先的通道（保命路径）是显式例外，但须单独补偿控制并登记。
- 只审单个组件而漏级联——上游默认放行+下游假设上游已拦，是复合静默失效，要沿链路问三态。

### 作者在书中警告的失败模式

- 静默失效比未部署更危险（制造"已部署"错觉）。
- 加密流的静默断开可被截断攻击利用（ce078）。

### 作者的盲点 / 时代局限

- 书中案例集中在邮件/IPsec/TLS（成书 2017 前）；现代配置中心、特性开关、服务网格策略的三态语义需自行映射——书内没有"配置中心连不上"的样本，框架是外推应用。

### 容易混淆的邻近方法论

- v45 两阶段开门（结构 vs 方向）。
- v48 灰度收紧（过程）、v05 准则清单（母集）。

---

## 相关 skills (阶段 3 定稿)

- **depends-on**: `stallings-design-principles-review-protocol` —— 三态问句是"故障安全默认"准则（那个 13 条清单之一）的专项审计化——先理解准则清单，再做单点方向审计。
- **contrasts-with**: `stallings-protocol-belief-analysis` —— 配置面（规则不命中返回什么）vs 时序面（协议信念是否成立）——两类缺陷分开审。
- **composes-with**: `stallings-policy-gradual-rollout` —— 先声明单点失效方向（本 skill），方向正确的策略再按那个灰度收紧——先定方向再灰度。

---

## 审计信息

- **验证通过**: V1 ✓ / V2 ✓ / V3 ✓
- **测试通过率**:
- **蒸馏时间**: 2026-11-10
