# 04-服务器与基础设施 · 服务器与基础设施层 —— 技能说明

## 本目录审计范围

审计范围：操作系统账号、端口开放、防火墙、云安全组、SSH、数据库权限、备份策略、定时任务、容器/云主机配置、日志权限、是否存在 webshell/后门/恶意文件。

## 技能清单（11 个）

| 集合 | 技能 | 一句话说明 | 归类理由 |
|---|---|---|---|
| Web应用防御 | `whitehat-attack-chain-pruning`<br>[攻击链裁剪配权](../../skills/webapp-defense/whitehat-attack-chain-pruning/SKILL.md) | 先画攻击者升级路径再逐跳砍权限，数据库/进程/容器配权由攻击链推导 | 面向数据库/容器/进程的基础设施配权 |
| 渗透测试方法论 | `wahh-layered-trust-attack-paths`<br>[分层信任攻击路径](../../skills/pentest-methodology/wahh-layered-trust-attack-paths/SKILL.md) | 枚举谁完全信任谁，单点漏洞经信任放大扩张影响半径 | 应用内部层间基础设施信任 |
| 体系审核验证 | `isms-network-service-three-line-audit`<br>[网络服务三线审核](../../skills/system-audit-verification/isms-network-service-three-line-audit/SKILL.md) | 合同、配置、日志三线互证外包服务，防声明加密实为HTTP回源 | 外包网络服务基础设施核验 |
| 体系审核验证 | `isms-privilege-audit-chain`<br>[特权权限审核链](../../skills/system-audit-verification/isms-privilege-audit-chain/SKILL.md) | 定义、平台核查、使用日志三步取证，专查提权盲区与分权判据 | 特权账号核验，依托审计链 |
| 体系审核验证 | `isms-three-layer-evidence-chain`<br>[三层取证链](../../skills/system-audit-verification/isms-three-layer-evidence-chain/SKILL.md) | 文档、配置、运行记录三层逐层取证互证，抓配置有日志无断链 | 控制落地核验的通用骨架 |
| 合规测评 | `mlps-backup-recoverability-verification`<br>[备份恢复的可恢复性验证](../../skills/compliance-assessment/mlps-backup-recoverability-verification/SKILL.md) | 有备份不等于可恢复，按四层核查并强制恢复演练证据 | 备份恢复对象为系统数据 |
| 合规测评 | `mlps-reconciliation-style-checking`<br>[对账式核查法](../../skills/compliance-assessment/mlps-reconciliation-style-checking/SKILL.md) | 以系统外基准与不可变主键对账查共享、幽灵、默认账户 | 系统账号端口最小化核查 |
| 密码工程 | `stallings-cheap-check-first`<br>[廉价验证前置排序](../../skills/crypto-engineering/stallings-cheap-check-first/SKILL.md) | 带密钥的廉价校验排在昂贵运算前，cookie 先证可达再放行 | 抗握手洪泛属服务器可用性防护 |
| 密码工程 | `stallings-control-anchor-forgeability`<br>[管控落点与锚点可伪造性](../../skills/crypto-engineering/stallings-control-anchor-forgeability/SKILL.md) | 检查点问依赖标识可否伪造，锚点选早可得难伪造字段 | 准入与网络层落点属基础设施 |
| 密码工程 | `stallings-environment-threat-rewrite`<br>[环境迁移的威胁模型重推](../../skills/crypto-engineering/stallings-environment-threat-rewrite/SKILL.md) | 盘点旧环境免费保障，丢失项即新攻击面，三列闭环补回 | 环境威胁改写归基础设施 |
| 密码工程 | `stallings-security-layer-placement`<br>[协议栈层次与覆盖段选型](../../skills/crypto-engineering/stallings-security-layer-placement/SKILL.md) | 按覆盖杠杆/透明性/语义粒度选层，分段保护≠端到端 | IPsec/TLS层级落点属基础设施 |

**来源分布**：Web应用防御×1、渗透测试方法论×1、体系审核验证×3、合规测评×2、密码工程×4

## 覆盖缺口

缺口提示：容器/云主机配置核查、恶意文件排查暂无专门技能，建议结合 CIS 基线工具；现有技能偏基础设施的取证与验证方法论。
