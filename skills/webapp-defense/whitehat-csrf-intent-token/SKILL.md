---
name: whitehat-csrf-intent-token
description: |
  CSRF 本质定性：重要操作参数全部可猜测+浏览器自动携带凭据→攻击者能拼出完整伪造请求。防御统一为引入攻击者拿不到的意图凭证（Token：安全随机、双端比对、不进 URL、消耗后更新、框架级统一实施），并遵守依赖顺序——存在 XSS 则 Token 被读取（XSRF），先修 XSS；"改 POST 即防"已被 Gmail 案例证伪。适用于写接口防伪造设计、CSRF 审计（先问哪些凭据被自动携带）。触发词：CSRF、跨站请求伪造、Token、自动带 Cookie、POST 防得住吗、SameSite、XSRF。不适用于：XSS 本身防御、点击劫持。
source_book: Information-Security-Audit-Skill 技能库
source_chapter: 第 4 章 跨站点请求伪造 4.3.3；第 12 章 12.3
tags: [CSRF, token, intent-credential, session]
related_skills:
  - slug: whitehat-unpredictability
    relation: depends-on
  - slug: whitehat-signal-reliability
    relation: composes-with
---

# CSRF 的本质与意图凭证防御

## R — 原文 (Reading)

> "CSRF为什么能够攻击成功？其本质原因是重要操作的所有参数都是可以被攻击者猜测到的。"
> "XSS带来的问题，应该使用XSS的防御方案予以解决，否则CSRF的Token防御就是空中楼阁。"
>
> — 方法论出处，第 4 章《跨站点请求伪造》4.3.3.1 / 4.3.3.2

---

## I — 方法论骨架 (Interpretation)

CSRF 能成立，靠的是两件事同时为真：浏览器对目标站的请求**自动携带凭据**（Cookie 随发），且该操作的**全部参数可被攻击者猜到或预构造**。于是攻击者在自己页面里就能拼出一个完整请求，受害者的浏览器替它带上身份发出去——服务端只认凭据，不认本意。

防御因此只有一条主线：**往请求里塞进攻击者拿不到、也猜不到的东西**，把"是否用户本意"变成可验证的。Anti-CSRF Token 是标准实现，工程要点缺一即失效：

1. 安全随机数生成（不可预测原则的落地）；
2. 双端持有、服务端比对（Session 与表单各一份）；
3. 不进 URL（会随 Referer 外泄给第三方）；
4. 一次性消耗后更新、多页面共存多 Token；
5. 框架级统一实施——逐页手工必遗漏。

两条配套纪律：**依赖顺序**——存在 XSS 时攻击者直接读走页面里的 Token（XSRF），所以先修 XSS，Token 才有意义；**按凭据携带方式审计**——判断某接口有没有 CSRF 面，先问"哪些凭据会被浏览器自动带上"，而不是看请求方法（"改 POST 即防"已被 Gmail 案例证伪，POST 表单同样可被 JS 自动提交）。

---

## A1 — 书中的应用 (Past Application)

### 案例 1: 从"本质"推出 Token（第 4 章 4.3.3.1）
- **问题**: 防御 CSRF 的手段五花八门（改 POST、验 Referer、验证码、Token），哪个是正解。
- **方法论的使用**: 先定本质——参数全可猜测 + 凭据自动携带；再验证各手段：直接对参数做 md5(salt+username) 哈希可行但伤 URL 可读性与统计，于是演进为独立 Token；改 POST 被证伪；Referer 只满足充分条件；验证码体验上无法全量。
- **结论**: 一切有效手段都指向同一目标"区分是否用户本意"，最优实现是引入不可预测的意图凭证。
- **结果**: 产出 Token 使用原则四条（随机/双端比对/不进 URL/消耗后更新），成为后续工程实施纲。

### 案例 2: 2007 Gmail CSRF——POST 不是护身符（第 4 章 4.2.3）
- **问题**: "重要操作改成只允许 POST 就安全"是流行观点，如何证伪。
- **方法论的使用**: 按本质分析——POST 表单同样可被跨站自动提交：攻击页构造 form、JS 自动 submit、藏进不可见 iframe，请求照带 Cookie。
- **结论**: Gmail 案例中攻击者借此创建了一条自动转发所有带附件邮件的 Filter，静默且难察觉。
- **结果**: "把安全寄托在单一请求方法上是假防线"成为定论，审计时不能因接口是 POST 就判无 CSRF。

### 案例 3: 框架级四步与逐页手工的对比（第 12 章 12.3）
- **问题**: 大型站点成百上千个写接口，逐页加 Token 为什么必失败。
- **方法论的使用**: 把 Token 工程化为框架四步——Session 绑定 token、所有 form 自动填隐藏 token、所有 Ajax POST 自动带头、服务端统一校验；只绑定敏感操作以降成本。
- **结论**: 依靠人工在每个页面插 token 必然遗漏，"全局管理才防得住漏配"。
- **结果**: Rails/Django 的 CSRF 中间件模式成为范式；同时确立依赖顺序——站内有 XSS 时 Token 被 XSRF 读取，先修 XSS。

---

## A2 — 触发场景 (Future Trigger) ★

### 用户会在什么情境下需要这个 skill?

1. 设计写操作/资金操作/后台接口的防伪造方案，选 Token、SameSite、验证码还是组合。
2. 审计已有接口的 CSRF 面：哪些凭据被浏览器自动携带、哪些参数可预构造。
3. Token 方案实现评审（生成、存放、传递、校验、生命周期各环节）。
4. 排查"接口明明只收 POST 为什么还能被伪造"的困惑。
5. 混合架构（App 用 Bearer 头、Web 用 Cookie、混合开发把 token 写回 Cookie）下的 CSRF 风险变化判断。

