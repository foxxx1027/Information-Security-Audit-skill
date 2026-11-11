---
name: stallings-capability-negotiation-baseline
description: |
  设计或评审算法/能力协商（新旧版本客户端并存、多端同步）时调用：能力未知必须有确定性选择规则（已知按最高→未知选兼容面最广强算法且失败显式化→再按最弱档）+强制最低集随版本只升不降+明确失败终止；弱副本木桶律——同一内容多端同步时任何弱副本使整体=最弱。不适用于：封闭单版本系统。关键 trigger：client preference list、mandatory to implement、minimum cipher、silent downgrade、legacy clients weak crypto、multi-recipient encryption、群发加密。
source_book: Information-Security-Audit-Skill 技能库
source_chapter: 第19章 19.4.3；第17章 17.4；第16章 16.2
tags: [capability-negotiation, interop, downgrade, weakest-replica, algorithm-baseline]
related_skills:
  - slug: stallings-policy-gradual-rollout
    relation: composes-with
  - slug: stallings-protocol-migration-governance
    relation: composes-with
  - slug: stallings-extension-point-criticality
    relation: composes-with
---

# 能力协商确定性与弱副本木桶

## R — 原文 (Reading)

> "（3）如果发送方代理没有接收方的任何解密性能方面的知识，并且想冒险一试（接收方可能无法解密消息），则应该选择3DES。"
>
> — 方法论出处，第19章 19.4.3 S/MIME 认可的密码算法（算法降级选择四步法）

---

## I — 方法论骨架 (Interpretation)

可互操作协议的协商层必须回答一个工程师常忽略的问题：**对端能力未知时选什么？**没有确定性规则的协议，各实现会自行其是——要么互通失败，要么静默降级到弱算法。设计三件套：

1. **确定性选择规则**：发送方四步选法——已知对端能力按其最高选；未知但愿冒险，选兼容面最广的强算法，且把"可能无法解密"显式化（失败要可见，不得静默换弱档）；再不确定按协议规定的最弱兼容档。协商本身也要确定（客户端优先列表中第一个双方共有项）。
2. **强制最低集**：MUST 档算法随协议版本只升不降——互操作压力不能诱发弱算法被随意协商。
3. **明确失败终止**：能力不匹配时换方法（NAK）或明确 Failure 结束，两条出路都要有。

再加一条**弱副本木桶律**：同一内容发给多个接收方/同步到多端时，只要存在一份弱加密副本，整体安全=最弱那份——攻击者永远攻最弱的分身。降级兼容路径稀释整体安全，必须靠最低集与拒发机制挡住。

---

## A1 — 书中的应用 (Past Application)

### 案例 1: S/MIME 四步选法与 MUST/SHOULD 分级（第19章）
- **问题**: 收件方能力参差（AES、3DES、RC2/40），发件代理怎么选算法？
- **方法论的使用**: 算法按 MUST/SHOULD 分级（AES 各长度与 3DES 必需，弱算法可选），配四步选法处理能力未知——冒险选 3DES（兼容面最广的强档）且显式承担解密失败风险。
- **结论**: 能力未知的行为被协议规定，实现没有自由发挥空间。
- **结果**: S/MIME 互操作测试有了确定基准。

### 案例 2: 多接收方弱副本（第19章）
- **问题**: 群发邮件各接收方能力不同，分别构造强/弱两份副本行吗？
- **方法论的使用**: 木桶律核对——"该消息的安全性将由于弱安全性的一份副本而受到威胁"，攻击者取弱副本即可读全部内容。
- **结论**: 确立最低算法基线并拒绝向不满足基线的端发送敏感内容，或强算法加密一次、仅另行安全交付密钥材料。
- **结果**: 弱副本风险成为多端分发设计的必答项。

### 案例 3: EAP 的 NAK 与失败终止（第16章）+ SSH KEXINIT（第17章）
- **问题**: 认证方法/密钥交换不支持对端提议时怎么办？
- **方法论的使用**: EAP 客户端不支持则回 NAK，服务器换方法或发 Failure 结束——可降级的双面性（弹性 vs 降级面）由强制最低集平衡；SSH 的 KEXINIT 用确定性规则（客户端优先列表第一个共有项）+必须实现项。
- **结论**: 换方法与明确失败两条出路都必须存在；协商确定性与最低集是双保险。
- **结果**: 成为 IETF 式协商设计的标准结构。

