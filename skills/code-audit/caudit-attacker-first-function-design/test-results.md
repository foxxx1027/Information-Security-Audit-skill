# test-results — caudit-attacker-first-function-design

- 通过: 5/6（83%）
- 诱饵容错: ✓ 全过
- 判定: ✅ 接受
- 盲测方式: 独立 sub-agent 全目录选择题盲测（书级 162 条乱序混合）

## 失败用例

| id | 类型 | 期望 | 实测 | 盲测理由 |
|---|---|---|---|---|
| caudit-attacker-first-function-design::edge-01 | edge_case | caudit-logic-vuln-audit | caudit-attacker-first-function-design | 上线前补安全检查属攻击者先行评审 |
