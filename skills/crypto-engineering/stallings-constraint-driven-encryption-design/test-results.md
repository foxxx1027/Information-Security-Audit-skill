# test-results — stallings-constraint-driven-encryption-design

- 通过: 5/6（83%）
- 诱饵容错: ✓ 全过
- 判定: ✅ 接受
- 盲测方式: 独立 sub-agent 全目录选择题盲测（书级 336 条乱序混合）

## 失败用例

| id | 类型 | 期望 | 实测 | 盲测理由 |
|---|---|---|---|---|
| stallings-constraint-driven-encryption-design::edge-01 | edge_case | stallings-constraint-driven-encryption-design | stallings-deterministic-leak-tweak-binding | 密文去重泄漏相等关系 |
