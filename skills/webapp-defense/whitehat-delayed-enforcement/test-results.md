# test-results — whitehat-delayed-enforcement

- 通过: 5/6（83%）
- 诱饵容错: ✓ 全过
- 判定: ✅ 接受
- 盲测方式: 独立 sub-agent 全目录选择题盲测（书级 234 条乱序混合）

## 失败用例

| id | 类型 | 期望 | 实测 | 盲测理由 |
|---|---|---|---|---|
| P108 | edge_case | whitehat-delayed-enforcement | whitehat-abuse-feature-model | 误砍正常大单，三维交叉验证降误杀 |
