# test-results — caudit-trust-tier-isolation

- 通过: 5/6（83%）
- 诱饵容错: ✓ 全过
- 判定: ✅ 接受
- 盲测方式: 独立 sub-agent 全目录选择题盲测（书级 162 条乱序混合）

## 失败用例

| id | 类型 | 期望 | 实测 | 盲测理由 |
|---|---|---|---|---|
| caudit-trust-tier-isolation::edge-01 | edge_case | none | caudit-trust-tier-isolation | 同表多角色是否按信任级拆表判别 |
