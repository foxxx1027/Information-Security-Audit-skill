# 09-通用安全方法论 · 通用安全方法论（跨领域支撑） —— 技能说明

## 本目录审计范围

补充类：不隶属单一审计域、可迁移到以上所有类别的安全思维模型与方法论（如信任假设检验、纵深防御、敌手建模、可证明安全观、证据纪律等）。

## 技能清单（32 个）

| 集合 | 技能 | 一句话说明 | 归类理由 |
|---|---|---|---|
| Web应用防御 | `whitehat-coverage-first`<br>[覆盖率优先原则](../../skills/webapp-defense/whitehat-coverage-first/SKILL.md) | 白帽漏一即败：先全覆盖拿未覆盖清单再深挖，未发现须与未覆盖并列呈报 | 攻防不对称导出的求全排序思维 |
| Web应用防御 | `whitehat-decompose-by-attack-class`<br>[按攻击类别分解防御](../../skills/webapp-defense/whitehat-decompose-by-attack-class/SKILL.md) | 把告警风险归因到攻击类别逐类设计方案，以类别为工作单元化被动为主动 | 安全工作组织层面的分解思维模型 |
| Web应用防御 | `whitehat-defense-in-depth`<br>[纵深防御体系](../../skills/webapp-defense/whitehat-defense-in-depth/SKILL.md) | 多层设防各层在正确位置解决本层根因，勿把多目标压在单一机制上 | 跨层防御总体思维模型 |
| Web应用防御 | `whitehat-security-as-product-feature`<br>[安全作为产品特性](../../skills/webapp-defense/whitehat-security-as-product-feature/SKILL.md) | 没有不安全的业务只有不安全的实现：保护业务目标，改造实现方式两全 | 安全业务冲突裁决的思维模型 |
| Web应用防御 | `whitehat-security-interaction-design`<br>[安全交互设计](../../skills/webapp-defense/whitehat-security-interaction-design/SKILL.md) | 提示是稀缺资源：仅用户可行动且风险具体时出现，能服务端裁决的不问用户 | 面向用户的提示设计跨域纪律 |
| Web应用防御 | `whitehat-signal-reliability`<br>[信号可靠性分级](../../skills/webapp-defense/whitehat-signal-reliability/SKILL.md) | 能取到值不等于能当安全边界：按可伪造成本/可缺失性分级，裁决权在服务端 | 信号可信度的信任本质判断 |
| Web应用防御 | `whitehat-trust-assumption-audit`<br>[信任假设审计](../../skills/webapp-defense/whitehat-trust-assumption-audit/SKILL.md) | 列出机制隐含信任的前提逐条攻击验证，前提被打破则机制整体失效 | 信任本质检验的评审思维模型 |
| Web应用防御 | `whitehat-unpredictability`<br>[不可预测性原则](../../skills/webapp-defense/whitehat-unpredictability/SKILL.md) | 关键值可预测=可批量枚举预构造，随机化抬高攻击成本，含ASLR式缓解 | 不可猜设计与攻击成本思维模型 |
| Web应用防御 | `whitehat-whitelist-first`<br>[白名单优先原则](../../skills/webapp-defense/whitehat-whitelist-first/SKILL.md) | 白名单失败关闭黑名单失败开放，优先只允许已知安全项，通配符即退化 | 校验授权规则形态的通用思想 |
| 代码审计 | `caudit-attacker-first-function-design`<br>[攻击者视角功能安全设计总纲](../../skills/code-audit/caudit-attacker-first-function-design/SKILL.md) | 新功能先枚举攻击面推演利用方式，再按利用反推安全设计，顺序强制不可颠倒 | 攻击面到利用到对策的跨域门禁 |
| 渗透测试方法论 | `wahh-untrusted-input-dimensions`<br>[不可信输入公理](../../skills/pentest-methodology/wahh-untrusted-input-dimensions/SKILL.md) | 用户可提交任意输入，改值/乱序/增加/删除四维操纵面 | 跨领域不可信输入公理 |
| 密码学基础 | `stinson-adversary-capability-goal-matrix`<br>[敌手能力×目标双轴建模](../../skills/crypto-foundations/stinson-adversary-capability-goal-matrix/SKILL.md) | 把安全声明拆成敌手能力×攻击目标格子再评估 | 敌手建模跨领域通用思维 |
| 密码学基础 | `stinson-attack-feasibility-three-dimensions`<br>[攻击可行性三维评估](../../skills/crypto-foundations/stinson-attack-feasibility-three-dimensions/SKILL.md) | 算法复杂度×数据可得性×存储成本定级攻击现实威胁 | 攻击定级通用评估框架 |
| 密码学基础 | `stinson-composition-not-amplification`<br>[组合不自动增强](../../skills/crypto-foundations/stinson-composition-not-amplification/SKILL.md) | 双重加密默认零增益，须证非幂等与组件密钥独立 | 组合≠增强跨领域思维 |
| 密码学基础 | `stinson-evidence-tier-labeling`<br>[安全证据四级标注](../../skills/crypto-foundations/stinson-evidence-tier-labeling/SKILL.md) | 证明/ROM/启发式/未证假设分级，决策由最弱环节主导 | 证据层级选型决策方法论 |
| 密码学基础 | `stinson-feasibility-ceiling-first`<br>[可行性上界优先](../../skills/crypto-foundations/stinson-feasibility-ceiling-first/SKILL.md) | 先证信息论上界再构造顶界方案，不可能性先于选型 | 不可能性判定思维 |
| 密码学基础 | `stinson-oracle-surface-control`<br>[谕示面收敛控制](../../skills/crypto-foundations/stinson-oracle-surface-control/SKILL.md) | 每个能力接口都是攻击原语，须限型限格式默认关闭 | 接口谕示面通用收敛思维 |
| 密码学基础 | `stinson-perfect-secrecy-formalization`<br>[完美保密形式化判据](../../skills/crypto-foundations/stinson-perfect-secrecy-formalization/SKILL.md) | 后验=先验分布三查，核验OTP/QKD类绝对安全宣称 | 完美保密形式化思维 |
| 密码学基础 | `stinson-proof-coverage-audit`<br>[可证明安全覆盖域审计](../../skills/crypto-foundations/stinson-proof-coverage-audit/SKILL.md) | 证明只保护声明过的格子，拆敌手/量化/模型/构造四界 | 可证明安全观边界审计 |
| 密码学基础 | `stinson-provable-security-usability-cost`<br>[可证明方案可用性代价](../../skills/crypto-foundations/stinson-provable-security-usability-cost/SKILL.md) | 扩张率/解密歧义/吞吐决定混合加密是必然形态 | 安全可用性代价核算 |
| 密码学基础 | `stinson-pseudorandomness-criterion`<br>[伪随机性判据](../../skills/crypto-foundations/stinson-pseudorandomness-criterion/SKILL.md) | 统计全绿仅必要条件，验收看不可预测与种子链路 | 伪随机判据理论思维 |
| 密码学基础 | `stinson-reduction-comparison`<br>[归约比较性质强弱](../../skills/crypto-foundations/stinson-reduction-comparison/SKILL.md) | 性质蕴含须写出黑盒转译构造，不靠直觉排序 | 归约思想核心方法 |
| 密码学基础 | `stinson-security-notion-calibration`<br>[安全度量口径校准](../../skills/crypto-foundations/stinson-security-notion-calibration/SKILL.md) | 计算/可证明/无条件三把尺子不可混用，先声明再论证 | 安全定义口径方法论 |
| 密码学基础 | `stinson-simulatability-zero-knowledge`<br>[可模拟性零知识判据](../../skills/crypto-foundations/stinson-simulatability-zero-knowledge/SKILL.md) | 零泄漏证明靠模拟器生成同分布假本，失败处即泄漏 | 可模拟性理论判据 |
| 密码工程 | `stallings-analysis-cost-vs-brute-force`<br>[理想原语判据：分析代价≥穷举](../../skills/crypto-engineering/stallings-analysis-cost-vs-brute-force/SKILL.md) | 原语强度被最便宜攻击路径封顶，选型先查有无结构捷径 | 理想原语判据是跨域评估思维 |
| 密码工程 | `stallings-attack-service-mechanism-alignment`<br>[攻击—服务—机制三层对齐矩阵](../../skills/crypto-engineering/stallings-attack-service-mechanism-alignment/SKILL.md) | 资产定级后逐行核对攻击→服务→机制，交叉矩阵暴露覆盖缺口 | 攻击服务机制对齐属跨域方法论 |
| 密码工程 | `stallings-attack-tree-and-or-modeling`<br>[攻击树与/或建模](../../skills/crypto-engineering/stallings-attack-tree-and-or-modeling/SKILL.md) | 根为目的叶为手法，或节点找最便宜切断点排防御优先级 | 攻击树是威胁建模通用方法 |
| 密码工程 | `stallings-design-principles-review-protocol`<br>[安全设计准则清单化评审](../../skills/crypto-engineering/stallings-design-principles-review-protocol/SKILL.md) | 13 条准则逐条过，违反项登记补偿控制，检验同因失效伪纵深 | 设计准则评审是通用方法论 |
| 密码工程 | `stallings-hardness-dependency-audit`<br>[难题依赖审计与等效换算](../../skills/crypto-engineering/stallings-hardness-dependency-audit/SKILL.md) | 陷门/归约/同族三问，跨算法换算对称等效位数再比较 | 难题依赖是跨域评估思维 |
| 密码工程 | `stallings-passive-active-response-asymmetry`<br>[被动主动对策不对称](../../skills/crypto-engineering/stallings-passive-active-response-asymmetry/SKILL.md) | 被动难检测投预防，主动难防投检测恢复，据此分预算 | 对策重心不对称是通用思维 |
| 密码工程 | `stallings-security-solution-four-elements`<br>[安全方案四要素核对](../../skills/crypto-engineering/stallings-security-solution-four-elements/SKILL.md) | 算法/产生/分发/协议四栏完备性，任一薄弱整体即薄弱 | 四要素核对是通用方法论 |
| 密码工程 | `stallings-statistical-residual-order-analysis`<br>[统计残留的阶数分析](../../skills/crypto-engineering/stallings-statistical-residual-order-analysis/SKILL.md) | 密钥空间非指标，按保留几阶统计与所需样本量定档 | 自研构造强度定档判据 |

**来源分布**：Web应用防御×9、代码审计×1、渗透测试方法论×1、密码学基础×13、密码工程×8

## 覆盖缺口

本类为支撑层：调用时先查 01–08 专属技能，无匹配再回到本类思维模型。
