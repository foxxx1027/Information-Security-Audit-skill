---
name: stallings-cheap-check-first
description: |
  抗资源耗尽与省打扰的排序律：把带密钥的廉价校验排在昂贵操作之前——Cookie 往返先证源可达再放行 DH；ICV 对密文计算使解密前即丢伪造包；离线证书检查先于交互 PIN。不适用于：威胁模型无资源耗尽的内网受控环境、不带密钥的纯性能 fail-fast（那会制造新旁路）。关键 trigger：handshake flood、clogging attack、握手洪泛 CPU 打满、spoofed source address、先证可达再做昂贵计算、stateless cookie。
source_book: Information-Security-Audit-Skill 技能库
source_chapter: 第20章 20.5.1；第15章 15.6；第13章 13.5；第20章 20.3
tags: [dos-resistance, ordering, cookie, verification-pipeline, protocol-design]
related_skills:
  - slug: stallings-precompute-offline-split
    relation: contrasts-with
  - slug: stallings-side-channel-mitigation-ladder
    relation: contrasts-with
  - slug: stallings-crypto-operation-ordering
    relation: composes-with
  - slug: stallings-two-phase-gated-access
    relation: composes-with
---

# 廉价验证前置排序

## R — 原文 (Reading)

> "具有很强的可计算性。当攻击者申请许多密钥时，受害者很容易受阻塞攻击（clogging attack）。受害者需要花费相当多的资源做无意义的乘方、取模运算。"
>
> — 方法论出处，第20章 20.5.1 密钥确定协议（[HUIT98]）

---

## I — 方法论骨架 (Interpretation)

把"带密钥的廉价校验"排在"昂贵计算"之前，是抗资源耗尽与省打扰的统一排序律。它不是工程上的 fail-fast 常识，而有三个安全特化点：

1. **廉价检查必须带密钥/绑定本地秘密**——否则校验点自身可被伪造，成为新旁路。
2. **前置的目的是让伪造源付出代价**：Cookie 型往返中，源地址伪造者收不到回执，永远进不了昂贵阶段。
3. **按成本升序排**：离线静态检查（格式、证书链）→ 本地廉价密码校验（MAC）→ 昂贵交互（模幂、PIN、质询）。

Cookie 的三条生成要求是可验收的：与特定通话方绑定、由本地秘密生成且无需存储即可验证、生成验证足够快。验证链中把"对已知常数的断言"前置，还能让格式错误早暴露、可定位。

---

## A1 — 书中的应用 (Past Application)

### 案例 1: IKE 的 Cookie 闸门（第20章）
- **问题**: 裸 DH 计算昂贵，攻击者伪造源地址大量申请密钥，受害者做无意义模幂直至瘫痪（阻塞攻击）。
- **方法论的使用**: DH 交换前先做 Cookie 交换——初始报文带伪随机 Cookie 且必须在 DH 第一条报文中重复；源地址伪造者收不到回执，"只能要求用户生成确认报文但不可能要求用户执行 Diffie-Hellman 计算"。
- **结论**: 便宜的往返证明源可达，才解锁昂贵计算；Cookie 按三要求生成（绑定通话方/本地秘密可验证/足够快）。
- **结果**: IKE 五特性之首即防阻塞，"保持了 Diffie-Hellman 优点而去掉了其缺点"。

### 案例 2: ESP 的 ICV 前置（第20章）
- **问题**: 解密昂贵，伪造与重放包不应消耗解密资源。
- **方法论的使用**: ICV 对密文计算（带密钥的廉价校验），解密前即可丢弃不合法包。
- **结论**: 认证前置是抗 DoS 的结构手段，与覆盖域语义（v29）分开论证。
- **结果**: 成为 IPsec 入站处理三步的标准次序。

### 案例 3: PIV 认证三关顺序（第15章）
- **问题**: 持卡人认证要做证书链、PIN、密码学质询三类检查，顺序如何定？
- **方法论的使用**: 按成本升序——先离线验卡证书（无交互），再交互 PIN，最后密码学质询。
- **结论**: 便宜的离线检查先挡住大部分无效尝试，昂贵的密码学操作只对已过滤对象执行。
- **结果**: PIV 保障级别机制定型为证书→PIN→挑战响应的标准次序。

---

## A2 — 触发场景 (Future Trigger) ★

### 用户会在什么情境下需要这个 skill?

