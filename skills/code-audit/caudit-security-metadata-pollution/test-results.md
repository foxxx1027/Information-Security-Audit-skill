# test-results — caudit-security-metadata-pollution

- 通过: 5/6（83%）
- 诱饵容错: ✓ 全过
- 判定: ✅ 接受
- 盲测方式: 独立 sub-agent 全目录选择题盲测（书级 162 条乱序混合）

## 失败用例

| id | 类型 | 期望 | 实测 | 盲测理由 |
|---|---|---|---|---|
| caudit-security-metadata-pollution::edge-01 | edge_case | caudit-type-context-defense | caudit-security-metadata-pollution | 判别page属数据还是安全元数据 |
