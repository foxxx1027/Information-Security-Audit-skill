# test-results — whitehat-framework-authority-audit

- 通过: 5/6（83%）
- 诱饵容错: ✓ 全过
- 判定: ✅ 接受
- 盲测方式: 独立 sub-agent 全目录选择题盲测（书级 234 条乱序混合）

## 失败用例

| id | 类型 | 期望 | 实测 | 盲测理由 |
|---|---|---|---|---|
| P123 | should_trigger | whitehat-framework-authority-audit | whitehat-context-encoding | 模板自动转义够吗，auto-escape能力评估 |
