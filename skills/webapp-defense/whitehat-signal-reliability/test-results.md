# test-results — whitehat-signal-reliability

- 通过: 5/6（83%）
- 诱饵容错: ✓ 全过
- 判定: ✅ 接受
- 盲测方式: 独立 sub-agent 全目录选择题盲测（书级 234 条乱序混合）

## 失败用例

| id | 类型 | 期望 | 实测 | 盲测理由 |
|---|---|---|---|---|
| P188 | should_trigger | whitehat-signal-reliability | whitehat-trust-assumption-audit | 前端算金额加签可信吗，信任客户端前提审查 |
