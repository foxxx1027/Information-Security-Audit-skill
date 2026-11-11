# test-results — caudit-audit-path-selection

- 通过: 4/6（67%）
- 诱饵容错: ✗ 1 条诱饵失守
- 判定: 🔧 回炉（<80%）
- 盲测方式: 独立 sub-agent 全目录选择题盲测（书级 162 条乱序混合）

## 失败用例

| id | 类型 | 期望 | 实测 | 盲测理由 |
|---|---|---|---|---|
| caudit-audit-path-selection::edge-01 | edge_case | caudit-audit-path-selection | caudit-horizontal-depth-pillars | 年度安全预算投入深度规划属两支柱 |
| caudit-audit-path-selection::should-not-trigger-01 | should_not_trigger | none | caudit-escape-as-last-step | 截断位于校验后属变换顺序判定 |

## 复测（回炉后定向盲测 2026-11-11）

- 全 6 用例重测 24/24 通过（含此前失守诱饵与边界），已接受。
