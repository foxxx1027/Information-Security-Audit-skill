# test-results — stallings-challenge-response-design-criteria

- 通过: 5/6（83%）
- 诱饵容错: ✓ 全过
- 判定: ✅ 接受
- 盲测方式: 独立 sub-agent 全目录选择题盲测（书级 336 条乱序混合）

## 失败用例

| id | 类型 | 期望 | 实测 | 盲测理由 |
|---|---|---|---|---|
| stallings-challenge-response-design-criteria::should-trigger-03 | should_trigger | stallings-challenge-response-design-criteria | stallings-anti-replay-window-engineering | OTP新鲜性与旧码重放判定 |
