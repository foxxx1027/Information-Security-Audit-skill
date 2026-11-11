# test-results — stallings-trust-topology-blast-radius

- 通过: 5/6（83%）
- 诱饵容错: ✓ 全过
- 判定: ✅ 接受
- 盲测方式: 独立 sub-agent 全目录选择题盲测（书级 336 条乱序混合）

## 失败用例

| id | 类型 | 期望 | 实测 | 盲测理由 |
|---|---|---|---|---|
| stallings-trust-topology-blast-radius::edge-01 | edge_case | stallings-trust-topology-blast-radius | stallings-unauthenticated-key-exchange | TOFU与内部CA首次信任选型 |
