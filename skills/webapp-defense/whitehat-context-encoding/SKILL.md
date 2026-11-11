---
name: whitehat-context-encoding
description: |
  没有万能转义函数：输出场景→编码一一对应（HTML 正文 HtmlEncode、script/事件 JavascriptEncode+引号、CSS 禁止或专用编码、URL URLEncode+协议白名单）；DOM XSS 每一跳都是新输出，须逐跳按目标语境重编码，服务器端编码管不到 JS 中段。用于 XSS 防御实现、auto-escape 能力评估、前端渲染（innerHTML/属性/href）注入排查。触发词：转义、escape、HtmlEncode、auto-escape、innerHTML、context-aware encoding。不适用于：防线放哪的裁决（用解释发生处技能）、富文本白名单设计。
source_book: Information-Security-Audit-Skill 技能库
source_chapter: 第 3 章 3.3.3–3.3.4；第 12 章 12.2
tags: [output-encoding, XSS, context-aware, DOM-XSS]
related_skills:
  - slug: whitehat-defense-at-interpretation
    relation: depends-on
  - slug: whitehat-whitelist-first
    relation: contrasts-with
  - slug: whitehat-source-sink-audit
    relation: composes-with
---

# 输出语境 × 编码矩阵与 DOM XSS 逐跳编码

## R — 原文 (Reading)

> "导致XSS攻击发生的原因，是由于没有分清楚输出变量的语境！因此并非在模板引擎中使用了auto-escape就万事大吉了，XSS的防御需要区分情况对待。"
> "也就是说，从JavaScript输出到HTML页面，也相当于一次XSS输出的过程，需要分语境使用不同的编码函数。"
>
> — 方法论出处，第 3 章《跨站脚本攻击 XSS》3.3.3.2 / 3.3.6

---

## I — 方法论骨架 (Interpretation)

"转义了"不等于"安全了"。转义是否有效取决于**接收方是谁**：同一份 HtmlEncode 后的数据放进 HTML 正文是安全的，放进事件属性则被 HTML 实体解码还原，JS 拿到的仍是原始攻击载荷。所以编码不是一个函数，而是一张矩阵——先枚举输出场景，再为每个场景指定专用编码：

- HTML 标签内容 → HtmlEncode（最小字符集含 `& < > " ' /`，表要完整照抄标准）；
- `<script>` 内与事件属性 → JavascriptEncode，且变量必须包在引号内（编码+引号成对）；引号无保证时用严格版（非字母数字全 `\xHH`）；
- CSS/style → 尽量禁止用户输入，必须允许时用专用编码器；
- URL 参数 → URLEncode；变量是完整 URL 时先做协议白名单（防 `javascript:` 伪协议），再编码余下部分。

第二条规则管住数据在浏览器内的旅程：**每一跳都是一次新的输出**。数据从服务器到 `<script>` 是一跳，从 JS 再 `document.write`/`innerHTML` 写到页面又是新的一跳——上一跳的编码在下一跳会被解码消费，必须按新跳的目标语境重新编码。服务器端编码天然管不到 JS 中段，DOM XSS 的审计因此变成 source 清单（location/referrer/cookie/input）× sink 清单（write/innerHTML/location）的逐跳核对。

---

## A1 — 书中的应用 (Past Application)

### 案例 1: auto-escape 在事件属性上失效（第 3 章 3.3.3.2）
- **问题**: 模板引擎开了默认转义，为何 onclick 里的变量仍被执行。
- **方法论的使用**: 按矩阵分析解码顺序——htmlparser 先于 JS parser 执行，`onclick="alert('$var')"` 中 HtmlEncode 的实体会被解码回原始字符，JS 事件拿到的还是攻击载荷。
- **结论**: 默认转义只覆盖 HTML 正文语境；"同一编码在错误语境无效"，必须按语境选函数。
- **结果**: 评估模板引擎 XSS 能力的标准定为"是否区分六类上下文并提供对应编码"，Django 默认 escape 只是"值得称道的好起点"。

