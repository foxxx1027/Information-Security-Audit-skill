# test-results — caudit-server-side-state-truth

- 通过: 4/6（67%）
- 诱饵容错: ✓ 全过
- 判定: 🔧 回炉（<80%）
- 盲测方式: 独立 sub-agent 全目录选择题盲测（书级 162 条乱序混合）

## 失败用例

| id | 类型 | 期望 | 实测 | 盲测理由 |
|---|---|---|---|---|
| caudit-server-side-state-truth::edge-01 | edge_case | none | caudit-server-side-state-truth | 已读状态存放位置的真值裁决 |
| caudit-server-side-state-truth::should-trigger-03 | should_trigger | caudit-server-side-state-truth | caudit-payment-invariants | 开通扣费时间差重放属原子幂等 |

## 复测（回炉后定向盲测 2026-11-11）

- 全 6 用例重测 24/24 通过（含此前失守诱饵与边界），已接受。
