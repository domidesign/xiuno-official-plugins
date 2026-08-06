# 项目规则

## Git 推送后强制刷新 jsDelivr CDN 缓存

每次 `git push` 到 `main` 分支后，由 GitHub Actions 自动触发 jsDelivr purge 强刷，无需手动操作。

- 原始资源根链接：`https://cdn.jsdelivr.net/gh/domidesign/xiuno-official-plugins@main`
- 强刷接口根链接：`https://purge.jsdelivr.net/gh/domidesign/xiuno-official-plugins@main`
- 自动化 workflow：`.github/workflows/purge-jsdelivr.yml`

### 自动化机制

push 到 `main` 后 workflow 自动运行：

1. 计算本次推送变更的文件列表（首次推送时用 `git ls-files` 全量刷新）
2. 过滤掉 `.trae/`、`.github/`、`.DS_Store` 等非 CDN 资源
3. 将变更文件路径用逗号拼接，一次性调用 purge 接口
4. 用 jq 验证返回结果：`status == "finished"`、所有 `paths` 下 `providers` 的 `CF` 和 `FY` 均为 `true`、`throttled` 为 `false`
5. 验证失败自动重试 3 次（每次间隔 5 秒），仍失败则以 error 退出

### 手动强刷（仅当 Actions 未触发时备用）

针对变更文件拼接路径到 purge 根链接后调用：

```bash
curl -s "https://purge.jsdelivr.net/gh/domidesign/xiuno-official-plugins@main/<文件相对路径>"
```

验证标准与自动化一致：返回 JSON 中对应 `paths` 项下 `providers` 的 `CF` 和 `FY` 均为 `true`，且 `throttled` 为 `false`。
