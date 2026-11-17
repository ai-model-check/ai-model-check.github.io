# 模型检测 · 中转站模型身份探针快照

模型检测快照每天汇总 Folkbench 公开的模型身份探针结果，可以按模型或按中转站查看：同一模型在各家中转站的一致率、Token 范围和指纹识别结果，以及识别结果与申报模型不一致的观察。做中转站掺假检测时，这些结果只能作为线索：单次结果不能证明模型被替换，部分模型共享底模、指纹无法区分。核对某家中转站时，请结合多次结果和主站页面判断。

发布地址：https://ai-model-check.github.io/

AI 模型身份探针公开快照，按模型和站点查看，数据来自 Folkbench。 数据来自 [folkbench-data](https://github.com/Folkbench/folkbench-data) 的已归档公开快照，由 [Folkbench](https://folkbench.com/?utm_source=ai-model-check&utm_medium=pages&utm_campaign=subsite&utm_content=repo-readme) 维护。

排序沿用主站规则，包含合作档位与运营加分。

[打开站点](https://ai-model-check.github.io/) · [方法说明](https://folkbench.com/methodology?utm_source=ai-model-check&utm_medium=pages&utm_campaign=subsite&utm_content=repo-methodology)

一致率按公开的 agree / total 展示，记录数不是执行次数。单次结果不能证明模型被替换；部分模型共享底模，指纹无法区分。本站使用每日快照，不作周封存。

## 徽章

```markdown
![公开快照](https://ai-model-check.github.io/badge.svg)
```

## 运维

- 每日 21:00（北京时间）读取公开归档发布；失败不覆盖当前版本。
- 固定已审核的 FOLKBENCH_TOOLING_SHA，定时启用变量为 PUBLIC_DISTRIBUTION_ENABLED=true；手动 workflow_dispatch 可在定时关闭时运行。
- 访问来源使用 utm_source=ai-model-check、utm_medium=pages、utm_campaign=subsite。
- 验证变量 BING_SITE_VERIFICATION、BAIDU_SITE_VERIFICATION 为空时不输出标签；取得验证码后填入变量并重新发布。
- sitemap：https://ai-model-check.github.io/sitemap.xml 。本仓库不自动注册或登录搜索平台。
- 不在仓库中写入每日快照；构建只读公共工具和数据，无额外 token。
- 手动 data_ref 可指定数据仓库提交。不存在的 ref 会在真实 checkout 阶段失败，部署步骤不执行。
- 提交和推送使用正常 Git hooks；FOLKBENCH_DISTRIBUTION_TOOL_ROOT 指向已审核的公共工具工作区。

## 兜底发布与 IndexNow

- 原定时任务保持不变，另有两个入口：数据仓库归档成功后的 `repository_dispatch`（`public-snapshot-archived`）通知，以及北京时间 23:35 的备用定时。自动触发时，如果线上 `publish-state.json` 已经是最新快照，就直接结束，不重复发布。
- 自动发布失败时，本仓库会开一个「公开快照站点自动发布失败」issue，之后发布成功会自动关闭。
- 配置仓库变量 `INDEXNOW_KEY` 后，发布产物输出 `/{key}.txt`；部署成功后，把 sitemap 中 lastmod 等于本次归档日期的 URL 推送到 IndexNow。推送失败只记日志，不影响发布结果。

## 其它公开快照视图

- [AI 中转站排行](https://folkbench.github.io/relay-rank/)：按模型的每日公开快照与历史名次
- [中转站检测周报](https://folkbench.github.io/integrity-weekly/)：模型身份探针的每周汇总
- [AI 中转站对比](https://ai-relay-bench.github.io/)：同一模型在各中转站的并排对比
- [AI API 价格对比](https://aiapi-rank.github.io/)：中转站公开标价与官方参考价
- [AI 中转站大全](https://ai-zhongzhuan.github.io/)：站点目录、公开资料与新手指南
