# 2.1-身份认证与会话管理 —— 技能说明

## 本子域审计范围

默认口令、弱口令策略、MFA、验证码、会话固定、Cookie 属性（HttpOnly/Secure/SameSite）、令牌有效期、登出失效、密码找回流程、暴力破解防护。

## 技能清单（22 个）

| 集合 | 技能 | 一句话说明 | 归类理由 |
|---|---|---|---|
| Web应用防御 | `whitehat-credential-rotation-on-state-change`<br>[凭证轮换与作废纪律](../../../skills/webapp-defense/whitehat-credential-rotation-on-state-change/SKILL.md) | 状态质变必轮换会话标识，一次性凭据消费即原子作废，防固定与重放 | 会话与令牌生命周期管理纪律 |
| 代码审计 | `caudit-captcha-failure-premises`<br>[验证码失效四前提与硬规则](../../../skills/code-audit/caudit-captcha-failure-premises/SKILL.md) | 验证码有效拆为一次性、限次、机器识别、代答经济四前提，任一不满足即验收不过 | 验证码四前提检验，防凭证爆破 |
| 代码审计 | `caudit-password-reset-three-stages`<br>[找回密码三阶段防线](../../../skills/code-audit/caudit-password-reset-three-stages/SKILL.md) | 发码、校验、执行三阶段分别核地址来源、凭证四性、执行复验，防账号接管 | 凭证重发流程三阶段缺陷谱 |
| 代码审计 | `caudit-rate-limit-dual-edge`<br>[限频多维组合与滥用面](../../../skills/code-audit/caudit-rate-limit-dual-edge/SKILL.md) | 每维限频推演绕过端与滥用端（锁号DoS、误杀），输出多维组合加分级响应 | 限频策略绕过与滥用两端推演 |
| 渗透测试方法论 | `wahh-authentication-audit-panorama`<br>[验证机制全景审查](../../../skills/pentest-methodology/wahh-authentication-audit-panorama/SKILL.md) | 登录/注册/改密/找回逐个过13类缺陷清单，凭据全路径三查 | 认证全流程缺陷审查 |
| 渗透测试方法论 | `wahh-brute-force-engineering`<br>[认证蛮力工程学](../../../skills/pentest-methodology/wahh-brute-force-engineering/SKILL.md) | 锁定模型四分类配绕过，广度优先猜密，字典按实测规则收缩 | 凭据猜测攻击的运筹方法 |
| 渗透测试方法论 | `wahh-multistage-state-machine-attack`<br>[多阶段状态机攻击](../../../skills/pentest-methodology/wahh-multistage-state-machine-attack/SKILL.md) | 孤立重放各阶段请求，定位无需前序即可触发的处理逻辑 | 多阶段流程状态机攻击 |
| 渗透测试方法论 | `wahh-session-token-generation-analysis`<br>[会话令牌生成侧分析](../../../skills/pentest-methodology/wahh-session-token-generation-analysis/SKILL.md) | 采样差分与统计检验估有效熵，假想最弱熵源失效试验 | 令牌生成熵与可预测性审计 |
| 渗透测试方法论 | `wahh-session-token-lifecycle-audit`<br>[会话令牌生命周期审查](../../../skills/pentest-methodology/wahh-session-token-lifecycle-audit/SKILL.md) | 传输/日志/终止/固定/Cookie范围全链路，服务端废弃才失效 | 令牌处理侧生命周期审计 |
| 密码学基础 | `stinson-authenticated-key-establishment`<br>[密钥建立认证绑定审计](../../../skills/crypto-foundations/stinson-authenticated-key-establishment/SKILL.md) | 裸DH必遭中间人，签名须盖身份与瞬时值并验持有 | 认证密钥建立协议审计 |
| 密码学基础 | `stinson-cross-session-reflection-defense`<br>[跨会话反射攻击防御](../../../skills/crypto-foundations/stinson-cross-session-reflection-defense/SKILL.md) | 并行会话搬运认证值，唯一解法是消息流域分离 | 协议认证域分离纪律 |
| 密码学基础 | `stinson-freshness-replay-decision-tree`<br>[新鲜性与重放决策树](../../../skills/crypto-foundations/stinson-freshness-replay-decision-tree/SKILL.md) | 时间戳/随机挑战/幂等键三路线，新鲜值须进签名覆盖 | 重放防护三路线抉择 |
| 密码学基础 | `stinson-low-entropy-password-offline-audit`<br>[低熵口令离线验证审计](../../../skills/crypto-foundations/stinson-low-entropy-password-offline-audit/SKILL.md) | 关键在验证面位置：可离线试解的构造必败须移在线 | 口令认证离线暴破面审计 |
| 密码工程 | `stallings-anti-replay-window-engineering`<br>[防重放机制选型与窗口工程](../../../skills/crypto-engineering/stallings-anti-replay-window-engineering/SKILL.md) | 重放分四型，按信道形态选质询/时间戳/序号窗口机制 | 防重放属会话新鲜性管理 |
| 密码工程 | `stallings-auth-assurance-tiering`<br>[认证对象分解与保障分档](../../../skills/crypto-engineering/stallings-auth-assurance-tiering/SKILL.md) | 验物还是验人、因子按失效定价、风险定 step-up 档位 | 认证机制分档属身份认证 |
| 密码工程 | `stallings-auth-mechanism-axes`<br>[认证机制选型四轴](../../../skills/crypto-engineering/stallings-auth-mechanism-axes/SKILL.md) | 覆盖率/范围/摩擦/追责四轴比选域级与个人级机制 | 认证机制比选属身份认证 |
| 密码工程 | `stallings-challenge-response-design-criteria`<br>[挑战-应答设计判据](../../../skills/crypto-engineering/stallings-challenge-response-design-criteria/SKILL.md) | 应答须为持钥者变换，权威三件套防反射重放与错配 | 挑战应答判据属认证机制 |
| 密码工程 | `stallings-credential-splitting`<br>[凭据拆分与协商摊销](../../../skills/crypto-engineering/stallings-credential-splitting/SKILL.md) | 载体凭据管分发摊销+一次性证明管身份绑定，各配寿命 | 凭据拆分属会话凭据管理 |
| 密码工程 | `stallings-evidence-alignment-binding`<br>[证据绑定与对齐聚合](../../../skills/crypto-engineering/stallings-evidence-alignment-binding/SKILL.md) | 多层验证须对齐核心身份，签名三方绑定防剥离搬运重签 | 认证证据对齐属身份认证 |
| 密码工程 | `stallings-evidence-asymmetry-non-repudiation`<br>[证据不对称与不可否认](../../../skills/crypto-engineering/stallings-evidence-asymmetry-non-repudiation/SKILL.md) | MAC 双方对等不能举证，签名可仲裁，按仲裁场景选机制 | 不可否认判定属认证选型 |
| 密码工程 | `stallings-protocol-belief-analysis`<br>[协议信念分析三步法](../../../skills/crypto-engineering/stallings-protocol-belief-analysis/SKILL.md) | 写信念断言逐条找反例再审新假设，审协议时序逻辑 | 认证协议审计属会话管理 |
| 密码工程 | `stallings-two-phase-gated-access`<br>[两阶段开门与控制面先行](../../../skills/crypto-engineering/stallings-two-phase-gated-access/SKILL.md) | 身份认证与密钥就绪拆两道门，消除已认证明文窗口 | 两阶段门控属认证会话管理 |

**来源分布**：Web应用防御×1、代码审计×3、渗透测试方法论×5、密码学基础×4、密码工程×9
