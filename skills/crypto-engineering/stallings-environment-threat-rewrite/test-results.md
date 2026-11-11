# test-results — stallings-environment-threat-rewrite

- 通过: 5/6（83%）
- 诱饵容错: ✓ 全过
- 判定: ✅ 接受
- 盲测方式: 独立 sub-agent 全目录选择题盲测（书级 336 条乱序混合）

## 失败用例

| id | 类型 | 期望 | 实测 | 盲测理由 |
|---|---|---|---|---|
| stallings-environment-threat-rewrite::edge-01 | edge_case | stallings-environment-threat-rewrite | none | 机房网络未变，同域增量变更 |
