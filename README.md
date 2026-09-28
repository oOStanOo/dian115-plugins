# 豆瓣订阅中心（dian115 插件）

把豆瓣榜单与豆瓣「想看」列表自动变成 dian115 聚合订阅，并把 Emby 观影记录回写豆瓣。

- 插件 ID：`local.douban115`
- 运行时：WASM（`dian115:wasm@1`，沙箱运行，256 MiB 线性内存上限）
- 兼容宿主：dian115 `>=3.8.51 <5.0.0`（在 4.0.55 上完成验证）
- 本仓库只发布**签名后的插件包**（`.d115p`），不包含源码与私钥

## 功能

- **榜单订阅**：RSSHub 的豆瓣榜单（即将上映 / 实时热门 / 华语口碑 / 全球口碑 / 电影口碑 / BangumiTV），把条目解析成 TMDB 身份后创建聚合订阅，已订阅的自动跳过。
- **想看订阅**：支持多个豆瓣用户的「想看」列表，合并去重，来源用户以标签展示。
- **媒体识别**：标题变体匹配（剥篇章名 → 剥季号 → 主副标题 → 逐词递减）＋ TMDB 候选打分（名称相关性 + 年份 + 封顶热度 + 最低阈值）；仍匹配不上时用豆瓣条目的原名/又名重搜，解决「TMDB 只有原名」的条目（如《流人 第六季》）。
- **Emby 观影回写**：按 Emby 播放记录把条目在豆瓣标记为「看过 / 在看」。
- **CookieCloud**：可直接读取 dian115 内置的 CookieCloud 同步豆瓣 Cookie，不必手填。
- **仪表盘**：订阅/历史/识别结果一览，支持清理历史与黑名单。

## 安装

1. 从 [Releases](https://github.com/oOStanOo/douban115-plugin/releases) 下载对应版本的 `.d115p`；
2. 打开 dian115 插件中心 → 导入插件包，按提示确认权限即可；
3. 或在插件中心添加 `https://github.com/madbrolab/dian115` 市场（收录后可直接从市场安装）。

导入不会自动发布到市场，安装路径与校验规则完全一致（签名、完整性、Manifest、权限逐条一致）。

## 权限

| 类型 | 用途 |
|---|---|
| `GET /api/tmdb/search`、`GET /api/tmdb/movie/:id`、`GET /api/tmdb/tv/:id` | 解析条目的 TMDB 身份 |
| `GET/POST /api/subscribe/pool/intents` | 查询现有订阅去重、创建聚合订阅 |
| `GET/PUT /api/plugin-runtime/storage/:key` | 读写插件自己的配置与历史 |
| `POST /api/notifications/plugin` | 推送同步结果通知 |
| 豆瓣（www / movie / m）、TMDB、RSSHub、`127.0.0.1:3000`（CookieCloud）等网络来源 | 抓取榜单与想看数据、回写观看状态 |

网络来源里本机 CookieCloud 地址声明为 `proxy_mode: direct`，避免被宿主全局代理拦截。

## 版本

| 版本 | 文件 | SHA-256 |
|---|---|---|
| 1.0.8 | `local.douban115-1.0.8.d115p` | `657aa397bf67050f23c113007fe488152f9194a5b22a386922cf305edd49f239` |

1.0.8 的重点是把榜单 / 想看 / Emby 三类同步改为**分片执行**：每片只做几秒的工作、进度落盘、被回收后从断点继续，解决「任务跑久了插件崩溃重启、且永远跑不完」的问题；Emby 同步还加了每轮条数上限与连续失败熔断。

## 校验

```bash
shasum -a 256 local.douban115-1.0.8.d115p
# 657aa397bf67050f23c113007fe488152f9194a5b22a386922cf305edd49f239
```

包内 `manifest.json` / `integrity.json` / `signature.json` 由 Ed25519 私钥签名，安装时宿主会校验签名与完整性。
