# test-results — whitehat-root-cause-patch-discipline

- 通过: 5/6（83%）
- 诱饵容错: ✓ 全过
- 判定: ✅ 接受
- 盲测方式: 独立 sub-agent 全目录选择题盲测（书级 234 条乱序混合）

## 失败用例

| id | 类型 | 期望 | 实测 | 盲测理由 |
|---|---|---|---|---|
| P152 | should_trigger | whitehat-root-cause-patch-discipline | whitehat-mitigation-vs-fix | WAF拦住工单就想关，减损控件不能结案 |
