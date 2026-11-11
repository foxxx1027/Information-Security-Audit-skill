# test-results — isms-document-consistency-matrix

- 通过: 5/6（83%）
- 诱饵容错: ✓ 全过
- 判定: ✅ 接受
- 盲测方式: 独立 sub-agent 全目录选择题盲测（书级 156 条乱序混合）

## 失败用例

| id | 类型 | 期望 | 实测 | 盲测理由 |
|---|---|---|---|---|
| BT-054 | edge_case | isms-counterfactual-document-review | isms-document-consistency-matrix | 程序与产出物断链核对，从对应关系审 |
