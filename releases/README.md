# PartnerNet Software 发布索引

每个产品一个子目录：`releases/<product>/README.md`。产品标识使用小写字母、数字与连字符；当前为 `unisacc` 和 `ujs`。目录仅保存说明、链接与 SHA256，不存放二进制、安装包或归档文件，也不把它们提交进 git 历史。

## GitHub Releases 对应关系

本仓库 GitHub Release tag 统一为 `<product>-v<version>`，例如 `unisacc-v0.0.27`。一个产品版本对应一个 Release；同一 Release 可含多个平台附件。上游版本 tag 可以不同，必须通过 Source 明确链接。tag 标识发布版本，源码以 Source 指向的产品仓库为准。

最终二进制上传至 `partnernetsoftware/unisa` 的 GitHub Releases。复制上游附件时保留文件名与字节内容；如字节内容变化，应发布新版本，不覆盖已索引附件。索引不使用 `latest` 下载地址。

## 索引表

每个可下载二进制附件一行，同一版本可出现多行，版本按发布时间从新到旧排列。

| 字段 | 约定 |
|---|---|
| Version | 产品版本，不带 tag 前缀 |
| Date (UTC) | 本仓库 Release 的发布日期，`YYYY-MM-DD` |
| Release | 本仓库 Release 页面链接，标签显示完整 tag |
| Asset | 与附件文件名一致的直接下载链接 |
| Target | 操作系统和架构；跨平台文件列出所有适用目标 |
| SHA256 | 下载文件字节的 SHA256，64 位小写十六进制 |
| Source | 上游产品 Release 或不可变源码版本链接 |

空表模板：

```markdown
| Version | Date (UTC) | Release | Asset | Target | SHA256 | Source |
|---|---|---|---|---|---|---|
```

发布顺序：确定上游版本 → 上传并发布本仓库 Release → 下载核对附件与 SHA256 → 更新产品索引。建议 Release 同时附带 `SHA256SUMS.txt`；它是校验辅助文件，不需要作为二进制单独列入表格。只有已发布且可下载的附件才进入索引。
