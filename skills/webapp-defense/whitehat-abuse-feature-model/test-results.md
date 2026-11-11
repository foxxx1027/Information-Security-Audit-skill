# test-results — whitehat-abuse-feature-model

- 通过: 5/6（83%）
- 诱饵容错: ✓ 全过
- 判定: ✅ 接受
- 盲测方式: 独立 sub-agent 全目录选择题盲测（书级 234 条乱序混合）

## 失败用例

| id | 类型 | 期望 | 实测 | 盲测理由 |
|---|---|---|---|---|
| P006 | edge_case | none | whitehat-signal-reliability | 单一IP信号作防刷依据是否可靠，限流取字段问题 |
