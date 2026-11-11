# test-results — stinson-deterministic-pke-fails

- 通过: 5/6（83%）
- 诱饵容错: ✓ 全过
- 判定: ✅ 接受
- 盲测方式: 独立 sub-agent 全目录选择题盲测（书级 186 条乱序混合）

## 失败用例

| id | 类型 | 期望 | 实测 | 盲测理由 |
|---|---|---|---|---|
| deterministic-pke-edge-01 | edge_case | stinson-encrypt-authenticate-composition | stinson-deterministic-pke-fails | ECB 即确定性加密按明文空间审查 |
