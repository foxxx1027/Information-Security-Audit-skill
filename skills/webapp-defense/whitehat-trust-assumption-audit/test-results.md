# test-results — whitehat-trust-assumption-audit

- 通过: 4/6（67%）
- 诱饵容错: ✓ 全过
- 判定: 🔧 回炉（<80%）
- 盲测方式: 独立 sub-agent 全目录选择题盲测（书级 234 条乱序混合）

## 失败用例

| id | 类型 | 期望 | 实测 | 盲测理由 |
|---|---|---|---|---|
| P213 | should_trigger | whitehat-trust-assumption-audit | whitehat-continuous-security-verification | 厂商承诺当安全状态，外部保障需持续验证 |
| P216 | edge_case | whitehat-trust-assumption-audit | whitehat-defense-in-depth | Token加防火墙仍被打，层间配合与摆位问题 |

## 复测（回炉后定向盲测 2026-11-11）

- 全 6 用例重测 18/18（3 技能合计）全部通过，已接受。
