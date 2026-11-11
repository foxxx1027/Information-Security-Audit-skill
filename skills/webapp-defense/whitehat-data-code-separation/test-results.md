# test-results — whitehat-data-code-separation

- 通过: 5/6（83%）
- 诱饵容错: ✓ 全过
- 判定: ✅ 接受
- 盲测方式: 独立 sub-agent 全目录选择题盲测（书级 234 条乱序混合）

## 失败用例

| id | 类型 | 期望 | 实测 | 盲测理由 |
|---|---|---|---|---|
| P074 | should_trigger | whitehat-data-code-separation | whitehat-context-encoding | 转义了日志仍被CRLF注入，输出场景编码对应 |