1. 服务被连接洪泛/握手洪泛打满 CPU（IoT 网关、UDP 服务、TLS 握手放大）。
2. 设计认证/握手流程，需要决定各检查的先后次序。
3. 高吞吐包处理路径需要"快速过滤+慢速处理"两级结构。
4. 验证函数太慢且错误不可定位，需要重排验证链。

### 语言信号 (用户的话里出现这些就应激活)

- "握手洪泛/CPU 被打满 / handshake flood, clogging attack"
- "先验什么再算什么 / cheap validation before expensive crypto"
- "无状态 cookie / stateless cookie exchange"
- "伪造源地址 / spoofed source address"
- "验证是瓶颈 / verification is the bottleneck"

### 与相邻 skill 的区分

- 与 `stallings-crypto-operation-ordering` 的区别: 那个是语义/责任视角（可见性、可仲裁性），本 skill 是成本/DoS 视角；ESP 的 ICV 对密文计算同属两者——本 skill 解释为什么前置，那个解释覆盖域防什么。
- 与 `stallings-two-phase-gated-access` 的区别: 那个是"认证与密钥就绪"的全局状态机结构，本 skill 是单条流水线内的检查排序；先选状态机再排管线。
- 与工程 fail-fast 常识：不带密钥的早退只是性能优化，甚至引入旁路——本 skill 的关卡必须带密钥或绑定秘密。

---

## E — 可执行步骤 (Execution)

1. **列成本表**：写出请求处理路径全部步骤，标注相对成本（CPU/内存/交互轮次）与是否带密钥。
   - 完成标准: 成本表成文，最贵步骤被明确标出。
   - 判停条件: 若威胁模型确认不含资源耗尽（封闭受控环境），停在此步记录豁免理由。
2. **在第一个昂贵步骤前找关卡**：问"在此之前有没有带密钥的廉价往返/校验可挡住伪造源？"
   - 完成标准: 每个昂贵步骤之前至少有一个带密钥关卡，或书面说明为何不需要。
3. **设计 Cookie 型闸门时核对三要求**：绑定通话方、本地秘密生成且免存储可验证、足够快。
   - 完成标准: 三要求逐条有实现方案与测试。
4. **把离线可判检查前移**：格式校验、证书链检查移到任何交互之前。
   - 完成标准: 交互发生时对象已通过全部离线检查。
5. **验证链前置常数断言**：对已知常数逐一断言后再做摘要比对，让格式错误早暴露可定位。
   - 完成标准: 恶意/畸形输入在第一阶段被拒且错误可定位。

---

## B — 边界 (Boundary) ★

### 不要在以下情况使用此 skill

- 内网受控环境且无资源耗尽威胁——为排序增加状态不值得。
- 纯性能优化场景无安全语义时——普通缓存排序即可，勿引入密钥关卡。

### 作者在书中警告的失败模式

- Cookie 不满足三要求（可伪造或拖慢）则闸门自身失效。
- SSH 跳过主机密钥验证"短期内有实际意义"但对主动攻击脆弱（ce079）——便宜不能以跳过认证为代价。

### 作者的盲点 / 时代局限

- 书中 DoS 对策止于 Cookie 型闸门与故障安全默认（成书 2017 前），未涉及 proof-of-work、速率限制等更广谱手段；外推时需注明这是书外扩展。

### 容易混淆的邻近方法论

- fail-fast 工程常识（无密钥、无攻击者模型）。
- v45 两阶段开门（状态机结构而非单管线排序）。

---

## 相关 skills (阶段 3 定稿)

- **contrasts-with**: `stallings-precompute-offline-split` —— 同是重排计算：本 skill 把廉价检查放前挡 DoS，那个把昂贵计算移出关键路径提速——目标相反，可同管线并用。
- **contrasts-with**: `stallings-side-channel-mitigation-ladder` —— "把耗时操作移走"不等于"时间恒定"：排序省资源 vs 消除数据相关性，两回事。
- **composes-with**: `stallings-crypto-operation-ordering` —— 成本/DoS 视角的排序（便宜带钥校验前置）与语义/责任视角的次序学同管线并用，ESP 的 ICV 前置是交叉点。
- **composes-with**: `stallings-two-phase-gated-access` —— 先定全局状态机（哪扇门何时开），再排单条管线内的检查次序——结构在前、排序在后。

---

## 审计信息

- **验证通过**: V1 ✓ / V2 ✓ / V3 ✓
- **测试通过率**:
- **蒸馏时间**: 2026-11-10
