---
name: caudit-mechanism-to-search-terms
description: |
  对某类漏洞做白盒定向挖掘时调用：先吃透该漏洞的触发机理，再由机理现场推导搜索词（不是背危险函数清单），搜到 sink 后回溯参数可控性、并判定过滤是否充分。机理变则搜索词变，方法不变——可迁移到 NoSQL 注入、GraphQL、SSTI 等任何新场景。不适用于：逻辑漏洞（无关键字可搜，用逻辑漏洞方法论）。触发词：怎么搜漏洞 / how do I grep for this vuln、sink / 危险函数、关键字定向 / keyword-driven audit、NoSQL 注入怎么挖、机理 / mechanism。
source_book: Information-Security-Audit-Skill 技能库
source_chapter: 第4–6章（4.1/4.2/5.1/5.2/5.3/6.1），全书挖掘章节的统一体例
tags: [code-audit, taint-analysis, sink-search, vulnerability-mechanism]
related_skills:
  - slug: caudit-audit-path-selection
    relation: depends-on
  - slug: caudit-logic-vuln-audit
    relation: contrasts-with
  - slug: caudit-structured-full-read
    relation: contrasts-with
  - slug: caudit-escape-as-last-step
    relation: composes-with
  - slug: caudit-type-context-defense
    relation: composes-with
  - slug: caudit-patch-diff-remediation
    relation: composes-with
  - slug: caudit-var-overwrite-chain
    relation: composes-with
---

# 机理驱动的定向挖掘三步法（vf03）

## R — 原文 (Reading)

> 「既然知道了原理…搜索urldecode和rawurldecode」（SQL 注入章）；第5章按机理给出 include 四函数、move_uploaded_file、命令执行七函数加反引号等各自的关键字清单
>
> — 原作者, 原始方法论来源第4章 4.1（source.txt 行4377；另见行5907/6321/7989/8441）

---

## I — 方法论骨架 (Interpretation)

挖掘工作流把"知道漏洞原理"和"搜代码"接成一条单向推导链，方向不能反：

1. **先写机理**：这类漏洞要成立，代码里必须出现什么结构？例如 SQL 注入 = 用户数据未参数化地进入 SQL 语义；命令执行 = 用户数据进入 shell 解释器；变量覆盖 = 请求数据注册进已有变量名。
2. **由机理现场推出搜索词**：搜索词是机理的函数，不是背诵清单。换语言/换组件时清单全变（PHP 的反引号对应 Node 的 child_process、MongoDB 的 db.collection.find），但"由机理推词"这步不变。机理理解错，搜索词就全错——所以推不出的地方先回炉机理。
3. **回溯可控性 × 过滤充分性**：搜到 sink 只是候选。逐个回溯参数来源回答两个问题——参数真的可控吗（入口可达、中间无阻断）？过滤对**这个语境**够吗（转义是否最后一步、类型是否锁定）？两问都过才算漏洞。

书中每章都按"知道了原理 → 就可以通过搜索 X 来挖掘"组织，这个体例本身就是方法。第三步的双问把静态搜索和"有过滤 ≠ 安全"的判定接起来，避免报告里堆满误报。

---

## A1 — 书中的应用 (Past Application)

### 案例 1: espcms 搜索注入——三步完整走一遍
- **问题**: 演示回溯法如何从可疑点到坐实漏洞。
- **方法论的使用**: 自动审计列出可疑 echo/$sRst → 回溯 accept()/daddslashes() 取参链 → 确认 $_GET 可达且过滤在解码之前失效。
- **结论**: 参数可控 + 过滤不足（顺序错位）双问皆过。
- **结果**: 坐实注入点（3.1 节；作者 2013 年亲自发现的同型漏洞在 4.1.1.3 完整分析）。

### 案例 2: 亿邮命令执行——机理推出"反引号"这个易漏 sink
- **问题**: 命令执行的 sink 清单里最容易被忽略的是什么。
- **方法论的使用**: 先实证反引号等价 shell_exec（机理校准），再在亿邮 /swfupload/upload_files.php 追 $uid/$domain 从 GET 到反引号的完整链。
- **结论**: 机理理解完整（含反引号）后搜索词才不漏；命令不出网时用带外域名验证。
- **结果**: 漏洞确认，可注入命令写文件（5.3.1.3，作者本人挖掘）。

