# test-results — whitehat-resource-quota-audit

- 通过: 5/6（83%）
- 诱饵容错: ✓ 全过
- 判定: ✅ 接受
- 盲测方式: 独立 sub-agent 全目录选择题盲测（书级 234 条乱序混合）

## 失败用例

| id | 类型 | 期望 | 实测 | 盲测理由 |
|---|---|---|---|---|
| P146 | should_trigger | whitehat-resource-quota-audit | whitehat-signal-reliability | 按IP限流维度是否可靠，共享出口与可伪造 |
