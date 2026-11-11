# test-results — stallings-protocol-belief-analysis

- 通过: 5/6（83%）
- 诱饵容错: ✗ 1 条诱饵失守
- 判定: 🔧 回炉（诱饵失守，容错0）
- 盲测方式: 独立 sub-agent 全目录选择题盲测（书级 336 条乱序混合）

## 失败用例

| id | 类型 | 期望 | 实测 | 盲测理由 |
|---|---|---|---|---|
| stallings-protocol-belief-analysis::should-not-trigger-01 | should_not_trigger | none | stallings-policy-gradual-rollout | 关旧TLS变更按灰度上线 |

## 复测（回炉后定向盲测 2026-11-11）

- 全 6 用例重测 12/12（2 技能合计）全部通过，已接受。
