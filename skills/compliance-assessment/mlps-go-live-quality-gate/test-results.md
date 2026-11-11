# test-results — mlps-go-live-quality-gate

- 通过: 5/6（83%）
- 诱饵容错: ✗ 1 条诱饵失守
- 判定: 🔧 回炉（诱饵失守，容错0）
- 盲测方式: 独立 sub-agent 全目录选择题盲测（书级 228 条乱序混合）

## 失败用例

| id | 类型 | 期望 | 实测 | 盲测理由 |
|---|---|---|---|---|
| mlps-go-live-quality-gate::should-not-trigger-02 | should_not_trigger | mlps-delivery-completeness-check | none | 运维移交非项目交付验收 |

## 复测（回炉后定向盲测 2026-11-11）

- 全 6 用例重测 24/24 通过（含此前失守诱饵与边界），已接受。
