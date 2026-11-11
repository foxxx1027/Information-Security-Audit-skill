# test-results — whitehat-mitigation-vs-fix

- 通过: 5/6（83%）
- 诱饵容错: ✗ 1 条诱饵失守
- 判定: 🔧 回炉（诱饵失守，容错0）
- 盲测方式: 独立 sub-agent 全目录选择题盲测（书级 234 条乱序混合）

## 失败用例

| id | 类型 | 期望 | 实测 | 盲测理由 |
|---|---|---|---|---|
| P130 | should_not_trigger | none | whitehat-security-assessment | 渗透测试报告组织，写渗透报告适用场景命中 |

## 复测（回炉后定向盲测 2026-11-11）

- 全 6 用例重测 18/18（3 技能合计）全部通过，已接受。
