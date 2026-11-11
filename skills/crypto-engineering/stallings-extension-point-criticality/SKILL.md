---
name: stallings-extension-point-criticality
description: |
  设计需长期演进的协议/证书/消息格式时调用：演进不靠加固定字段而靠可选扩展+显式忽略语义（criticality/危险指示）——不认识且 critical=TRUE 则整体非法（旧实现显式拒绝），非 critical 可安全跳过；识别变化轴（方法×承载）在其间放稳定接口。不适用于：一次性短命格式。关键 trigger：forward compatible format、critical extension、unknown field 怎么处理、ignore unknown fields、versioning strategy、reserved for future use。
source_book: Information-Security-Audit-Skill 技能库
source_chapter: 第14章 14.4.2；第16章 16.2；第20章 20.2
tags: [format-evolution, criticality, extension-mechanism, decoupling, interoperability]
related_skills:
  - slug: stallings-capability-negotiation-baseline
    relation: composes-with
---

# 演进接口：扩展点与解耦

## R — 原文 (Reading)

> "每一个扩展项有一个扩展标识、一个危险指示和一个扩展值。危险指示用于指出该扩展项是否能安全地被忽略，如果值为TRUE且实现时未处理它，则其证书将会被当成非法的证书。"
>
> — 方法论出处，第14章 14.4.2 X.509 版本3 证书扩展

---

## I — 方法论骨架 (Interpretation)

格式要用十年，就不能靠"加固定字段"演进——每次加字段都是一次 break。长寿命的秘诀是**可选扩展+显式的忽略语义**：每个扩展带三件套（标识+危险指示 criticality+值）。

危险指示定了旧实现的行为：

- 不认识且 critical=TRUE → 整个对象非法（显式拒绝）；
- 非 critical → 可安全跳过。

这条规则同时买到两个方向——允许旧实现安全跳过新信息，也允许标准方声明"此项不可忽略"以强制执行。

最危险的缺省是**没有 criticality 声明**：旧实现静默跳过本应强制的新语义，安全属性无声丢失（X.509 把时间戳校验设为"可选"导致的反射攻击是同族教训）。

第二个设计动作是**识别变化轴并解耦**：找出会独立变化的两维（认证方法×传输承载），在它们之间放稳定接口（EAP 框架）；机制与密钥管理相互独立，接口收窄到单一标识符（IPsec 的 SPI）——避免每变一项就 fork 一个协议。

---

## A1 — 书中的应用 (Past Application)

### 案例 1: X.509v3 扩展三类（第14章）
- **问题**: v2 固定字段满足不了新需求（主体映射、策略标注、使用范围限定），怎么演进？
- **方法论的使用**: v3 不改固定格式，增可选扩展——每个扩展带危险指示，TRUE 且未处理则整张证书非法；扩展分三类（密钥和策略信息/主体与发行商属性/证书路径约束）。
- **结论**: 格式稳定演进且可强制新语义；路径约束还能限定使用范围以缩小 CA 失误的影响。
- **结果**: X.509v3 证书沿用至今，成为扩展机制的教科书实证。

### 案例 2: EAP 框架与承载解耦（第16章）
- **问题**: 认证方法与链路技术都在快速变化，怎么设计不被任何一边绑死？
- **方法论的使用**: 识别变化轴（认证方法×传输承载），在其间放稳定框架——EAP 消息封装多种认证方法（EAP-TLS/TTLS/GPSK 等），下垫 802.1X/EAPOL、PPP 等多种承载。
- **结论**: "怎么传"与"怎么验"分离——新增方法不改传输，链路更迭不改方法。
- **结果**: EAP 成为跨链路认证的标准框架。

### 案例 3: SPI 单一标识符解耦（第20章）
- **问题**: SA 机制与密钥管理如何互不牵连？
- **方法论的使用**: 接口收窄到单一标识符——SA 与密钥管理只经 SPI 联系，数据面查 SPI 即得全部安全参数。
- **结论**: 解耦的最小形态是"一个句柄"；两侧各自演进互不破坏。
- **结果**: IPsec 数据面与 IKE 演进相互独立。

