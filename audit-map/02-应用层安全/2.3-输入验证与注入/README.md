# 2.3-输入验证与注入 —— 技能说明

## 本子域审计范围

SQL注入、NoSQL注入、XSS（反射/存储/DOM）、CSRF、SSRF、XXE、路径遍历、文件包含、开放重定向、模板注入、不安全反序列化、文件上传漏洞（webshell）。

## 技能清单（19 个）

| 集合 | 技能 | 一句话说明 | 归类理由 |
|---|---|---|---|
| Web应用防御 | `whitehat-context-encoding`<br>[输出语境编码矩阵](../../../skills/webapp-defense/whitehat-context-encoding/SKILL.md) | 无万能转义：按输出场景对应编码，DOM XSS每跳按目标语境重编码 | XSS防御编码选型，注入防治核心 |
| Web应用防御 | `whitehat-csrf-intent-token`<br>[CSRF意图凭证防御](../../../skills/webapp-defense/whitehat-csrf-intent-token/SKILL.md) | CSRF本质是参数可猜加凭据自动携带，统一引入不可预测Token并先修XSS | CSRF归因请求伪造，Token防御落地 |
| Web应用防御 | `whitehat-data-code-separation`<br>[数据与代码分离原则](../../../skills/webapp-defense/whitehat-data-code-separation/SKILL.md) | 一切注入=用户数据被解释器当代码，防御靠参数化/编码等结构分离而非黑名单 | 注入类漏洞统一成因模型与分离防御 |
| Web应用防御 | `whitehat-defense-at-interpretation`<br>[解释发生处设防](../../../skills/webapp-defense/whitehat-defense-at-interpretation/SKILL.md) | 语境在哪环可确定防线就在哪环：存原始按消费点编码，入口过滤两头失败 | 注入防御防线位置裁决方法 |
| Web应用防御 | `whitehat-parser-consistency-audit`<br>[解析器一致性审计](../../../skills/webapp-defense/whitehat-parser-consistency-audit/SKILL.md) | 同一数据过两个解释器口径必不一致，画全解析环节逐对核对防校验绕过 | 双端解析差异致注入绕过的审计 |
| 代码审计 | `caudit-admin-webshell-parity`<br>[后台高危功能Webshell等价管控](../../../skills/code-audit/caudit-admin-webshell-parity/SKILL.md) | 把后台文件管理、在线SQL、命令执行、备份翻译成webshell能力清单并按等价强度管控 | 后台高危功能等价webshell执行面 |
| 渗透测试方法论 | `wahh-blind-exploitation-ladder`<br>[盲利用阶梯](../../../skills/pentest-methodology/wahh-blind-exploitation-ladder/SKILL.md) | 无回显时按条件响应→时间延迟→带外通道逐级构造取数信道 | 注入确认后的盲取数技术 |
| 渗透测试方法论 | `wahh-boundary-validation-model`<br>[边界确认模型](../../../skills/pentest-methodology/wahh-boundary-validation-model/SKILL.md) | 每组件按下一跳解释器重新确认输入，入口单点确认必失效 | 输入校验部署位置原则 |
| 渗透测试方法论 | `wahh-csrf-assessment`<br>[CSRF判定与令牌评估](../../../skills/pentest-methodology/wahh-csrf-assessment/SKILL.md) | 三特征判可攻击性，令牌五问审实现，Referer是坏防御 | CSRF可攻击性判定 |
| 渗透测试方法论 | `wahh-filesystem-attack-surface`<br>[文件系统攻击面测试](../../../skills/pentest-methodology/wahh-filesystem-attack-surface/SKILL.md) | 遍历探测加标记串定位，读写两路目标清单，LFI借受控文件升级 | 路径遍历与文件包含攻击面 |
| 渗透测试方法论 | `wahh-filter-bypass-model`<br>[过滤器绕过模型](../../../skills/pentest-methodology/wahh-filter-bypass-model/SKILL.md) | 分别建模过滤器与后端解析规则集，差异点即绕过面四类向量 | 输入过滤的对抗性绕过方法 |
| 渗透测试方法论 | `wahh-injection-unified-model`<br>[注入统一模型](../../../skills/pentest-methodology/wahh-injection-unified-model/SKILL.md) | SQL/NoSQL/XPath/命令统一为输入被解析为指令，确认阶梯取证 | 跨解释器注入确认总模型 |
| 渗透测试方法论 | `wahh-input-handling-spectrum`<br>[输入处理五法谱系](../../../skills/pentest-methodology/wahh-input-handling-spectrum/SKILL.md) | 黑名单→白名单→净化→安全处理→语法检查的选择判据 | 输入校验防御方法选型 |
| 渗透测试方法论 | `wahh-native-code-blackbox-probe`<br>[本地代码黑盒探测](../../../skills/pentest-methodology/wahh-native-code-blackbox-probe/SKILL.md) | 约整长度阶梯加边界值表，一次一参数，反常信号甄别崩溃 | 原生组件内存破坏黑盒探查 |
| 渗透测试方法论 | `wahh-parameterization-discipline`<br>[参数化纪律](../../../skills/pentest-methodology/wahh-parameterization-discipline/SKILL.md) | 统一判据=值以数据形式绑定，全量全字段覆盖防残留拼接 | 注入防御判定与覆盖审计 |
| 渗透测试方法论 | `wahh-stored-dom-xss-mapping`<br>[存储型与DOM型XSS定位](../../../skills/pentest-methodology/wahh-stored-dom-xss-mapping/SKILL.md) | 提交特殊串遍历全部显示点，DOM用source→sink污点追踪 | 存储/DOM型XSS定位方法 |
| 渗透测试方法论 | `wahh-xss-detection-bypass`<br>[XSS系统化探测与绕过](../../../skills/pentest-methodology/wahh-xss-detection-bypass/SKILL.md) | 良性串定位全部反射，判语法上下文构造逃逸，过滤三分诊 | 反射型XSS探测与上下文逃逸 |
| 渗透测试方法论 | `wahh-xss-impact-defense-baseline`<br>[XSS影响评估与防御基线](../../../skills/pentest-methodology/wahh-xss-impact-defense-baseline/SKILL.md) | 借域信誉执行代码，载荷五类分类学，输出编码防御三重 | XSS定级与输出编码基线 |
| 密码工程 | `stallings-canonicalization-first`<br>[规范化先行与松紧权衡](../../../skills/crypto-engineering/stallings-canonicalization-first/SKILL.md) | 对被改写对象签名/比较前先定规范化，等价类过宽即调包面 | 规范化归一属输入验证范畴 |

**来源分布**：Web应用防御×5、代码审计×1、渗透测试方法论×12、密码工程×1