---

## A2 — 触发场景 (Future Trigger) ★

### 用户会在什么情境下需要这个 skill?

1. 新旧版本客户端并存的算法协商规则设计（60% 老用户旧版本）。
2. 评审"弱算法还能被协商到"的配置与默认值。
3. 多端同步（群聊、群发、多方文档）的算法下限设计。
4. 互操作测试失败或行为不一致的排查。

### 语言信号 (用户的话里出现这些就应激活)

- "客户端优先列表 / client preference list negotiation"
- "最低算法集 / mandatory to implement, minimum cipher suite"
- "静默降级 / silent downgrade"
- "老版本还支持弱算法 / legacy clients stuck on weak crypto"
- "群发/多端同步的加密强度 / multi-recipient encryption strength"

### 与相邻 skill 的区分

- 与 `stallings-protocol-migration-governance` 的区别: 那个管过渡期治理与砍 legacy 的窗口（何时淘汰），本 skill 管协商规则本身（怎么选、最低集、失败终止）——治理层 vs 机制层。
- 与 `stallings-policy-gradual-rollout` 的区别: 那个管最低集逐步收紧的节奏，本 skill 定最低集与选择规则的内容。
- 与 `stallings-unauthenticated-key-exchange` 的区别: 匿名/弱套件协商问题常与认证缺失叠加，但对象不同——本 skill 管强度档位选择，那个管身份背书缺失。

---

## E — 可执行步骤 (Execution)

1. **写确定性规则**：定义能力协商的完整算法（谁先提议、按什么序、平局如何、能力未知选什么），消除实现自由度。
   - 完成标准: 规则可被两个独立实现遵循并得到相同结果。
2. **定强制最低集**：列出 MUST 档算法/能力，声明随版本只升不降的治理规则。
   - 完成标准: 最低集清单+版本治理规则成文。
   - 判停条件: 封闭单版本系统（无协商需求）跳过，直接固定算法。
3. **显式化冒险失败**：能力未知默认选"兼容面最广的强档"，失败必须可见（错误码/回执），禁止静默降级。
   - 完成标准: 失败路径测试通过，无静默换档。
4. **执行弱副本策略**：多端/多接收方场景按最弱副本定级，或拒绝向不达标端发送——登记例外。
   - 完成标准: 同内容全部副本≥最低集，例外有书面批准。
5. **互操作矩阵验证**：新新/新老/老老组合全部跑通且行为符合规则。
   - 完成标准: 矩阵全格通过并归档。

---

## B — 边界 (Boundary) ★

### 不要在以下情况使用此 skill

- 把"能协商"当弹性资产无限开放算法清单——协商面越大降级面越大，清单要短且分级。
- "冒险一试"成为常态路径——书内它是显式例外（可能无法解密要可见），不是默认。

### 作者在书中警告的失败模式

- 弱副本使整体安全受威胁（多接收方分发的木桶效应）。
- EAP 可降级的双面性：没有最低集与失败终止的降级通道就是攻击面。

### 作者的盲点 / 时代局限

- 书内"3DES 为兼容面最广的强算法"的判断是成书时代（2017 前）的产物，今 3DES 已属弱档——引用规则框架时基线算法必须按当代重选，勿照抄书内档位。

### 容易混淆的邻近方法论

- v39 迁移治理（何时砍 legacy）。
- v48 灰度收紧（节奏）、v35 认证缺失（另一缺陷类）。

---

## 相关 skills (阶段 3 定稿)

- **composes-with**: `stallings-policy-gradual-rollout` —— 协商基线的内容（本 skill）与收紧节奏（那个）配合。
- **composes-with**: `stallings-protocol-migration-governance` —— 机制层（选择规则、最低集）与治理层（过渡策略、砍 legacy 窗口）分工。
- **composes-with**: `stallings-extension-point-criticality` —— 运行时行为（协商选法）与解析时行为（未知字段 criticality 语义）是同一互操作问题的两个层面。

---

## 审计信息

- **验证通过**: V1 ✓ / V2 ✓ / V3 ✓
- **测试通过率**:
- **蒸馏时间**: 2026-11-10
