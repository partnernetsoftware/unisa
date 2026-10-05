# UNISA 站点接线短摘

核实：2026-10-05（只读调查，未修改线上配置）。

公司级权威记录在私有仓
[company-dev-hub：站点与域名思维树](https://github.com/partnernetsoftware/company-dev-hub/blob/main/docs/products/site-and-domain-tree.md)。
完整 DNS、发布源、HTTPS、代理边界与接线验收流程只维护在那里，避免两处配置说明漂移。

- 现有 MiniCon 子域站采用 Cloudflare 代理 → GitHub Pages（`main:/docs`），可作接线参照。
- UNISA 的 `docs/CNAME` 已是 `unisa.agenterm.work`，但本次 API 实测 `has_pages=false`、Pages 接口 404，
  权威 DNS 返回 NXDOMAIN；当前尚未接线，不能将页面提交或 CNAME 文件视为已上线。
- 下一步需启用本仓 `main:/docs` Pages、绑定自定义域名，再配置精确子域 CNAME 指向
  `partnernetsoftware.github.io` 并验证 HTTPS。此处仅记录方案，本次未执行。

以上是调查时点快照；后续状态以公司仓思维树的最新核实为准。`docs/CNAME` 保持不变。