### 案例 2: 统一 5 字符 HtmlEncode 的绕过（第 12 章 12.2）
- **问题**: Django/Velocity 类框架统一用一个 HtmlEncode（5 字符），为何书断言"很可能会被攻击者绕过"。
- **方法论的使用**: 对照矩阵找缺口——统一编码在 script、事件、URL、CSS 语境全部错配；且为方便程序员常被 `|safe`/`autoescape off` 关闭。
- **结论**: "默认安全"不等于"全场景安全"，框架级方案须按上下文自动选择编码，并补自定义 filter/宏。
- **结果**: 输出编码矩阵成为框架 XSS 防御的验收清单（标签内/属性/script/事件/CSS/URL 逐项核对）。

### 案例 3: DOM XSS 逐跳重编码（第 3 章 3.3.6）
- **问题**: 服务器端已对变量做了 javascriptEncode，经 `document.write` 输出后事件属性为何仍被注入。
- **方法论的使用**: 画出数据流"JS 读入→JS 写出"：script 内的编码在写入 HTML 时被浏览器解码后再渲染，事件属性拿到的又是原始载荷；换 HtmlEncode 同样在另一跳失效。
- **结论**: 每一跳都是新输出，都要按该跳的目标语境重新编码；以 sink×source 清单配对做污点追踪，逐跳核对编码。
- **结果**: YUI History Manager（信任 hash 变量 fqstate）等框架漏洞的修补（htmlEscape 该变量）验证了方法：官方修复正是"按输出语境编码"。

---

## A2 — 触发场景 (Future Trigger) ★

### 用户会在什么情境下需要这个 skill?

1. 实现或评审 XSS 防御：写输出编码逻辑、选模板引擎、评估 auto-escape 是否够用。
2. 前端渲染用户数据（innerHTML、属性、href、style、事件绑定）时判断要不要处理、怎么处理。
3. WebSocket/SSE/JSON API 推送的消息在前端渲染，疑心服务器编码管不管用。
4. 框架选型/升级：评估其上下文感知编码能力（是否区分六类场景）。
5. 排查"转义了还是被 XSS"的存量问题。

### 语言信号 (用户的话里出现这些就应激活)

- "用了 escape 怎么还是被 XSS？"
- "auto-escape 开了是不是就防住 XSS 了？"
- "前端 innerHTML 渲染接口返回的富文本/消息，怎么防？"
- "变量进了 onclick/href 还要处理吗？"
- "escaped but still XSS / is auto-escape enough / how to render user HTML safely"

### 与相邻 skill 的区分

- 与 `whitehat-defense-at-interpretation` 的区别: 那个裁决防线放在哪一环（位置）；本 skill 在位置确定后给出"每个语境用哪种编码"的矩阵与逐跳规则（选型）。定完位再用本 skill。
- 与 `whitehat-whitelist-first` 的区别: 富文本处理两者都涉及但分工不同——标签/属性集合的取舍用白名单原则，非富文本的输出编码用本矩阵。
- 与 `whitehat-source-sink-audit` 的区别: DOM XSS 审计时那个提供 source/sink 枚举框架（找路径）；本 skill 提供每条路径上"用什么编码"的判定（修路径）。

---

## E — 可执行步骤 (Execution)

当 skill 被激活后， agent 应按以下步骤执行：

1. **枚举输出场景**：列出数据的全部落点并分类——HTML 正文、HTML 属性、script 块、事件属性、CSS/style、URL（参数 vs 完整 URL）、JS 字符串/JSON。
   - 完成标准: 一张"输出点 → 语境类型"清单，覆盖服务端模板与浏览器端（DOM）两侧。
2. **逐场景指定编码**：按矩阵为每类语境绑定专用编码；核对转义字符集完整（HtmlEncode 含 `/`；JS 编码配引号；整 URL 前置协议白名单）。
   - 完成标准: 每个输出点的编码函数与语境一一对应，无"统一转义函数"残留。
   - 判停条件: 若某输出点无法确定语境（数据去向动态不定），把该输出点升级为设计问题——收敛数据去向或改为白名单净化，不在原处硬编码。
