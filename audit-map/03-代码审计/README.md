# 03-代码审计 · 代码审计（SAST 源码审计） —— 技能说明

## 本目录审计范围

审计范围：源码、配置文件、脚本；污点传播分析、不安全函数、硬编码密钥、权限缺陷、加密实现缺陷；并与 DAST 动态扫描、IAST 交互式检测配合。

## 技能清单（17 个）

| 集合 | 技能 | 一句话说明 | 归类理由 |
|---|---|---|---|
| Web应用防御 | `whitehat-source-sink-audit`<br>[Source-Sink白盒审计](../../skills/webapp-defense/whitehat-source-sink-audit/SKILL.md) | 注入漏洞=可控输入×危险解释器，枚举source跟踪数据流抵达sink即漏洞面 | 污点传播源码级审计方法论 |
| 代码审计 | `caudit-api-relay-architecture`<br>[站库分离API中转与阈值监控](../../skills/code-audit/caudit-api-relay-architecture/SKILL.md) | 站库分离须API层收口加受限凭证，调用画像阈值兼作拖库入侵检测 | 数据访问收口架构与防拖库监控 |
| 代码审计 | `caudit-audit-path-selection`<br>[审计路径选型框架](../../skills/code-audit/caudit-audit-path-selection/SKILL.md) | 按时间预算、目标归属、漏洞类型在回溯、定向、通读四路径中选型并声明覆盖边界 | 四条审计路径的选型与放弃声明 |
| 代码审计 | `caudit-blacklist-failure-modes`<br>[黑名单失效模式与等价能力推演](../../skills/code-audit/caudit-blacklist-failure-modes/SKILL.md) | 黑名单从枚举不全、等价变体、改写重建、语义错位四向漏，等价能力推演定设计否定 | 黑名单四类失效的源码级推演 |
| 代码审计 | `caudit-choke-point-first`<br>[收口点优先审计策略](../../skills/code-audit/caudit-choke-point-first/SKILL.md) | 统一过滤或数据访问层读一处覆盖多数路径，无收口本身即最高风险信号 | 收口点决定审计切入与架构定性 |
| 代码审计 | `caudit-data-pollution-two-paths`<br>[数据污染两条路径模型](../../skills/code-audit/caudit-data-pollution-two-paths/SKILL.md) | 污染分被动接收与主动获取两路，入口与功能点两层过滤，改写点即新污染源 | 污染源两路径建模的源码级方法 |
| 代码审计 | `caudit-escape-as-last-step`<br>[转义必须是最后一步](../../skills/code-audit/caudit-escape-as-last-step/SKILL.md) | 转义后任何解码、转码、改写都使转义归零，审计动作是列变换清单判位置 | 转义时序判据：后有变换即失效 |
| 代码审计 | `caudit-filter-coverage-map`<br>[过滤覆盖面盲区测绘](../../skills/code-audit/caudit-filter-coverage-map/SKILL.md) | 按数据类别、入口、时机测绘统一过滤覆盖边界，空格即盲区并逐项验证 | 统一过滤覆盖边界的源码测绘 |
| 代码审计 | `caudit-mechanism-to-search-terms`<br>[机理驱动定向挖掘三步法](../../skills/code-audit/caudit-mechanism-to-search-terms/SKILL.md) | 先吃透漏洞机理再现场推导搜索词，搜到sink后回溯可控性与过滤充分性双问 | 机理推搜索词的定向挖掘三步法 |
| 代码审计 | `caudit-patch-diff-remediation`<br>[补丁diff入口与成因类修复](../../skills/code-audit/caudit-patch-diff-remediation/SKILL.md) | diff定位根因提炼漏洞模式全库同成因检索，修复须过等价表示字面性检查 | 补丁diff入口与同类漏洞收敛 |
| 代码审计 | `caudit-second-order-vuln`<br>[二次漏洞锚点追踪法](../../skills/code-audit/caudit-second-order-vuln/SKILL.md) | 写入与消费是独立控制点，按表名字段锚点追全部消费点逐个核对话境过滤 | 写入触发分离，取出即新输入 |
| 代码审计 | `caudit-structured-full-read`<br>[通读法结构化读法](../../skills/code-audit/caudit-structured-full-read/SKILL.md) | 按目录、入口、过滤文件、函数配置的角色排序通读，产出数据流图与过滤覆盖表 | 通读法的文件角色注意力排序 |
| 代码审计 | `caudit-trust-tier-isolation`<br>[信任级数据隔离结构优先](../../skills/code-audit/caudit-trust-tier-isolation/SKILL.md) | 一次编码疏忽即可越界的校验型边界应升级分表、写死域、行级安全等结构型隔离 | 信任级结构型隔离的数据架构 |
| 代码审计 | `caudit-type-context-defense`<br>[类型即边界语境防御选型](../../skills/code-audit/caudit-type-context-defense/SKILL.md) | 引号语境转义、裸数值类型锁定、标识符枚举映射，校验语义须与解析器一致 | 按注入语境选武器的源码级判据 |
| 代码审计 | `caudit-var-overwrite-chain`<br>[变量覆盖三点连线判定](../../skills/code-audit/caudit-var-overwrite-chain/SKILL.md) | 覆盖点、前文关键变量、后文消费三点连线才算漏洞，修复即斩断任一边 | 覆盖点前文后文三点连线判定 |
| 代码审计 | `caudit-whitelist-spectrum`<br>[白名单三形态谱系](../../skills/code-audit/caudit-whitelist-spectrum/SKILL.md) | 固定枚举、类型锁定、正则形态约束三形态选型，处置须命中即拦截不得替换为空 | 白名单三形态谱系与处置规则 |
| 渗透测试方法论 | `wahh-source-code-audit`<br>[源码审计三重查找法](../../skills/pentest-methodology/wahh-source-code-audit/SKILL.md) | 数据流追踪+签名搜索+逐行深审排程，锚点与注释补救漏报 | 白盒源码审计排程方法 |

**来源分布**：Web应用防御×1、代码审计×15、渗透测试方法论×1

## 覆盖缺口

缺口提示：IAST 插桩与 CI 集成流程暂无专门技能；现有技能以 PHP/Web 语境为主，跨语言迁移时按各 SKILL.md 的 B 段边界执行。