### 案例 3: 变量覆盖同法实例化
- **问题**: 方法是否只在注入类成立。
- **方法论的使用**: 第6章对 extract/parse_str/$$ 按同一流程：机理（请求注册变量）→ 搜 $$ 与 extract( → 回溯覆盖面与消费点。
- **结论**: 三步法是跨漏洞类型的统一工作流，函数清单只是载荷。
- **结果**: Metinfo $$ 覆盖连数据库配置一起覆盖的完整链被挖出（6.1.1.3）。

---

## A2 — 触发场景 (Future Trigger) ★

### 用户会在什么情境下需要这个 skill?

1. 审计 Node.js + MongoDB 项目，要系统排查 NoSQL 注入（手册里的 PHP 清单完全用不上）。
2. 新框架/新组件（GraphQL resolver、模板引擎、消息队列消费者）没有现成 sink 清单，要自建检索词。
3. 给团队写某类漏洞的白盒审计 checklist / 检索规则。
4. SAST 工具规则自研：把某漏洞机理翻译成查询（Semgrep/CodeQL）。

### 语言信号 (用户的话里出现这些就应激活)

- "这类漏洞在代码里怎么搜 / what to grep for"
- "sink 清单 / dangerous functions list"
- "帮我审一下有没有命令注入 / SSRF / NoSQL injection"
- "机理是什么 / how does this vuln actually trigger"
- "搜索关键字从哪来 / where do search terms come from"

### 与相邻 skill 的区分

- 【依赖】`caudit-audit-path-selection`: 路径选型决定"走定向挖掘"之后才用本 skill；那边管选路，本 skill 管执行层的搜-判流程。
- 【组合】`caudit-escape-as-last-step` / `caudit-type-context-defense`: 那两个是本 skill 第三步"过滤充分性"判定的专项判据（转义位置 / 语境选型）——三步全流程与两个判据配套。
- 【对比】`caudit-logic-vuln-audit`: 逻辑漏洞无关键字，机理法失效，必须换应然/实然对照法——按漏洞类型二选一。
- 【对比】`caudit-structured-full-read`: 定向挖掘带着已知机理搜 sink，通读不带预设产出地图与覆盖表——两条执行路径按时间预算与目标归属选一。
- 【组合】`caudit-var-overwrite-chain`: 搜到覆盖点（本 skill 的发现阶段）之后，可利用性判定交给那边的三点连线（判定阶段）——两阶段首尾相接。
- 【组合】`caudit-patch-diff-remediation`: 那边从补丁 diff 反推漏洞模式后做全库检索，检索动作（机理→搜索词→回溯）复用本 skill。

---

## E — 可执行步骤 (Execution)

1. **写机理卡**：一段话写清该漏洞成立所需的完整结构（入口可控数据 → 变换 → 解释器/执行点），并列出"机理不确定之处"。
   - 完成标准: 机理卡能回答"缺了哪个环节漏洞就不成立"。
   - 判停条件: 若机理有未验证假设（如新数据库的解析行为），先用最小样例验证机理，验证不了就停止推导——机理错误则后续全部作废。
2. **现场推导搜索词**：从机理的每个环节反推代码形态（函数/方法/语法/配置），生成检索词表，标注每个词对应机理的哪一环。
   - 完成标准: 检索词表覆盖机理全部环节，无"直接抄旧清单"的词。
3. **全库检索得候选清单**：执行检索，记录命中位置。
   - 完成标准: 每个命中点标注所属 sink 类型。
4. **逐点回溯可控性**：从 sink 向入口回溯，判定参数是否真可控。
   - 完成标准: 每个候选标注"可控/不可控/待查"及理由。
   - 判停条件: 不可控且无二次污染路径的点直接关闭，不进入下一步。
5. **判定过滤充分性**：对可控点套用专项判据（转义是否最后一步、类型是否锁定、覆盖面是否含此入口）。
   - 完成标准: 输出"成立/被有效过滤/绕过路径"三态结论。

---

## B — 边界 (Boundary) ★

### 不要在以下情况使用此 skill

- 逻辑/越权/支付类问题——没有 sink 关键字，硬套只会浪费时间。
- 机理未验证的新奇漏洞传言——先做最小样例，否则搜索词全盘错误。
- 二进制/内存破坏类——"机理→关键字"工作流面向解释型注入面。

### 作者在书中警告的失败模式

- 清单偏见：作者明示报错注入"多数人以为只有三种…实际上还有很多"（8.7，行12821）——背清单的人永远落后于清单外的等价能力。
- 只搜到 sink 就下结论：不过滤可控性与过滤充分性的报告是误报制造机（第3章贯穿）。

### 作者的盲点 / 时代局限

- 书中搜索词全是 PHP 5.x 函数（mysql_*、preg_replace /e、%00 截断），语言载体已过时；迁移时保留"机理→搜索词"的推导方向，替换全部具体词。
- 现代框架的间接层（ORM、依赖注入、动态代理）使"回溯可控性"常常跨文件跨仓库，人工回溯成本剧增，应结合 taint 感知的 SAST 工具，但工具结论仍需按第三步双问人工复核。
- 未涉及反序列化 gadget 链等 2015 后成为主力的攻击面。

### 容易混淆的邻近方法论

- 与"跑扫描器"不同：扫描器输出的是候选清单（相当于第3步的产物），本方法要求机理卡先行与双问判定。
- 与 fuzz 互证法（书中 8.5）互补：静态定位 + 动态验证；本 skill 覆盖静态侧。

---

## 相关 skills

- **depends-on `caudit-audit-path-selection`**: 本 skill 是"定向挖掘/回溯"路径的执行层——路径选型确认走这条路之后才启动。
- **contrasts-with `caudit-logic-vuln-audit`**: 有 sink 关键字的技术型漏洞 vs 无关键字的逻辑漏洞，两套方法互斥，按漏洞类型选一。
- **contrasts-with `caudit-structured-full-read`**: 定向搜索与全文通读是两条并列的执行路径，按时间预算与目标归属在路径选型处二选一或组合。
- **composes-with `caudit-escape-as-last-step`**: 第三步"过滤充分性"的专项判据之一——列转义前后的变换清单。
- **composes-with `caudit-type-context-defense`**: 第三步"过滤充分性"的专项判据之一——按注入语境核对武器选型。
- **composes-with `caudit-var-overwrite-chain`**: 发现（搜覆盖点）与判定（三点连线）两阶段衔接——变量覆盖类候选交给那边定级。
- **composes-with `caudit-patch-diff-remediation`**: 补丁 diff 反推出漏洞模式后的"漏洞联想全库检索"复用本 skill 的三步流程。

---

## 审计信息

- **验证通过**: V1 ✓ / V2 ✓ / V3 ✓
- **测试通过率**: 
- **蒸馏时间**: 2026-11-10
