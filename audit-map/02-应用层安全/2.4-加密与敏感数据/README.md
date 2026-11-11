# 2.4-加密与敏感数据 —— 技能说明

## 本子域审计范围

传输加密 TLS/SSL、证书、加密算法、敏感数据（手机号/身份证/密码）存储、明文日志泄露、前端本地存储敏感信息、密钥硬编码。

## 技能清单（36 个）

| 集合 | 技能 | 一句话说明 | 归类理由 |
|---|---|---|---|
| Web应用防御 | `whitehat-crypto-misuse-audit`<br>[密码学误用审计](../../../skills/webapp-defense/whitehat-crypto-misuse-audit/SKILL.md) | 加密安全=算法×模式×IV×认证×随机源×密钥管理乘法链，逐失败点查误用 | 密码学方案构造误用的审计清单 |
| 代码审计 | `caudit-security-metadata-pollution`<br>[安全元数据污染判别](../../../skills/code-audit/caudit-security-metadata-pollution/SKILL.md) | 白名单、开关、验证答案、金额真值、排序键等构造结构的参数不得出现在请求链上 | 安全元数据不得由请求携带裁决 |
| 渗透测试方法论 | `wahh-obfuscated-data-attack-ladder`<br>[模糊数据攻击四阶梯](../../../skills/pentest-methodology/wahh-obfuscated-data-attack-ladder/SKILL.md) | 逆向→换取→移植→畸形串递进，解不开的密文仍可利用 | 加密误用参数的攻击利用 |
| 合规测评 | `mlps-auth-transport-plaintext-veto`<br>[鉴别信息传输保护判据](../../../skills/compliance-assessment/mlps-auth-transport-plaintext-veto/SKILL.md) | 明文传口令一票否决；能力存在须显式配置与实测证明 | 鉴别信息传输加密判定 |
| 合规测评 | `mlps-data-transit-storage-grid`<br>[数据安全传输/存储两分检查格](../../../skills/compliance-assessment/mlps-data-transit-storage-grid/SKILL.md) | 传输存储乘完整性保密性四格防漏，检测恢复成对验收 | 数据传输存储保护防漏 |
| 密码学基础 | `stinson-birthday-bound-parameter-sizing`<br>[生日界参数反推](../../../skills/crypto-foundations/stinson-birthday-bound-parameter-sizing/SKILL.md) | n位空间仅给n/2位碰撞安全，按敌手查询量反推位长 | 摘要与ID位长参数选型 |
| 密码学基础 | `stinson-collusion-threshold-verification`<br>[合谋阈值双验证](../../../skills/crypto-foundations/stinson-collusion-threshold-verification/SKILL.md) | 门限须同验t份可恢复与t-1份零信息及份额独立性 | 门限密码方案验收框架 |
| 密码学基础 | `stinson-deterministic-pke-fails`<br>[确定性公钥加密必败](../../../skills/crypto-foundations/stinson-deterministic-pke-fails/SKILL.md) | 持公钥即可加密候选比对，先查明文空间可枚举性 | 公钥加密随机化审查 |
| 密码学基础 | `stinson-encrypt-authenticate-composition`<br>[加密认证组合检查表](../../../skills/crypto-foundations/stinson-encrypt-authenticate-composition/SKILL.md) | ECB禁用、先签名后加密，自定义拼接MAC默认可伪造 | 加密认证组合构造审计 |
| 密码学基础 | `stinson-hash-property-usage-matching`<br>[Hash性质用途匹配](../../../skills/crypto-foundations/stinson-hash-property-usage-matching/SKILL.md) | 原像/第二原像/碰撞与用途一一对应，SHA-256非充分 | 哈希用途选型检查表 |
| 密码学基础 | `stinson-key-lifetime-rolling`<br>[密钥寿命与参数滚动](../../../skills/crypto-foundations/stinson-key-lifetime-rolling/SKILL.md) | 参数按最优攻击外推做生命周期预算与迁移策略 | 密钥参数生命周期管理 |
| 密码学基础 | `stinson-keysize-not-security`<br>[密钥尺寸不等于安全](../../../skills/crypto-foundations/stinson-keysize-not-security/SKILL.md) | 大密钥空间遇结构弱点即作废，另查四条结构线 | 密钥尺寸≠安全强度 |
| 密码学基础 | `stinson-linearity-kills-ciphers`<br>[线性构造必被解方程](../../../skills/crypto-foundations/stinson-linearity-kills-ciphers/SKILL.md) | 线性/仿射组合的密码构造强度为零，须非线性层 | 线性性致结构性崩溃 |
| 密码学基础 | `stinson-nonce-reuse-failure-checklist`<br>[一次性值复用失败清单](../../../skills/crypto-foundations/stinson-nonce-reuse-failure-checklist/SKILL.md) | IV/nonce/签名k/种子任何复用触发代数级崩溃 | nonce复用即代数崩溃 |
| 密码学基础 | `stinson-partial-leakage-amplification`<br>[部分泄露同态放大审计](../../../skills/crypto-foundations/stinson-partial-leakage-amplification/SKILL.md) | 一位泄漏可经同态运算加二分查找放大为全明文恢复 | 公钥方案泄漏面清点 |
| 密码学基础 | `stinson-signature-homomorphism-breaking`<br>[签名同态伪造审查](../../../skills/crypto-foundations/stinson-signature-homomorphism-breaking/SKILL.md) | 裸RSA签名可由旧签名相乘拼出，必须Hash绑定编码域 | 签名同态致组合伪造 |
| 密码学基础 | `stinson-structural-security-bound`<br>[结构性安全界设计](../../../skills/crypto-foundations/stinson-structural-security-bound/SKILL.md) | 宽轨道/活动S盒数推轮数，用可计算不变量压攻击上界 | 密码结构可证界评估 |
| 密码工程 | `stallings-algorithm-retirement-crypto-agility`<br>[算法退役与密码敏捷治理链](../../../skills/crypto-engineering/stallings-algorithm-retirement-crypto-agility/SKILL.md) | 结构预警→难度外推→套件档位→格式中立→双算法冗余的退役路线图 | 算法退役与套件治理属参数治理 |
| 密码工程 | `stallings-birthday-bound-variant-substitution`<br>[生日界换算与变式调包攻击](../../../skills/crypto-engineering/stallings-birthday-bound-variant-substitution/SKILL.md) | m 位 Hash 抗碰撞仅 m/2 位，变式构造使碰撞成调包攻击 | 哈希长度与碰撞量化属加密 |
| 密码工程 | `stallings-block-cipher-mode-five-axis`<br>[分组密码工作模式五轴评估](../../../skills/crypto-engineering/stallings-block-cipher-mode-five-axis/SKILL.md) | 按开销/错误传播/并行等五轴选模式，CTR 需计数器全局唯一 | 工作模式选型属加密治理 |
| 密码工程 | `stallings-brute-force-three-conditions`<br>[穷举可行三条件](../../../skills/crypto-engineering/stallings-brute-force-three-conditions/SKILL.md) | 算法已知+空间可穷尽+明文可识别，抬高识别门槛即低成本加固 | 密钥空间与识别门槛属加密 |
| 密码工程 | `stallings-computational-security-three-questions`<br>[计算安全三问与一次一密判据](../../../skills/crypto-engineering/stallings-computational-security-three-questions/SKILL.md) | 防谁/防多久/值多少共同定强度档位，OTP 只作验收判据 | 密钥强度定档属参数治理 |
| 密码工程 | `stallings-constraint-driven-encryption-design`<br>[约束反推的存储加密设计](../../../skills/crypto-engineering/stallings-constraint-driven-encryption-design/SKILL.md) | 先列攻击面与功能代数再反推构造，P1619 七条为范例 | 存储加密与FPE设计属加密 |
| 密码工程 | `stallings-deterministic-leak-tweak-binding`<br>[确定性泄漏与tweak绑定](../../../skills/crypto-engineering/stallings-deterministic-leak-tweak-binding/SKILL.md) | 确定性加密泄相等关系，公开唯一 tweak 随对象变化封堵 | 确定性加密泄漏治理属加密 |
| 密码工程 | `stallings-domain-parameter-validation-gate`<br>[域参数与公钥校验闸门](../../../skills/crypto-engineering/stallings-domain-parameter-validation-gate/SKILL.md) | 曲线判别式/安全素数/群成员检查，校验失败即安全事件 | 域参数治理属加密硬闸门 |
| 密码工程 | `stallings-hash-property-application-mapping`<br>[Hash抗性蕴含与应用映射](../../../skills/crypto-engineering/stallings-hash-property-application-mapping/SKILL.md) | 原像/第二原像/碰撞互不蕴含，按用法选抗性且护校验值 | Hash选型映射属加密治理 |
| 密码工程 | `stallings-key-leak-blast-radius-forward-secrecy`<br>[密钥爆炸半径与前向安全](../../../skills/crypto-engineering/stallings-key-leak-blast-radius-forward-secrecy/SKILL.md) | 按能解多少历史定损，长期钥只认证、会话钥临时派生 | 密钥架构与前向安全属加密 |
| 密码工程 | `stallings-key-separation-binding`<br>[密钥用途单一与上下文绑定](../../../skills/crypto-engineering/stallings-key-separation-binding/SKILL.md) | 一钥一用且约束焊进密钥，KDF 纳入用途租约与转录 | 密钥用途纪律属加密治理 |
| 密码工程 | `stallings-meet-in-the-middle-cascade-audit`<br>[中间相遇：级联不叠加](../../../skills/crypto-engineering/stallings-meet-in-the-middle-cascade-audit/SKILL.md) | 双重加密名112实56位，复合构造须按两头夹击重算成本 | 级联强度防御核算属加密 |
| 密码工程 | `stallings-metadata-length-side-channel`<br>[元数据与长度侧信道](../../../skills/crypto-engineering/stallings-metadata-length-side-channel/SKILL.md) | 内容加密后仍泄压缩比/长度/通信存在性，可变填充切断 | 长度元数据泄漏属侧信道 |
| 密码工程 | `stallings-nonce-iv-one-time-constraints`<br>[一次性参数硬约束清单](../../../skills/crypto-engineering/stallings-nonce-iv-one-time-constraints/SKILL.md) | nonce/IV/盐/k 复用各有失效数学，五类参数统一审查 | 一次性参数防御清单属加密 |
| 密码工程 | `stallings-precompute-offline-split`<br>[预计算与在线离线分离](../../../skills/crypto-engineering/stallings-precompute-offline-split/SKILL.md) | 与输入无关的量离线预计算，在线路径轻量化，池按钥护 | 密码运算性能工程属加密 |
| 密码工程 | `stallings-randomness-engineering-governance`<br>[随机数工程与验收治理](../../../skills/crypto-engineering/stallings-randomness-engineering-governance/SKILL.md) | 双轴验收+多种子测试矩阵，熵不足拒发钥而非静默继续 | 随机数治理属加密随机源 |
| 密码工程 | `stallings-side-channel-mitigation-ladder`<br>[侧信道缓解阶梯](../../../skills/crypto-engineering/stallings-side-channel-mitigation-ladder/SKILL.md) | 盲化>恒定时间>随机延时，数学层与实现层分开评估 | 侧信道缓解属加密实现 |
| 密码工程 | `stallings-structural-reduction-parameterized-construction`<br>[结构归约与参数化构造](../../../skills/crypto-engineering/stallings-structural-reduction-parameterized-construction/SKILL.md) | 化归定长组件再论证，海绵三参数派生一族原语 | 密码构造设计方法论属加密 |
| 密码工程 | `stallings-unauthenticated-key-exchange`<br>[无认证密钥交换中间人](../../../skills/crypto-engineering/stallings-unauthenticated-key-exchange/SKILL.md) | 密钥协商≠身份认证，无背书公钥可被双钥替换整体接管 | 中间人反例防御检查归加密 |

**来源分布**：Web应用防御×1、代码审计×1、渗透测试方法论×1、合规测评×2、密码学基础×12、密码工程×19
