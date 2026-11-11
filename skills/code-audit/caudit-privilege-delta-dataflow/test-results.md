# test-results — caudit-privilege-delta-dataflow

- 通过: 5/6（83%）
- 诱饵容错: ✓ 全过
- 判定: ✅ 接受
- 盲测方式: 独立 sub-agent 全目录选择题盲测（书级 162 条乱序混合）

## 失败用例

| id | 类型 | 期望 | 实测 | 盲测理由 |
|---|---|---|---|---|
| caudit-privilege-delta-dataflow::edge-01 | edge_case | none | caudit-privilege-delta-dataflow | 工单谁写谁读是否权限差通道判定 |
