# test-results — stallings-keyless-mutation-test

- 通过: 5/6（83%）
- 诱饵容错: ✓ 全过
- 判定: ✅ 接受
- 盲测方式: 独立 sub-agent 全目录选择题盲测（书级 336 条乱序混合）

## 失败用例

| id | 类型 | 期望 | 实测 | 盲测理由 |
|---|---|---|---|---|
| stallings-keyless-mutation-test::should-trigger-02 | should_trigger | stallings-keyless-mutation-test | stallings-crypto-operation-ordering | MAC覆盖域漏IV遭位翻转 |
