# test-results — stallings-block-cipher-mode-five-axis

- 通过: 5/6（83%）
- 诱饵容错: ✓ 全过
- 判定: ✅ 接受
- 盲测方式: 独立 sub-agent 全目录选择题盲测（书级 336 条乱序混合）

## 失败用例

| id | 类型 | 期望 | 实测 | 盲测理由 |
|---|---|---|---|---|
| stallings-block-cipher-mode-five-axis::should-trigger-02 | should_trigger | stallings-block-cipher-mode-five-axis | stallings-constraint-driven-encryption-design | 存储加密随机访问约束反推构造 |
