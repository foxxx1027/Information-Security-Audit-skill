# 01-资产边界 · 资产边界与攻击面测绘 —— 技能说明

## 本目录审计范围

审计范围：域名、子域名、Web前端、后台管理、API接口（REST/GraphQL）、文件上传服务、第三方嵌入组件、服务器、中间件、数据库、缓存、CDN、WAF 的识别与边界划定；信任域/信任边界建模；攻击面枚举。明确排除：不受控第三方 SaaS、外部服务商黑盒系统。

## 技能清单（8 个）

| 集合 | 技能 | 一句话说明 | 归类理由 |
|---|---|---|---|
| Web应用防御 | `whitehat-attack-surface-reduction`<br>[攻击面收敛减面](../../skills/webapp-defense/whitehat-attack-surface-reduction/SKILL.md) | 按删除>禁用>加固次序收敛暴露面，管理台/调试接口/多余组件皆为待删项 | 攻击面识别与收敛，属资产边界管理 |
| Web应用防御 | `whitehat-cross-context-channel-enumeration`<br>[跨上下文通道枚举](../../skills/webapp-defense/whitehat-cross-context-channel-enumeration/SKILL.md) | SOP外还有拖拽/postMessage/CORS等侧门，逐通道核验接收端校验 | 枚举跨信任域通道，浏览器攻击面识别 |
| Web应用防御 | `whitehat-trust-boundary`<br>[信任域与边界划分](../../skills/webapp-defense/whitehat-trust-boundary/SKILL.md) | 低信任流向高信任必过边界检查，高流向低免检，检查位置跟数据流向走 | 信任边界建模归资产边界类 |
| 渗透测试方法论 | `wahh-function-path-enumeration`<br>[功能路径枚举](../../skills/pentest-methodology/wahh-function-path-enumeration/SKILL.md) | 参数即功能：枚举方法名映射隐藏API，低权直调测暴露面 | 隐藏功能面枚举测绘 |
| 渗透测试方法论 | `wahh-hidden-content-enumeration`<br>[隐藏内容枚举](../../skills/pentest-methodology/wahh-hidden-content-enumeration/SKILL.md) | 建不存在基线按差异判读，命名归纳构造词典迭代回灌 | 隐藏内容与端点发现 |
| 渗透测试方法论 | `wahh-tech-stack-fingerprinting`<br>[技术栈指纹方法论](../../skills/pentest-methodology/wahh-tech-stack-fingerprinting/SKILL.md) | 声明旗标→规范行为→语法差异三层信号，越靠行为越可信 | 纯信息收集的技术归因 |
| 渗透测试方法论 | `wahh-thick-client-dual-route`<br>[厚客户端双路线测试](../../skills/pentest-methodology/wahh-thick-client-dual-route/SKILL.md) | 拦流量（hosts+自签CA）或反编译，四类目标提取隐藏功能 | 客户端侧攻击面获取与测绘 |
| 密码工程 | `stallings-attack-surface-shrink-then-layer`<br>[攻击面双杠杆：先收缩再分层](../../skills/crypto-engineering/stallings-attack-surface-shrink-then-layer/SKILL.md) | 测绘网络/软件/人三栏暴露面先收缩，残余面再分层，两账分记 | 攻击面测绘即资产边界梳理 |

**来源分布**：Web应用防御×3、渗透测试方法论×4、密码工程×1

## 覆盖缺口

缺口提示：子域名接管、CDN/WAF 配置核查、API 清单自动化盘点暂无专门技能，建议结合外部资产测绘工具使用。
