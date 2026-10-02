# dian115-plugins

[dian115](https://github.com/madbrolab/dian115) 第三方插件发布仓库，当前收录：

## 豆瓣订阅中心（douban115）

把豆瓣榜单与豆瓣「想看」列表自动变成 dian115 聚合订阅，并把 Emby 观影记录回写豆瓣。

- 插件 ID：`douban115`
- 运行时：WASM（`dian115:wasm@1`，沙箱运行）
- 兼容宿主：dian115 `>=3.8.51 <5.0.0`（在 4.0.55 上完成验证）
- 本仓库只发布**签名后的插件包**（`.d115p`），不包含源码与私钥

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
| 1.5.3 | `douban115-1.5.3.d115p` | `ca3081aaec57e585b9dd86e571116d8f316d359192b63a42dbd20d9ba9f031ec` |
| 1.5.0 | `douban115-1.5.0.d115p` | `615f69febbbb3aa7b5b257250b422465bfc3b3c7e39f8dfaa562820612e45ae1` |
| 1.4.0 | `douban115-1.4.0.d115p` | `dc5d4366c329fd4be7b9b550aec3f62cc248dd3c57bc8d9e4916c794f92b6b79` |
| 1.3.1 | `douban115-1.3.1.d115p` | `b40be1bed5e6129481af4c5bc2263efc2ea6dcaa66fe18c3bbaf634825a77efe` |
| 1.3.0 | `douban115-1.3.0.d115p` | `28c3e26dcdc3d334b7c1b09fde5dec59b953b90b485fb961bfde5c0f5f5a1285` |
| 1.2.11 | `douban115-1.2.11.d115p` | `86c17f420f62806a7d9bd9bd903ce75b3096ecd2c74ad3d8bc65f05cded004ad` |
| 1.2.10 | `douban115-1.2.10.d115p` | `1ebeee3dcb0ff5a9cad0ceae3da989be4451e152cf4dd21c0ebb3e3122b644b7` |
| 1.2.9 | `douban115-1.2.9.d115p` | `48c8538e3ea2d864df68580b9dd33abc21fd5a8d7e00ddd003463040d8260be1` |
| 1.2.7 | `douban115-1.2.7.d115p` | `0cb954bb1163f2f0e1823403303a072293b6a1a6e2b608bc1672d703172b6577` |
| 1.2.6 | `douban115-1.2.6.d115p` | `0827053d038e37d82a270d948b7ea87fc99b5b8199627272c555c8dec15ad4da` |
| 1.2.5 | `douban115-1.2.5.d115p` | `69f5a5d45865b9521152ff5b49b09b599af6eddb35b05612716ea095134ce465` |
| 1.2.4 | `douban115-1.2.4.d115p` | `397a9dfacb41b16f3eac7c1fd93e6d88044ed82ce9885c91b53f18cd091672d1` |
| 1.2.3 | `douban115-1.2.3.d115p` | `32facc3e707b893958c7c231b5b40b2cf48faad46e74bed855f93af9bdc835f2` |
| 1.2.2 | `douban115-1.2.2.d115p` | `f8dc42803bd04eb4a5da43b5748801f1701e7864322066144f85c627874829c4` |
| 1.2.1 | `douban115-1.2.1.d115p` | `f724267c72d36d8679e34e30dfefcc9ace9c2829ef2d24a66b6f81d5c3449e12` |
| 1.2.0 | `douban115-1.2.0.d115p` | `4fe4dc03129c8582097c9951b87603c39354c171ba829323555cbd4c593df1e4` |
| 1.1.0 | `douban115-1.1.0.d115p` | `295ec798067b5e9a6fefb53cee2d419e44fef5ef8906afc200e1aa9ddd6b7140` |
| 1.0.12 | `douban115-1.0.12.d115p` | `991266dd4d618e0677bf34f83936aa0bcccad0edb890b39f4422e8d53e87a390` |
| 1.0.11 | `douban115-1.0.11.d115p` | `cae0dc9cd04d3d735d53960827c5feb4777e4f11ae87f66b30e7956d639503de` |
| 1.0.10 | `douban115-1.0.10.d115p` | `cac923055e920fbd6e184da4214c962a231ffcb8f93f64b5a81e6e368bbf3f4c` |
| 1.0.9 | `douban115-1.0.9.d115p` | `757a28f2eb2cc3f89464a102f891658bbd78cb577182d354b37a13652d0e756b` |
| 1.0.8 | `douban115-1.0.8.d115p` | `8e814e7b126cd18866bc8b8257f993db158e176c180c6941509bdcfe1d07cad0` |
