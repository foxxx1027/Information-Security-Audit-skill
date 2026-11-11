# test-results — whitehat-parser-consistency-audit

- 通过: 5/6（83%）
- 诱饵容错: ✓ 全过
- 判定: ✅ 接受
- 盲测方式: 独立 sub-agent 全目录选择题盲测（书级 234 条乱序混合）

## 失败用例

| id | 类型 | 期望 | 实测 | 盲测理由 |
|---|---|---|---|---|
| P138 | edge_case | whitehat-parser-consistency-audit | whitehat-mitigation-vs-fix | WAF拦截仍拖库，WAF是减损非修复 |
