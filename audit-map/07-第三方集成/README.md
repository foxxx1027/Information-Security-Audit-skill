# 07-第三方集成 · 第三方集成审计 —— 技能说明

## 本目录审计范围

审计范围：对接第三方接口、OAuth、单点登录、支付接口；信任边界、回调劫持、第三方 SDK 风险、接口鉴权。

## 技能清单（6 个）

| 集合 | 技能 | 一句话说明 | 归类理由 |
|---|---|---|---|
| 渗透测试方法论 | `wahh-shared-cloud-threat-model`<br>[共享云环境威胁模型](../../skills/pentest-methodology/wahh-shared-cloud-threat-model/SKILL.md) | 恶意租户与受害租户双威胁，隔离三措施与云特有攻击面 | 多租户共享环境隔离审查 |
| 密码学基础 | `stinson-certificate-validation-checklist`<br>[证书验证审计清单](../../skills/crypto-foundations/stinson-certificate-validation-checklist/SKILL.md) | 验签名/有效期/撤销/用途四步，信任锚治理与fail-open | 证书与信任基础设施审计 |
| 密码学基础 | `stinson-public-key-parameter-hygiene`<br>[公钥参数卫生检查表](../../skills/crypto-foundations/stinson-public-key-parameter-hygiene/SKILL.md) | RSA/DL/ECC参数结构弱点与私钥泄露处置逐项核对 | 公钥参数与密管卫生 |
| 密码工程 | `stallings-key-counting-hierarchy`<br>[组合计数与密钥分层](../../skills/crypto-engineering/stallings-key-counting-hierarchy/SKILL.md) | N(N-1)/2 计数变可算问题，层次坍缩按成本×频率分层 | 密钥分发架构属第三方集成 |
| 密码工程 | `stallings-revocation-as-propagation`<br>[撤销即通知传播](../../skills/crypto-engineering/stallings-revocation-as-propagation/SKILL.md) | 撤销本质是通知传播，有效期换不设防窗口须声明生效时限 | 吊销传播与PKI信任属集成 |
| 密码工程 | `stallings-trust-topology-blast-radius`<br>[信任拓扑与爆炸半径](../../skills/crypto-engineering/stallings-trust-topology-blast-radius/SKILL.md) | 集中度×密钥量双坐标，量化背书者失陷能冒充多少身份 | 信任拓扑治理属第三方集成 |

**来源分布**：渗透测试方法论×1、密码学基础×2、密码工程×3

## 覆盖缺口

缺口提示：OAuth 回调劫持、支付接口对账、第三方 SaaS 风险评估暂无直接技能，可借道 01-资产边界与 09-通用方法论的信任边界类技能。
