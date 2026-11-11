# 08-安全基线与渗透验证 · 安全基线与渗透验证 —— 技能说明

## 本目录审计范围

审计范围：自动化扫描 + 人工渗透验证；漏洞复测；风险评级（高危/中危/低危/信息提示）与整改方案。

## 技能清单（42 个）

| 集合 | 技能 | 一句话说明 | 归类理由 |
|---|---|---|---|
| Web应用防御 | `whitehat-continuous-security-verification`<br>[持续安全验证](../../skills/webapp-defense/whitehat-continuous-security-verification/SKILL.md) | 把制度/设备/零事故当待验假设，用Find-Fix循环加监控持续验证安全态 | 周期检查与复测式验证方法论 |
| Web应用防御 | `whitehat-mitigation-vs-fix`<br>[缓解与修复分级](../../skills/webapp-defense/whitehat-mitigation-vs-fix/SKILL.md) | 治根因还是治后果：HttpOnly/WAF/验证码皆减损控件，不算修复结案 | 整改措施定级与验收方法论 |
| Web应用防御 | `whitehat-root-cause-patch-discipline`<br>[根因修复纪律](../../skills/webapp-defense/whitehat-root-cause-patch-discipline/SKILL.md) | 补丁针对成因而非POC特征，按payload修必被变体绕过，补丁本身须过审 | 修复验收与复测的整改方法论 |
| Web应用防御 | `whitehat-security-assessment`<br>[四阶段安全评估](../../skills/webapp-defense/whitehat-security-assessment/SKILL.md) | 资产分级→威胁分析→风险分析→方案设计顺序推进，先定保护对象再排序 | 完整评估流程与风险排序框架 |
| Web应用防御 | `whitehat-tool-vs-manual-boundary`<br>[工具人工分工边界](../../skills/webapp-defense/whitehat-tool-vs-manual-boundary/SKILL.md) | 可模式化漏洞交扫描器，业务逻辑类必须人工，零告警可能是盲区非安全 | 扫描与人工渗透的分工方法论 |
| 渗透测试方法论 | `wahh-13-area-pentest-framework`<br>[13区域渗透测试总框架](../../skills/pentest-methodology/wahh-13-area-pentest-framework/SKILL.md) | 按逻辑依赖排序的13区域清单，防疏忽、依赖回溯防漏测 | 渗透测试组织与覆盖总纲 |
| 渗透测试方法论 | `wahh-attack-plan-prioritization`<br>[攻击计划优先级排序](../../skills/pentest-methodology/wahh-attack-plan-prioritization/SKILL.md) | 按功能有用度×漏洞严重度双变量排序，决定各区域时间预算 | 受攻击面翻译成攻击计划 |
| 渗透测试方法论 | `wahh-consistency-anomaly-targeting`<br>[全站一致性异常定位](../../skills/pentest-methodology/wahh-consistency-anomaly-targeting/SKILL.md) | 以点推面解码全站机制，风格不一致的拼接区是优先靶区 | 优先攻击目标的选择信号 |
| 渗透测试方法论 | `wahh-core-defense-weakest-link`<br>[核心防御与最弱环节](../../skills/pentest-methodology/wahh-core-defense-weakest-link/SKILL.md) | 防御归四格三层串联，总体安全按最弱环节定级与修复排序 | 整体安全基线定级框架 |
| 渗透测试方法论 | `wahh-custom-attack-automation`<br>[定制攻击自动化](../../skills/pentest-methodology/wahh-custom-attack-automation/SKILL.md) | 请求/响应对加触点六指标，会话处理解耦攻击语义防静默失效 | 批量攻击执行的自动化纪律 |
| 渗透测试方法论 | `wahh-experimental-testing-discipline`<br>[渗透测试实验纪律](../../skills/pentest-methodology/wahh-experimental-testing-discipline/SKILL.md) | 良性对照、新会话复现、重复请求、以代理字节为准四件套判真伪 | 单条发现的证实证伪纪律 |
| 渗透测试方法论 | `wahh-scanner-limits-discipline`<br>[扫描器能力边界纪律](../../skills/pentest-methodology/wahh-scanner-limits-discipline/SKILL.md) | 可靠探测边界=有签名漏洞，四大内在限制定人机分工比例 | 扫描器工具边界与使用纪律 |
| 体系审核验证 | `isms-control-test-admission`<br>[控制测试准入与选档](../../skills/system-audit-verification/isms-control-test-admission/SKILL.md) | 主动测试前五条准入约束，按信息对称度选串联、灰盒或盲测档位 | 渗透演练准入授权与选档纪律 |
| 体系审核验证 | `isms-recovery-time-verification`<br>[恢复时效实测](../../skills/system-audit-verification/isms-recovery-time-verification/SKILL.md) | 把有无备份升级为实测恢复耗时对照RPO与RTO，缺演练即未验证 | 备份灾备恢复时效技术验证 |
| 体系审核验证 | `isms-test-event-method`<br>[测试事件法](../../skills/system-audit-verification/isms-test-event-method/SKILL.md) | 受控触发一次事件沿路径核对记录与响应，验会不会记而非曾记录 | 受控事件动态验证记录响应 |
| 合规测评 | `mlps-active-verification-perturbation`<br>[主动验证法（可控扰动与否定式验证）](../../skills/compliance-assessment/mlps-active-verification-perturbation/SKILL.md) | 设计可控扰动以否定式结果证明防护生效的主动验证法 | 测评验证作业方法 |
| 合规测评 | `mlps-artifact-verification-record-quality`<br>[产物核验与记录实质性质检](../../skills/compliance-assessment/mlps-artifact-verification-record-quality/SKILL.md) | 两步核验过程产物实物并按四要素质检记录证明力 | 过程产物证据判定 |
| 合规测评 | `mlps-assessment-redlines`<br>[测评作业红线与现场纪律](../../skills/compliance-assessment/mlps-assessment-redlines/SKILL.md) | 授权限域限速陪同清零等渗透前红线与现场纪律清单 | 测评作业红线纪律 |
| 合规测评 | `mlps-assessment-scope-selection`<br>[测评对象确定法](../../skills/compliance-assessment/mlps-assessment-scope-selection/SKILL.md) | 架构调研先行，按资产赋值从九类对象裁剪测评范围 | 测评对象确定属测评作业 |
| 合规测评 | `mlps-audit-six-dimension-assessment`<br>[安全审计六维测评框架](../../skills/compliance-assessment/mlps-audit-six-dimension-assessment/SKILL.md) | 按范围内容分析防篡改进程保护防覆盖六维评审计能力 | 审计能力测评框架 |
| 合规测评 | `mlps-control-effectiveness-four-checks`<br>[控制有效性四查](../../skills/compliance-assessment/mlps-control-effectiveness-four-checks/SKILL.md) | 粒度覆盖生效技术强制四查，区分配置存在与控制生效 | 控制有效性核查方法 |
| 合规测评 | `mlps-indicator-selection-rules`<br>[测评指标确定规则集](../../skills/compliance-assessment/mlps-indicator-selection-rules/SKILL.md) | 按S/A等级选指标，共用资源就高，先适用性后符合性 | 指标确定属测评作业 |
| 合规测评 | `mlps-intrusive-test-downgrade`<br>[验证测试的降级权衡与豁免程序](../../skills/compliance-assessment/mlps-intrusive-test-downgrade/SKILL.md) | 高侵入测试先降级替代再豁免签章，报告写明未验范围 | 测试降级豁免程序 |
| 合规测评 | `mlps-level-diff-model`<br>[逐级增强三层次diff模型](../../skills/compliance-assessment/mlps-level-diff-model/SKILL.md) | 级差拆为控制点、要求项增加与强度增强三层可计数差异 | 标准级差分析方法 |
| 合规测评 | `mlps-method-role-allocation`<br>[访谈/检查/测试三法角色组合策略](../../skills/compliance-assessment/mlps-method-role-allocation/SKILL.md) | 检查为基本证据、测试为验证、访谈辅助，管理域禁用工具 | 三法角色组合方法论 |
| 合规测评 | `mlps-native-capability-gap-chain`<br>[原生能力缺口判定链](../../skills/compliance-assessment/mlps-native-capability-gap-chain/SKILL.md) | 指标超产品默认能力时按缺口、补偿、否则不符合三步判定 | 能力缺口判定链 |
| 合规测评 | `mlps-preponderant-evidence`<br>[证据优势法（强证据压倒弱证据）](../../skills/compliance-assessment/mlps-preponderant-evidence/SKILL.md) | 按测试、检查、访谈可靠性分级，强证据压倒弱证据 | 证据优势裁决法 |
| 合规测评 | `mlps-reference-value-fallback`<br>[标准留白参考值兜底法](../../skills/compliance-assessment/mlps-reference-value-fallback/SKILL.md) | 标准留白时自建参考值表兜底并声明其经验值性质 | 测评判定依据兜底 |
| 合规测评 | `mlps-report-validity-retest`<br>[测评结论时效边界与变更重测](../../skills/compliance-assessment/mlps-report-validity-retest/SKILL.md) | 结论仅对测评时点有效，组件变更或周期到即触发重测 | 报告时效与重测触发 |
| 合规测评 | `mlps-risk-assessment-six-steps`<br>[风险评估六步法与测评耦合](../../skills/compliance-assessment/mlps-risk-assessment-six-steps/SKILL.md) | 资产赋值、重要性阈值、威胁脆弱性到风险排序六步流程 | 六步风险分析方法 |
| 合规测评 | `mlps-score-aggregation-chain`<br>[可复算得分聚合链](../../skills/compliance-assessment/mlps-score-aggregation-chain/SKILL.md) | 0-5赋值、加权、修正到结论档位，全链可复算追分 | 得分聚合复算方法 |
| 合规测评 | `mlps-standard-six-relation-mapping`<br>[跨标准六关系差异映射法](../../skills/compliance-assessment/mlps-standard-six-relation-mapping/SKILL.md) | 跨标准条款差异收敛为六种关系并配映射矩阵可查询 | 标准差异映射方法 |
| 合规测评 | `mlps-test-vantage-point-placement`<br>[工具接入点布点法](../../skills/compliance-assessment/mlps-test-vantage-point-placement/SKILL.md) | 沿信任梯度五原则布接入点，隔离设备两侧分段探测 | 工具接入点布点 |
| 合规测评 | `mlps-tool-test-typology`<br>[工具测试类型学与证据形态匹配](../../skills/compliance-assessment/mlps-tool-test-typology/SKILL.md) | 扫描发现、监测观测、渗透验证三类证据形态不可互换 | 工具类型与证据匹配 |
| 合规测评 | `mlps-triple-consistency-check`<br>[三重一致性核查与形式合规穿透](../../skills/compliance-assessment/mlps-triple-consistency-check/SKILL.md) | 文档、实地、记录三重互证，任一断裂即降档穿透纸面合规 | 三重一致性核查 |
| 合规测评 | `mlps-verdict-chain-revision`<br>[判定链与整体测评回改机制](../../skills/compliance-assessment/mlps-verdict-chain-revision/SKILL.md) | 单项到结论判定链固定，整体测评回改是唯一修正通道 | 判定链与回改机制 |
| 合规测评 | `mlps-verdict-tiers`<br>[判定档位体系](../../skills/compliance-assessment/mlps-verdict-tiers/SKILL.md) | 符合、部分符合、不适用、进一步跟踪等档位各有触发纪律 | 判定档位体系 |
| 密码工程 | `stallings-attack-capability-success-levels`<br>[攻击能力×成功等级双轴声明](../../skills/crypto-engineering/stallings-attack-capability-success-levels/SKILL.md) | 不可伪造声明须拆解攻击者能力档×危害档，厂商宣称常是最低档 | 攻击能力分级用于验证声明 |
| 密码工程 | `stallings-confusion-diffusion-suite`<br>[混淆-扩散检验套件](../../skills/crypto-engineering/stallings-confusion-diffusion-suite/SKILL.md) | 影响矩阵/雪崩/SAC/非线性/密钥包裹五类自动化检测自研函数 | 自研密码自动化检测属验证 |
| 密码工程 | `stallings-crypto-operation-ordering`<br>[密码操作次序纪律](../../skills/crypto-engineering/stallings-crypto-operation-ordering/SKILL.md) | 签名加密压缩MAC次序定可见性与可仲裁性，覆盖域防降级重放 | 密码操作排序属验证审查 |
| 密码工程 | `stallings-keyless-mutation-test`<br>[无钥变形测试清单](../../skills/crypto-engineering/stallings-keyless-mutation-test/SKILL.md) | 重排/截断/拼接/定向翻转/解方程五类变形，校验过即证伪 | 无钥变形测试属验证方法 |
| 密码工程 | `stallings-linearity-solvability-test`<br>[线性可解性快判](../../skills/crypto-engineering/stallings-linearity-solvability-test/SKILL.md) | 线性变换即解方程组，已知明文下密钥直接可解，一票否决 | 自研加密线性快判属测试 |

**来源分布**：Web应用防御×5、渗透测试方法论×7、体系审核验证×3、合规测评×22、密码工程×5

## 覆盖缺口

覆盖较好：渗透方法论与等保测评方法双体系。缺口提示：自动化扫描器选型与 CVSS 定级暂无专门技能。
