# dian115-plugins

[dian115](https://github.com/madbrolab/dian115) 第三方插件发布仓库，当前收录：

## 豆瓣订阅中心（douban115）

把豆瓣榜单与豆瓣「想看」列表自动变成 dian115 聚合订阅，并把 Emby 观影记录回写豆瓣。

- 插件 ID：`douban115`
- 当前版本：**2.0.7**（`.dian115p` / `protected-v4`）
- 运行时：插件 API v3 —— 后台 JavaScript + 宿主接口（不再使用 WASM）
- 兼容宿主：dian115 `>=5.0.0`（在 5.0.60 / 5.0.69 上完成验证）；dian115 4.x 请留在 1.14.0 的 `.d115p`
- 本仓库只发布**插件包**（`.dian115p`），不包含私钥
- 交付格式：**`protected-v4` 编译签名包**（dian115 5.0.69 起，新正式安装与更新强制要求），由宿主本地「编译 MCP」签发；源码包只允许管理员作本机调试导入
- UI 资源约束：正式包只把 `ui/` 目录暴露成浏览器静态资源，`ui/*.js` **不得** `import '../lib/'`；UI 需要的纯函数模块放在 `ui/lib/`（与根 `lib/` 保持同步，自测会校验）

> 2.0.0 起插件随 dian115 改版重写：容器从 `.d115p`（WASM）换成 `.dian115p`（后台 JS）。
> TMDB、订阅池、存储全部改走宿主接口，不再需要插件侧密钥。
> **升级：插件中心 → 第三方插件 → 市场 → 刷新市场 → 点「更新」原地升级**，配置 / 快照 / 订阅历史都会保留。
> **不要「卸载并清空数据」再装**（会清空插件数据）；本地上传 `.dian115p` 只用于首次安装 —— 同 id 覆盖安装会被宿主静默忽略。

### 功能

- **榜单订阅**：RSSHub 的豆瓣榜单（一周口碑电影 / 豆瓣热门电影 / 实时热门电影 / 实时热门电视 / 华语口碑剧集 / 全球口碑剧集 / 国内口碑综艺 / 国外口碑综艺 / BangumiTV）+ 自定义路由，把条目解析成 TMDB 身份后创建聚合订阅，已订阅的自动跳过。
- **想看订阅**：支持多个豆瓣用户的「想看」列表，合并去重，来源用户以标签展示。
- **媒体识别**：标题变体匹配 ＋ TMDB 候选打分；匹配不上时用豆瓣条目的原名/又名重搜。
- **Emby 观影回写**：按 Emby 播放记录把条目在豆瓣标记为「看过 / 在看」。
- **CookieCloud**：可直接读取 dian115 内置的 CookieCloud 同步豆瓣 Cookie。
- **配置备份与恢复**：设置页一键「导出配置」（完整配置存成 JSON 文件，含 Cookie 等凭据）与「导入配置」，重装后快速恢复。
- **仪表盘**：订阅 / 历史 / 识别结果一览；榜单卡片按设置顺序展示，快照行按「名次 / 标题 / 年份 / 评分来源 / 评分 / 订阅状态」固定列对齐，标题可左右滚动，悬停操作按钮固定在最右。支持清理历史与黑名单。

### 安装

两种方式任选：

1. **自定义插件仓库（推荐）**：在 dian115 插件中心 → 管理仓库 → 添加仓库，索引地址填 **raw 地址**（`blob` 页面宿主解析不了）：

   ```
   https://raw.githubusercontent.com/oOStanOo/dian115-plugins/main/plugin-market/index.json
   ```

   宿主会读取该索引并列出可安装插件；发新版后点「刷新市场」再点插件的「更新」即可原地升级。

2. **手动安装/更新**：从 [Releases](https://github.com/oOStanOo/dian115-plugins/releases) 下载 **带 release_id 文件名的正式包**，在插件中心 → 用户插件 → 卡片「管理」→ 手动更新（上传文件或填下载地址）。
   注意：源码调试包（如 `douban115-2.0.5.dian115p`）只能由管理员导入作本机调试，不能覆盖正式安装，商店/URL 更新会被宿主拒绝。

### 校验

```
shasum -a 256 douban115-<version>.dian115p
```

与 `plugin-market/index.json` 中 `sha256` 及 Release 说明里的值比对。

### 版本

| 版本 | 文件 | SHA-256 |
|---|---|---|
| **2.0.7** | `douban115-0450a393-3866-43c7-a1f5-fc7e5fbb5ca4.dian115p` | `599c9e06dbbb354db391efbdeda79246c5156a4fe15ab35afcce04142c184546` |
| 2.0.6 | `douban115-f7fe4342-4154-4b42-a2ce-07d985331a95.dian115p` | `b43919e5b496bb59842a8486ac1bec8fdb3587e06893b36ba875cf2e23b6d89d` |
| 2.0.5（勿装，UI 资源路径问题） | `douban115-34d544f7-3c06-493a-8658-27dca2f1ee8b.dian115p` | `c013a6481390e768c66967059b26919e908b161d7b687c9d2bea9b7f5536c18b` |
| 2.0.4 | `douban115-2.0.4.dian115p` | `cba1c224a63dd1ab6e1ab08b23cd4287d2c26679bfad796f069e837d1ab88fbb` |
| 2.0.3 | `douban115-2.0.3.dian115p` | `7e37ba7daf049a92efdced53e5e1d788247659c2f2fc115c406d721bebad75de` |
| 2.0.2 | `douban115-2.0.2.dian115p` | `56e89497834fe43eb2c784429c02439fe1676702176020050d7474e6bf831dd3` |
| 2.0.1 | `douban115-2.0.1.dian115p` | `12258753a0f6a7b67674241df68454bf936d70193d51c1760b4eea28bbe5b52b` |

以下为 dian115 4.x 用的旧版（`.d115p` / WASM），5.x 不再可用：

| 版本 | 文件 | SHA-256 |
|---|---|---|
| 1.14.0 | `douban115-1.14.0.d115p` | `ff6d809ba1d71f5ee04426eab8a979748f881417b734dc694eb364bda0e4317c` |
| 1.14.0 | `douban115-1.14.0.d115p` | `8506b61a6e283b7673d072e56f4755295a3b525ffe79881195939a8f94c8e7a2` |
| 1.14.0 | `douban115-1.14.0.d115p` | `ff1a73f42e205d7031b93c0ac7414eca532c077083d0d320a143698cbfbcfd1f` |
| 1.14.0 | `douban115-1.14.0.d115p` | `29a82f4c47d4a87363bedd84b82df25edc0893dda6cbd3c7a45e8db198038bcf` |
| 1.13.6 | `douban115-1.13.6.d115p` | `c30aece4c4fe06f67a75adf2fd01e56f74054aaa96331c0a0fd8ada7feb8bbd2` |
| 1.13.5 | `douban115-1.13.5.d115p` | `df8c462a98deb0e26758abd421ff31d1723fe0c9c1d77addf47798ba43b63874` |
| 1.13.4 | `douban115-1.13.4.d115p` | `52c1ee0ba7559973ab291606fd0b60c3511f560b06776941eb33b61e96614b43` |
| 1.13.3 | `douban115-1.13.3.d115p` | `cdcd6f5f14af5f618926f3ca7df356f742c72c8f1a8518ba241fb06522497ec0` |
| 1.13.2 | `douban115-1.13.2.d115p` | `1b2ae7c4ca65ed1fb4178b48e465e8f37b9e80d868536c1afaa4cbf0435baa17` |
| 1.13.2 | `douban115-1.13.2.d115p` | `63f9c002a6022db9f73e4bfd578bd3ca0c6b12000b179229ec832e9ecb66f397` |
| 1.13.1 | `douban115-1.13.1.d115p` | `60a578a220edd8b42630b100dad380a9d4fadd70459318522c58f7202c8b23e2` |
| 1.13.0 | `douban115-1.13.0.d115p` | `ad4f30389afe7cb8495e077abcff299e6d669d8dcf94d35ae43fb4526137db9f` |
| 1.12.0 | `douban115-1.12.0.d115p` | `99577b35bd8908aba3d2f640f04d9f7bbe46bef7a65606edd49bbabb79719218` |
| 1.11.0 | `douban115-1.11.0.d115p` | `752a817a9448a408c7191e157e0c9d7d97860bde05e90503b9d04ccab1e0ced3` |
| 1.10.3 | `douban115-1.10.3.d115p` | `efd25ebcba36b8ffd5fce32cf46b75e2959fef94454635c8219d596980e70c36` |
| 1.10.2 | `douban115-1.10.2.d115p` | `a7e04ad99fe97440847d634d0e27074f6c769c9ff231ecd1047c0e96e0130ba0` |
| 1.10.1 | `douban115-1.10.1.d115p` | `a32f71f774f9926f5c1e6bc1ca9913a87dc7f66fe0aa326501e507a666ee9367` |
| 1.10.0 | `douban115-1.10.0.d115p` | `f08167816e6a76aadb30692d498dbda11d120a22f4a02e39c4b419411b1f50ae` |
| 1.9.0 | `douban115-1.9.0.d115p` | `386ec35ff135193384fb3dbc6eee17c3606a1afb066fce099ee0623a49958bb6` |
| 1.8.1 | `douban115-1.8.1.d115p` | `d44089019f38b8c38d46874009c502d53499a7b58bd9f57fb0aac328048b7541` |
| 1.8.0 | `douban115-1.8.0.d115p` | `1d67802d9bbdb997335164dabfb0ae97e4eeba2ed11ecaaca03a99da7c9e6058` |
| 1.7.0 | `douban115-1.7.0.d115p` | `eb003cd5220741e6c38e4627f3a6bdaa108b5f9704e61f91b77366db596d2274` |
| 1.6.0 | `douban115-1.6.0.d115p` | `d30c67c4803ffa4dfa52d6ff7c064511ddca476ce8ea3123498b8823ac5544bf` |
| 1.5.11 | `douban115-1.5.11.d115p` | `7b8d004d037201f5723e26a4ae8de423cc08a7e94ca0ca2291418f05da61546c` |
| 1.5.7 | `douban115-1.5.7.d115p` | `f3278c6fd60240e10c1bfb3d3a5191d01374253ee0725d04c9945eab6fe9cd04` |
| 1.5.6 | `douban115-1.5.6.d115p` | `403873de13c396dee7e79d129d7c57bb425595306556f18138c18b25bc09ee8b` |
| 1.5.5 | `douban115-1.5.5.d115p` | `ebc8c94e077b4e73f2661c4285d68c5dd00514a2542168da388da41ab7a482c8` |
| 1.5.4 | `douban115-1.5.4.d115p` | `718dd7a45d6a94075b15c71489925a8520b90ad3d8bcc9d4e13b786c8e8acf62` |
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