3. **追浏览器内的每一跳**：对进入 JS 的数据画出"读入→中间处理→写出"全链，每跳标注目标语境与所用编码；source（location/referrer/cookie/input/消息通道）× sink（write/innerHTML/属性赋值/location 跳转）配对核对。
   - 完成标准: 每跳有独立编码动作；不存在"上一跳编码给下一跳用"的路径。
4. **实现选择**：优先框架/库的上下文感知编码（模板 auto-escape 仅作 HTML 正文基线）；富文本走解析后白名单净化（另见白名单技能）；DOM 构建优先 textContent/DOM API 而非字符串拼接。
   - 完成标准: 编码动作成为渲染路径的默认行为而非开发者临场记忆；`|safe`/`autoescape off` 类豁免点有清单。
5. **绕过验证**：对每个场景做错配测试——HtmlEncode 后的数据塞进事件属性看是否还原执行；伪协议 `javascript:` 塞完整 URL 看是否被协议白名单拦截。
   - 完成标准: 六类场景各有"错配输入被正确处理"的证据。

---

## B — 边界 (Boundary) ★

### 不要在以下情况使用此 skill

- 还没定防线位置（入口/出口之争）——先用"防线放在解释发生处"裁决，本 skill 只管位置定了之后的编码选型。
- 富文本的结构清洗（允许哪些标签）——白名单原则的领域；本 skill 处理的是"非富文本的普通数据按语境编码"。
- 非 HTML 语境注入（SQL、命令）——"按语境选编码"的思路相通，但具体矩阵不同，用数据与代码分离技能推导。

### 作者在书中警告的失败模式

- 一个 escape 函数走天下：统一 5 字符 HtmlEncode 在 script/事件/URL/CSS 全部错配——"一个通用转义函数覆盖所有输出点，是对抗性场景里的虚假安全感"。
- 相信 auto-escape 万事大吉：书中点名这是错误观点；默认转义只是好起点，且常被 `|safe` 关掉。
- 服务器编码覆盖 DOM：DOM XSS 的中段在浏览器里，服务器端方案"并不适用"——防线与数据流不匹配。

### 作者的盲点 / 时代局限

- 六类语境矩阵基于 2014 年浏览器与模板引擎；现代前端（React/Vue 的转义边界、`dangerouslySetInnerHTML`、CSP nonce）扩展了场景清单，但"语境决定编码、逐跳重编码"两条规则不变。
- 未覆盖 JSON 响应头的 `Content-Type` 纪律与 `X-Content-Type-Options`（JSON 数据被嗅探为 HTML 的新语境），引用时补。

### 容易混淆的邻近方法论

- 输入校验：改数据内容 vs. 按消费点编码——位置与职责不同（详见 `whitehat-defense-at-interpretation`）。
- HTML 净化（sanitize）：解析后重建文档并按白名单保留节点，用于"数据本身是 HTML"的场景；本 skill 的编码用于"数据是纯文本"的场景——用错对象两头出错。

---

## 相关 skills

- **`whitehat-defense-at-interpretation`** (depends-on) — 先用那个裁决"防线放在输出点"，再进入本 skill 的语境→编码矩阵选函数；定位错了，矩阵再全也无效。
- **`whitehat-whitelist-first`** (contrasts-with) — 输出处理按情境二选一：非富文本输出用本 skill 的语境编码，富文本用那个的标签白名单过滤。
- **`whitehat-source-sink-audit`** (composes-with) — DOM XSS 审计中那个找 source→sink 路径，本 skill 定每条路径终点用哪种编码——找面与修面接力。
---

## 审计信息

- **验证通过**: V1 ✓ / V2 ✓ / V3 ✓
- **测试通过率**: （留空，见 test-prompts.json）
- **蒸馏时间**: 2026-11-10