### 语言信号 (用户的话里出现这些就应激活)

- "怎么防 CSRF？加个 Token 就行了吗？"
- "接口只允许 POST，还会有 CSRF 吗？"
- "Token 放 URL 里方便跳转，有问题吗？"
- "SameSite Cookie 是不是就不用 Token 了？"
- "how to prevent CSRF / is POST enough / token in URL safe / SameSite vs CSRF token"

### 与相邻 skill 的区分

- 与 `whitehat-unpredictability` 的区别: 那个是一般原则（一切关键值不可猜）；本 skill 是该原则在 CSRF 场景的完整工程化——本质定性、Token 清单、依赖顺序、框架落地。归因到"参数可预测"用那个的思维，落地方案用本 skill。
- 与 `whitehat-signal-reliability` 的区别: 那个给防御候选信号分级（Referer 可缺失、Origin 更强）；本 skill 统摄 CSRF 防御全案并确立"意图凭证为主、来源信号为辅"的结构。
- 与 `whitehat-defense-at-interpretation` 的区别: 那个裁决"编码/校验放在数据旅程哪一环"；本 skill 防的是"请求是否本人意图"，作用在请求维度而非数据渲染维度。

---

## E — 可执行步骤 (Execution)

当 skill 被激活后， agent 应按以下步骤执行：

1. **盘点自动携带的凭据**：列出浏览器对目标站发请求时自动带上的东西（Cookie、HTTP 认证、客户端证书），标注哪些接口依赖它们做身份判定。
   - 完成标准: "凭据 × 写操作接口"矩阵完成；无自动凭据的接口（显式头携带的 Bearer）标注"传统 CSRF 不成立"并检查是否有写回 Cookie 的例外。
   - 判停条件: 若所有写接口的凭据均需 JS 显式设置且不落 Cookie，CSRF 面为空，输出结论并转向 XSS/令牌存储审计。
2. **核对参数可预测性**：对每个写接口检查参数是否全部可由第三方预构造（无服务端签发的一次性值）。
   - 完成标准: 每个写接口标注"全可猜（有 CSRF 面）/含不可猜参数"。
3. **实施意图凭证**：按五要素落 Token——安全随机生成、双端绑定、表单/头传递且不进 URL、消耗后更新、框架级统一注入与校验；只覆盖写操作以控成本。
   - 完成标准: 抽查任意写接口均含服务端校验逻辑；全站搜不到 Token 拼 URL 的写法。
4. **检查依赖顺序**：确认站内 XSS 修复状态——存在存储/反射 XSS 的域上 Token 可被读取，先修 XSS 或对高危操作加二次确认/验证码兜底。
   - 完成标准: "XSS 已修/未修 × Token 生效域"结论明确；未修区域的补偿措施上线。
5. **验证与回归**：构造跨站自动提交（隐藏 iframe + JS form）对 POST 与 GET 写接口各测一次；对 Token 生命周期测重放与并发多页面。
   - 完成标准: 伪造请求全部被拒；多标签页正常使用不误杀；Token 消耗后旧值失效。

---

## B — 边界 (Boundary) ★

### 不要在以下情况使用此 skill

- XSS 本身的防御——Token 防"借用身份的静默请求"，不防注入脚本（那走输出编码）；依赖顺序恰说明两者不能互替。
- 点击劫持——同样是"借用户之手"，但载体是视觉欺骗下的真实点击，防的是 X-Frame-Options/CSP frame-ancestors 一类嵌入控制。
- 登录 CSRF（强制登录进攻击者账户）之外的会话固定等问题——那是凭证轮换纪律（Session Fixation）的领域。

### 作者在书中警告的失败模式

- "改 POST 即防 CSRF"：Gmail 案例实证 POST+multipart 照样被自动提交——请求方法不是安全边界。
- Token 进 URL：随 Referer 外泄给第三方（书中给出 img 指向 evil.com 的具体外泄场景）。
- XSRF 击穿：站内有 XSS 时 Token 被直接读取——防御体系有依赖顺序，"相辅相成、缺一不可"。
- 逐页手工加 Token：大型应用必然遗漏——必须框架级全局实施。

### 作者的盲点 / 时代局限

- 成书早于 SameSite Cookie（书出版时无此属性）：现代浏览器下 Lax 默认已成第一道缓解，但 SameSite 可被子域与特定导航场景绕过，本书"服务端意图凭证为主"的结论依然成立，需补充两者的组合关系。
- OAuth 2.0/SPA（Bearer 头、state 参数、CSRF 与 OAuth state 的关系）未覆盖，引用时按"凭据携带方式"判据自行推导。

### 容易混淆的邻近方法论

- 验证码：同为意图验证，但体验约束决定它只能覆盖高敏感低频操作，是辅助手段而非主防线（见 `whitehat-mitigation-vs-fix` 的分级）。
- 一次性凭证纪律（登录轮换、消费即作废）：Token 的"消耗后更新"与其同源，但那套纪律管一切状态跃迁，CSRF Token 只是其一。

---

## 相关 skills

- **`whitehat-unpredictability`** (depends-on) — Token 必须"安全随机、攻击者拿不到"的要求来自不可预测性原则；本 skill 是该原则在 CSRF 场景的完整工程化。
- **`whitehat-signal-reliability`** (composes-with) — 防御结构"意图凭证为主、来源信号为辅"，辅助信号选型（Origin 优于 Referer）由那个的可伪造/可缺失分级决定。
---

## 审计信息

- **验证通过**: V1 ✓ / V2 ✓ / V3 ✓
- **测试通过率**: （留空，见 test-prompts.json）
- **蒸馏时间**: 2026-11-10
