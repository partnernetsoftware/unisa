# unisacc 包索引

PartnerNet Software 为 unisacc 维护的包发现入口。unisacc 是 neural-network-based compiler，网络由 TSV 表 DSL 构造，不是训练出来的。

## 格式约定（草案 v1）

入口为本目录 `index.json`，使用 UTF-8 标准 JSON，不支持注释。`index.json` 是可复制的空模板，空数组表示没有已收录项目；不加入虚构项目或占位下载地址。目前仅定义元数据格式，客户端读取、安装与兼容性判断尚待产品仓库实现。

| 顶层字段 | 类型 | 约定 |
|---|---|---|
| schema_version | integer | 必填，当前为 `1`；不兼容变更递增 |
| publisher | string | 必填，固定为 `PartnerNet Software`，表示索引维护者 |
| product | string | 必填，消费索引的产品标识 |
| entries | array | 必填，每个元素是一个已发布版本的元数据记录 |

## 记录字段

下列字段均必填，除明确注明可选者。字符串不得为空。

| 字段 | 类型 | 约定 |
|---|---|---|
| id | string | 稳定标识，`<owner>/<name>`；两段均匹配 `[a-z0-9]+(?:-[a-z0-9]+)*` |
| name | string | 展示名称 |
| version | string | SemVer 2.0.0，不带 `v` 前缀 |
| description | string | 简短用途说明 |
| publisher | string | 此项目的实际发布者，不等同于索引维护者 |
| license | string | SPDX 许可证表达式 |
| source_url | string | HTTPS 源码版本链接，应指向固定 tag 或 commit |
| release_url | string | HTTPS 发布页面链接 |
| compatibility | object | 产品兼容信息，字段见下文 |
| artifacts | array | 至少一个附件对象，字段见下文 |

记录唯一键为 `(id, version)`。

`compatibility` 必含 `unisacc_min`（SemVer，最低兼容版本，包含边界），可选 `unisacc_max_exclusive`（SemVer，最高版本排除边界），若提供上界必须大于下界。缺少上界表示发布者没有声明上限，不保证未来版本兼容。依赖解析、安装指令与包内布局不在本草案中定义。

## 附件字段

| 字段 | 类型 | 约定 |
|---|---|---|
| filename | string | 实际下载文件名，不能含路径分隔符 |
| url | string | 固定版本的 HTTPS 直接下载链接；不得使用 `latest` |
| sha256 | string | 下载文件字节的 SHA256，匹配 `[0-9a-f]{64}` |
| targets | array of strings | 至少一个目标：`linux-x86_64`、`linux-arm64`、`macos-x86_64`、`macos-arm64`、`windows-x86_64`、`windows-arm64` 或 `any`；`any` 单独使用，表示平台无关 |

同一记录的附件 `filename` 不重复，且目标不得重叠，避免客户端无法唯一选择附件。SHA256 校验成功后才能消费附件；校验值用于完整性检查，不代表签名或安全审核。二进制与归档仅放发布服务，git 中仅保存索引。已索引版本的附件 URL 与 SHA256 不覆盖修改，内容更新需发布新版本。

新增记录前核对发布页面、固定下载链接、实际文件 SHA256、许可证和兼容声明。`entries` 按 `id` 升序排列，同一 id 按 SemVer 优先级降序排列；相同优先级按完整版本字符串升序排列。草案允许增加可选字段，读取方忽略未知字段；不兼容变化必须升级 `schema_version`。

## 空模板

```json
{
  "schema_version": 1,
  "publisher": "PartnerNet Software",
  "product": "unisacc",
  "entries": []
}
```
