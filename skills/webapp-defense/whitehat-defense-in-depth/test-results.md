# test-results — whitehat-defense-in-depth

- 通过: 5/6（83%）
- 诱饵容错: ✓ 全过
- 判定: ✅ 接受
- 盲测方式: 独立 sub-agent 全目录选择题盲测（书级 234 条乱序混合）

## 失败用例

| id | 类型 | 期望 | 实测 | 盲测理由 |
|---|---|---|---|---|
| P097 | should_trigger | whitehat-defense-in-depth | whitehat-mitigation-vs-fix | 买了WAF代码漏洞还要修吗，WAF是减损控件 |