---

## A2 — 触发场景 (Future Trigger) ★

### 用户会在什么情境下需要这个 skill?

1. 设计需 5–10 年演进的协议/凭证/消息格式（含抗量子字段预留）。
2. 老版本解析器遇新字段的行为设计（拒绝还是跳过）。
3. 评审"加字段"式的扩展方案或版本升级方案。
4. 两个快速变化的子系统之间的接口设计。

### 语言信号 (用户的话里出现这些就应激活)

- "向后兼容的格式演进 / forward compatible format"
- "critical extension / 必须理解的字段"
- "unknown field 怎么处理 / ignore unknown fields"
- "版本策略 / versioning strategy"
- "预留扩展位 / reserved for future use"

### 与相邻 skill 的区分

- 与 `stallings-protocol-migration-governance` 的区别: 那个管演进治理的节奏与决策（兼容层身份、退役表、砍 legacy 窗口），本 skill 管格式/接口层的演进机制设计（扩展点+criticality+解耦）——治理决策落到格式上就用本 skill。
- 与 `stallings-capability-negotiation-baseline` 的区别: 那个管协商时的选择规则与最低集（运行时行为），本 skill 管消息格式的扩展语义（解析时行为）——同一互操作问题的两个层面。
- 与 `stallings-algorithm-retirement-crypto-agility` 的区别: 那个定算法何时换，本 skill 定换算法时格式怎么装得下——敏捷性靠扩展点承接。

---

## E — 可执行步骤 (Execution)

1. **识别变化轴**：列出格式未来 5–10 年最可能变化的维度（算法、方法、承载、策略字段），区分独立变化的轴。
   - 完成标准: 变化轴清单成文。
   - 判停条件: 一次性短命消息格式（无演进预期）不需要扩展点，避免过度设计。
2. **定义扩展三件套**：每个扩展点规定标识+criticality 标志+值；criticality 默认策略显式声明（安全强制项默认 critical）。
   - 完成标准: 三件套规范成文，无"无判定规则的 reserved 位"。
3. **定默认行为并测试**：旧实现读新消息的用例——critical 扩展被整体拒绝、非 critical 被跳过，行为进解析器规范测试集。
   - 完成标准: 双向测试（旧读新/新读旧）通过。
4. **在变化轴间放稳定接口**：为独立变化的轴设计中间层或单一句柄（EAP/SPI 模式），避免每变一项 fork 协议。
   - 完成标准: 接口定义成文，两轴可独立演进。
5. **版本治理挂钩**：扩展注册与 criticality 升级纳入版本流程（与 v39 的退役表衔接）。
   - 完成标准: 治理流程引用到位。

---

## B — 边界 (Boundary) ★

### 不要在以下情况使用此 skill

- 把非 critical 当默认偷懒——安全强制项默认必须 critical，静默跳过=语义无声丢失。
- 为想象中的变化预留无语义的位——reserved 但无判定规则，只会制造歧义实现。

### 作者在书中警告的失败模式

- X.509 早期把时间戳校验当可选，反射冒充三消息得手（ce060）——"可选校验"是 criticality 缺省的反面教材。
- 扩展无约束也会出问题：证书路径约束类扩展正是为限定 CA 失误/恶意破坏的影响而设——扩展本身要参与范围治理。

### 作者的盲点 / 时代局限

- 书中样本是 X.509/EAP/SPI（成书 2017 前）；TLV 编码、protobuf unknown fields 等现代机制书内无内容，语义对照（如 proto3 默认忽略未知字段≈全部非 critical）需自行完成。

### 容易混淆的邻近方法论

- v39 演进治理（节奏）、v49 协商规则（运行时）、v15 密码敏捷（算法轴）。

---

## 相关 skills (阶段 3 定稿)

- **composes-with**: `stallings-capability-negotiation-baseline` —— 协商（运行时选择）与扩展点（解析时忽略语义）同属互操作演进的两个层面。

---

## 审计信息

- **验证通过**: V1 ✓ / V2 ✓ / V3 ✓
- **测试通过率**:
- **蒸馏时间**: 2026-11-10
