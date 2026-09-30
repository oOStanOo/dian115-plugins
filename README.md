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
| 1.1.0 | `douban115-1.1.0.d115p` | `295ec798067b5e9a6fefb53cee2d419e44fef5ef8906afc200e1aa9ddd6b7140` |
| 1.0.12 | `douban115-1.0.12.d115p` | `991266dd4d618e0677bf34f83936aa0bcccad0edb890b39f4422e8d53e87a390` |
| 1.0.11 | `douban115-1.0.11.d115p` | `cae0dc9cd04d3d735d53960827c5feb4777e4f11ae87f66b30e7956d639503de` |
| 1.0.10 | `douban115-1.0.10.d115p` | `cac923055e920fbd6e184da4214c962a231ffcb8f93f64b5a81e6e368bbf3f4c` |
| 1.0.9 | `douban115-1.0.9.d115p` | `757a28f2eb2cc3f89464a102f891658bbd78cb577182d354b37a13652d0e756b` |
| 1.0.8 | `douban115-1.0.8.d115p` | `8e814e7b126cd18866bc8b8257f993db158e176c180c6941509bdcfe1d07cad0` |

## 文档资源库（doc115）

<!-- versions:doc115 -->
| 版本 | 文件 | SHA-256 |
| 1.0.16 | `doc115-1.0.16.d115p` | `75e9a4d6442eb6248a62cc5f0942231fb00ece5428b0f297a1f4eb4b434a5547` |
| 1.0.15 | `doc115-1.0.15.d115p` | `caae83739a2f96c81288b17876089ea7ec3986ebdb88b43afbf7dc8efc0ea4a5` |
| 1.0.14 | `doc115-1.0.14.d115p` | `d2f69e924a1ae2613f5abb2d3ea8ef07a7b0c9953fac78646c2d4392b7195a7e` |
| 1.0.13 | `doc115-1.0.13.d115p` | `c27fabb55eb50e6a11a27a9375db1831072acd6243ace64f811cbe67d5a6b934` |
| 1.0.12 | `doc115-1.0.12.d115p` | `1889c54ec056168a59c746f0922138ac59decf4308e65ff5f2ef6d8e20976883` |
| 1.0.11 | `doc115-1.0.11.d115p` | `bc0c424e1fe321d840b4e4868dc903a87d748781a1fc92781ccb39325273ef8c` |
| 1.0.10 | `doc115-1.0.10.d115p` | `e34b9162883cded7348ad4f33230f9014225133c161e024aaf04bdc9897ef771` |
| 1.0.9 | `doc115-1.0.9.d115p` | `c00943407e4787ae4c9432fb4b38b5f7c7520d6e15fae4a463f8190a0f666b84` |
| 1.0.8 | `doc115-1.0.8.d115p` | `892a463361004ef752d31ee2acb6a5b495e47d1c10eeba6a3c053dbdb64df34f` |
| 1.0.7 | `doc115-1.0.7.d115p` | `ed7d16022fd2791f64a0b2ab280d80d67358a847645af2b4135d342f25e93521` |
| 1.0.6 | `doc115-1.0.6.d115p` | `9658950c4317d4b764d0cdc24f003de94e8180f0d032491d5bea267fe6f34a6f` |
| 1.0.5 | `doc115-1.0.5.d115p` | `2e159a4c7c6a21785001a3371eab084434bb6ec506306f5dd061f070d68128d6` |
| 1.0.4 | `doc115-1.0.4.d115p` | `76ce4e00dbd2cdbcc15e75882af2e32235b54ada9369e32c756c4f025483994b` |
| 1.0.3 | `doc115-1.0.3.d115p` | `a0af6b2b67bad74680d57d05c6e0fbecf469f07801d6a8ad9da415b569a21e52` |
| 1.0.2 | `doc115-1.0.2.d115p` | `3e497399c9430238276c03a1092a0f0f025259c46a052683909a62479336b604` |
| 1.0.1 | `doc115-1.0.1.d115p` | `a30d29586afc10010dfad64a23400a75829ea22626fd43196df9a1c402b7a357` |
|---|---|---|
| 1.0.0 | `doc115-1.0.0.d115p` | `20f04ec0f664d61aac93ba29137cfa7f09e22d8f49a9e9259f88e8501d779808` |

