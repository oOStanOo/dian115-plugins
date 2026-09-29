# dian115-plugins

[dian115](https://github.com/madbrolab/dian115) 第三方插件发布仓库，当前收录：

- [豆瓣订阅中心（douban115）](#豆瓣订阅中心douban115)
- [下载中心（dian115.download-center）](#下载中心dian115download-center)

本仓库只发布**签名后的插件包**（`.d115p`），不包含源码与私钥。

## 豆瓣订阅中心（douban115）

把豆瓣榜单与豆瓣「想看」列表自动变成 dian115 聚合订阅，并把 Emby 观影记录回写豆瓣。

- 插件 ID：`douban115`
- 运行时：WASM（`dian115:wasm@1`，沙箱运行）
- 兼容宿主：dian115 `>=3.8.51 <5.0.0`（在 4.0.55 上完成验证）

### 功能

- **榜单订阅**：RSSHub 的豆瓣榜单（即将上映 / 实时热门 / 华语口碑 / 全球口碑 / 电影口碑 / BangumiTV），把条目解析成 TMDB 身份后创建聚合订阅，已订阅的自动跳过。
- **想看订阅**：支持多个豆瓣用户的「想看」列表，合并去重，来源用户以标签展示。
- **媒体识别**：标题变体匹配 ＋ TMDB 候选打分；匹配不上时用豆瓣条目的原名/又名重搜。
- **Emby 观影回写**：按 Emby 播放记录把条目在豆瓣标记为「看过 / 在看」。
- **CookieCloud**：可直接读取 dian115 内置的 CookieCloud 同步豆瓣 Cookie。
- **仪表盘**：订阅/历史/识别结果一览，支持清理历史与黑名单。

### 安装

两种方式任选：

1. **自定义插件仓库（推荐）**：在 dian115 插件中心 → 添加自定义仓库，仓库地址填

   ```
   https://github.com/oOStanOo/dian115-plugins
   ```

   宿主会自动读取本仓库的 `plugin-market/index.json` 并列出可安装插件。

2. **手动导入**：从 [Releases](https://github.com/oOStanOo/dian115-plugins/releases) 下载 `.d115p`，在插件中心导入。

### 校验

```
shasum -a 256 douban115-<version>.d115p
```

与 `plugin-market/index.json` 中 `sha256` 及 Release 说明里的值比对。

### 版本

| 版本 | 文件 | SHA-256 |
|---|---|---|
| 1.0.12 | `douban115-1.0.12.d115p` | `991266dd4d618e0677bf34f83936aa0bcccad0edb890b39f4422e8d53e87a390` |
| 1.0.11 | `douban115-1.0.11.d115p` | `cae0dc9cd04d3d735d53960827c5feb4777e4f11ae87f66b30e7956d639503de` |
| 1.0.10 | `douban115-1.0.10.d115p` | `cac923055e920fbd6e184da4214c962a231ffcb8f93f64b5a81e6e368bbf3f4c` |
| 1.0.9 | `douban115-1.0.9.d115p` | `757a28f2eb2cc3f89464a102f891658bbd78cb577182d354b37a13652d0e756b` |
| 1.0.8 | `douban115-1.0.8.d115p` | `8e814e7b126cd18866bc8b8257f993db158e176c180c6941509bdcfe1d07cad0` |

## 下载中心（dian115.download-center）

把 MoviePilot V3 的 `downloadmanagerlocal` 移植成 dian115 WASM 插件：一套页面管理下载器的做种生命周期。

- 插件 ID：`dian115.download-center`
- 运行时：WASM（`dian115:wasm@1`，沙箱运行）
- 兼容宿主：dian115 `>=3.8.51 <5.0.0`（在 4.0.58 上完成验证）

### 功能

- **转移做种**：源下载器导出已完成种子的 `.torrent` 后推送到目标下载器继续做种；触发方式支持「种子完成时间 + 延迟分钟」与「兜底间隔」两种，可只转移已完成、转移后打标签。
- **种子重命名**：经 TMDB 识别后重命名种子（识别不出时不改动原名）。
- **站点标签**：按 tracker 匹配站点并给种子打标签。
- **做种校验**：按做种时长/分享率暂停或删除种子。
- **速度监控**：上传/下载速度异常检测并发通知。
- **上传限速**：按时间段的上传限速策略。
- **IYUU 辅种**：IYUU 站点哈希索引查询 + 辅种成功后自动重校验。

下载器（qBittorrent / Transmission）与 PT 站点的地址、凭据全部由用户在配置页自行填写，插件经宿主 Broker 直连，不依赖官方下载器模块，也不需要预先声明站点域名。

### 安装

同上文「自定义插件仓库」或「手动导入」，Release 标签为 `download-center-v<版本>`。

### 校验

```
shasum -a 256 dian115.download-center-<version>.d115p
```

### 版本

| 版本 | 文件 | SHA-256 |
|---|---|---|
| 1.0.0 | `dian115.download-center-1.0.0.d115p` | `af70ba792fc999bb555599a5cac89cf79880d2e212dff2922300123eb70bb87f` |
