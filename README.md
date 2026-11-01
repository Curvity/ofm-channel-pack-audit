# 01 · Issue 发布正文（2026-11-01 5.4万Star 终审完全体定稿）

## 📋 主贴标题（复制填入 Issue Title）

```plaintext
关于 vendor/channel-pack 的来源溯源、自研宣发矛盾与 76 位外部贡献者回流核查
```

---

## 📋 主贴正文（复制填入 Issue Body）

> **【公开技术审计与事实送达声明】**
> 1. **全量存证与永久授权**：本核查报告及配套的逐文件 SHA256 哈希比对表、可复现验证脚本、Issue/PR 统计快照已同步开源存档于独立存证仓库 **[`Curvity/ofm-channel-pack-audit`](https://github.com/Curvity/ofm-channel-pack-audit)** 及全量代码镜像仓 **[`Curvity/dsh-our-free-model-backup`](https://github.com/Curvity/dsh-our-free-model-backup)**，并以 **[CC BY 4.0](https://creativecommons.org/licenses/by/4.0/deed.zh-hans)** 协议授权任意再分发。
> 2. **独立核查说明**：本报告系基于公开 Git 提交树、构建产物与公开视频记录完成的独立开源合规核查，未向上游仓库所有者（`iJetLi`）征求授权或事先沟通；报告中的每一项结论均由客观 SHA256 哈希与 Git 历史构成，任何针对本报告的异议，仅需对照一楼脚本在代码与数据层面直接回应。
> 3. **不可逆送达告知**：本 Issue 仅作为面向开源社区与 76 位外部协作者的公开事实告知函。无论本仓库维护者选择公开回应、关闭议题还是物理删除，所有公开 Git 提交历史、代码等价性铁证与各方存证镜像均已完成不可逆固化与分发。

本仓库在主页与 6 期官方视频（累计播放 66.7 万次）中作为核心卖点宣发的「十三个白嫖渠道，一体接入」及所谓「重磅推出的桌面端独立入口与中转 API 网关」（核心源码位于 `vendor/channel-pack` 目录），其底层代码来源、Git 吸收时序、协议维护能力与对外宣发口径之间存在不可调和的事实背离。

以下为基于公开 Git 提交历史、逐文件源码哈希比对、B 站 6 期官方视频字幕与置顶自白、评论区舆情及本仓库 Issue/PR 全量记录（截至 2026-11-01 `v2.7.4` / `v2.8.0`）的核查报告。所有结论均在一楼附有完整的可复现验证脚本。

---

### 一、 代码吸收与去品牌化时序（13 小时 55 分钟完成整包搬运与改名）

1. **上游持续迭代与公开连载（2026-08-15 至 2026-11-01）**：
   上游开源项目 [`iJetLi/dsh-providers-hub`](https://github.com/iJetLi/dsh-providers-hub)（GitHub 官方主仓库，同源 Gitee 仓库 [`iJetLi/deepseek-harness-codearts`](https://gitee.com/iJetLi/deepseek-harness-codearts)）由原作者 [iJet（B 站主页 UID: 384916748）](https://space.bilibili.com/384916748) 及 30 位社区贡献者历时两个多月持续开发，逐一完成 CodeArts（华为云）、CodeBuddy、WorkBuddy、Qoder、LobsterAI、Cline、Loomy、Raccoon、ZCode、MiniMax Code、AutoClaw、Accio、OfficeAce 等十余个商业渠道的登录逆向、账号池轮巡、每日签到逻辑与本地 OpenAI 兼容网关，并在 B 站连续公开发布 23 期带有「开源：」前缀的开发实录视频：
   - **2026-08-15（首发第 1 期）**：[`BV1WHgM64Ewj`](https://www.bilibili.com/video/BV1WHgM64Ewj)《开源：新玩具 deepseek-harness codearts 登陆和模型引用插件》；
   - **2026-09-14（第 9 期，批量签到 + WorkBuddy）**：[`BV1EoY66AEKM`](https://www.bilibili.com/video/BV1EoY66AEKM)《开源：DSH 白用 Deepseek V4.1 Flash 升级：批量领取积分和国际版 WorkBuddy》；
   - **2026-09-19（第 11 期，Qoder + LobsterAI）**：[`BV1FBeb6zERT`](https://www.bilibili.com/video/BV1FBeb6zERT)《开源：DSH hub 支持 Qoder / LobsterAI》；
   - **2026-09-26（第 14/15 期，讯飞 Loomy + 商汤 Raccoon）**：[`BV1VxhD6jEv9`](https://www.bilibili.com/video/BV1VxhD6jEv9) / [`BV1PXhR65Efj`](https://www.bilibili.com/video/BV1PXhR65Efj)；
   - **2026-09-30（第 17 期，智谱 ZCode + MiniMax Code）**：[`BV1UnYF6eEk5`](https://www.bilibili.com/video/BV1UnYF6eEk5)《开源：Hub 支持 Zcode / MiniMax code / 锁定长期积分》；
   - **2026-10-02（第 19 期，本地 OpenAI 网关首发）**：[`BV1qWaS6QECY`](https://www.bilibili.com/video/BV1qWaS6QECY)《开源：Hub 加入流量徽标 + 网关 + opencode provider》；
   - **2026-10-18（第 23 期，正式上架 GitHub 与插件市场）**：[`BV1gLng6vEns`](https://www.bilibili.com/video/BV1gLng6vEns)《开源：Hub上架dshmarket和github 更新澳龙/魔塔/minimax国际站/非临期聚合》。
2. **上游合并基准提交（2026-10-06 02:14:52 +0800）**：
   上游仓库合并 PR !59，生成提交 `345f0a07b22713c0ae189ca7d8b97ec4f64626c6`（作者 Jet）。
3. **本仓整包吸收（2026-10-06 16:10:01 +0800，相隔 13 小时 55 分钟）**：
   本仓库推送 Commit `fba1eb2`（`feat: absorb the free-channel pack (jet-hub) ... 2.0.0`），将上游 `src/` 整包拷入本仓，并在同日 15:10 推送 v2.0.0 公告宣称「一次性接入十三个账号渠道」。
4. **抹除上游品牌代号（2026-10-07 13:14:19 +0800）**：
   本仓库推送 Commit `7bc8068`（`refactor: the vendored channel pack loses its upstream codename`），将目录与内部标识符中的 `jet-hub` 批量替换为 `channel-pack`。该提交信息原文记录如下：
   > `vendor/jet-hub becomes vendor/channel-pack; the RPC mount, store, identifiers, locales and every path reference follow, and pack.js is rebuilt from the renamed sources (same pinned build deps). The upstream attribution stays in vendor/channel-pack/NOTICE.md with its repository link and MIT license; only the brand name is gone.`
5. **未清理干净的上游工程残留与前端照搬**：
   即便执行了上述去品牌化提交，本仓库内部仍长期残留多处未改净的上游标识与机械照搬痕迹：
   - `vendor/channel-pack/package.json` 第 2 行包名仍为 `"name": "dsh-codearts-auth"`；
   - `vendor/channel-pack/src/index.ts` 导出名仍为 `export const name = 'codearts-auth'`，且多处日志前缀仍硬编码着 `[codearts-auth]`；
   - 前端文件 `client.js` 中的 13 个渠道卡片元数据定义及积分能力门控矩阵（`claim: true`、`unit: 'dollars'`、`unit: 'tokens'` 等），亦直接复制映射自上游 `plugin-src/client/credits-capabilities.js`。

---

### 二、 逐文件源码比对结果：吸收基线 130 / 141 个文件逻辑一字未改

按本仓库 `vendor/channel-pack/NOTICE.md` 第 11 行指认的上游基准提交 `345f0a07` 导出 `src/` 快照，与本仓库吸收基线 `vendor/channel-pack/src/` 下的同名文件（共 141 个）进行去 BOM 与行尾 LF 归一化比对：

| 比对层级 | 文件数量 / 占比 | 具体技术事实 |
| :--- | :--- | :--- |
| **层级 1：仅还原 6 组代码标识符** | **85 / 141 (60.3%)** | 仅将 `channel-pack` / `ChannelPack` / `CHANNEL_PACK` / `channelPack` 等代码标识符还原为 `jet-hub` 对应形式，即与上游 `345f0a07` 逐字节完全一致（含 66 个连标识符都未改动的纯拷贝文件及 `backup.ts` 等 19 个标识符替换文件） |
| **层级 2：还原带空格的品牌文案** | **+45 / 141 (31.9%)** | 另有 45 个文件（含 `account-pool.ts`、`buddy.ts`、`login.ts`、`product.ts`、`llm-adapter.ts`、`qoder.ts`、`trae.ts` 等）代码逻辑与上游 100% 相同，唯一差异仅是将注释或报错提示语中带空格的 `"Jet Hub"` 替换为 `"Channel Pack"` |
| **合计：代码逻辑逐字节完全等价** | **130 / 141 (92.2%)** | **上述两项合计 130 个核心渠道与网关文件（外加二进制 `qoder-auth-wasm.wasm`），本仓库在吸收时未做一字逻辑修改** |
| **存在代码逻辑改动的同名文件** | **11 / 141 (7.8%)** | 在吸收基线剩余 11 个文件中，6 个属于本仓声明「默认停用」的 OpenCode 车道（`index.ts`、`opencode*.ts`）；其余 5 个文件（`gemini-adapter.ts`、`gemini-auth.ts`、`llm-register-compat.ts`、`openai-compat.ts`、`types.ts`）在整个代码库中合计仅改动 **+24 / -5 行** |
| **13 个账号渠道与本地网关本仓独立新增实现** | **0 行 (0.0%)** | 除将 `jet-hub-rpc.ts` / `jet-hub-store.ts` 改名为 `channel-pack-rpc.ts`（相似度 0.9925）/ `channel-pack-store.ts`（相似度 0.9773）并抽出 `channel-fetch.ts` 外，13 个渠道与本地 OpenAI 网关的核心逆向及业务逻辑无一行本仓原创代码 |

---

### 三、 从「自称团队研发 13 渠道」到「自爆 3–4 人学生团队、无力维护而删渠道」的宣发破产闭环

1. **以 Star 数量绑定号池配额，但自有 EAC 与免费车道长期崩溃**：
   本仓库将自有 EAC 协付车道设为「必须使用 GitHub 登录 + 已 Star 本仓库」方可获取令牌（见 `README.md` 第 627 行），客户端界面直接展示配额公式 `pool.formula: 'Star {stars} × 1.5'`，维护者 `Nefert-zx` 在官方视频（`BV1y5h16EE1r`、`BV1y4Hj6LEfA`、`BV1ZwHD68E3m`、`BV1umpj6RETg`、`BV1Qdng6TE5o`）及置顶评论中反复号召：**「号池号的数量是按 star 数 x1.5 来配置的，所以各位懂我意思吧，为了大家更好的体验，点点star吧」「不要白嫖啊，去点点 star」**。
   然而在实际运行中，本仓自有的 EAC 车道与免费车道长期处于高故障率与瘫痪状态：
   - **视频评论区实测舆情**：6 个官方视频（累计播放 667,745 次、总评论 4,589 条）已抓取的近 3,000 条评论中，超 **350 条（占比逾 12%）** 集中反馈卡死、超时、502 报错及无法调用（例如高赞评论 `@骛过-` 71 赞反馈「已经给我卡成傻福了，发个你好，回复五分钟」，`@poeso` 48 赞实测 6 个模型超时 >170s 直斥「骗star来的」，`@莫得感情の憨包饿龙` 反馈「骗star的，免费模型，eac全部卡的用不了，都不解决还在宣传」）；
   - **维护者公开承认号池枯竭**：在 2026-10-31 第 6 期视频（[`BV1ZNx16oES6`](https://www.bilibili.com/video/BV1ZNx16oES6)）置顶长评中，维护者终于承认：**「EAC渠道和oc渠道都在抢修中……不过号的数量只有 100 多个，估计很快就会打空」**——54,600+ 个按 `Star × 1.5` 公式承诺的 Star 背后，真实号池仅有 100 多个账号。

2. **前期高调冒领「我们团队研发」，后期风控变更无力维护只能「直接删除渠道」**：
   在自有车道难以支撑可用性的背景下，本仓库将整包拷自上游的 13 个渠道与本地网关推向前台充当核心卖点，却在用户可见处彻底抹除来源，并在近期暴露了毫无底层维护能力的真相：
   - **用户可见处 0 署名与双重标准**：在 `README.md`、`README_EN.md`、`PACKAGING.md`、`client.js`、`index.js` 中检索 `iJetLi`、`dsh-providers-hub`、`deepseek-harness-codearts` 或 `gitee`，命中次数全部为 **0**（仅藏于用户从不翻阅的 `vendor/channel-pack/NOTICE.md`）。而同一份 `README.md` 第 266、280 行却明确为 `free-claude-code` 与 `9router` 署了名，唯独对提供 130 个核心文件的上游仓库进行选择性隐匿。
   - **视频原声连环冒领**：
     - **2026-10-08**（吸收上游代码仅两天后），视频 [`BV1ZwHD68E3m`](https://www.bilibili.com/video/BV1ZwHD68E3m) 宣称：**「以及我们更新了能接入其他渠道模型以及自动每日签到，work buddy、qoder、trae 和 zcode 等渠道都可以接入，现在还支持一键签到账号，实时查看积分面板，一键切换账号轮巡防风控等功能」**；
     - **2026-10-11**（34.4 万播放爆款视频），视频 [`BV1umpj6RETg`](https://www.bilibili.com/video/BV1umpj6RETg) 宣称：**「今天我们团队研发出了最新的插件，就叫 our free model……13 个白嫖渠道，每天帮你寻一遍当月额度，一键收进口袋」**；
     - **2026-10-18**（与上游原作者发布 [`BV1gLng6vEns`](https://www.bilibili.com/video/BV1gLng6vEns) 宣布上架 GitHub 同日），视频 [`BV1Qdng6TE5o`](https://www.bilibili.com/video/BV1Qdng6TE5o) 宣称：**「OFM 又升级了。这次我们重磅推出桌面端能进 agent。以前是 DSH 专属，现在有独立入口了，像配中转一样，拿地址和 key 就能接……最后也请各位多点点 star……这就是我们的 OFM」**——该网关实为 10-06 随包拷入的上游 `src/openai-gateway/` 模块（15 个文件中 12 个逐字节完全一致）。
   - **2026-10-31 最新视频自爆真实人力与「删渠道」实证（最致命的工程证伪）**：
     在 2026-10-31 发布的第 6 期视频 [`BV1ZNx16oES6`](https://www.bilibili.com/video/BV1ZNx16oES6) 及置顶长评中，面对海量故障质疑，维护者首次公开自白：
     > **「说实话 up 也是高中生，我们团队总共就 3-4 个人，最大的都还在上大学，那个广告也就满足我们服务器的钱，每周划去服务器的💰我能拿到……」**
     > **「work buddy 和华为云被移除了喵，上游风控封掉了😭」**（对应代码库 `vendor/channel-pack/src/` 文件数从 141 个被删减至 136 个）。
     
     这两句自白直接构成了对本仓库「自研」宣发的终极证伪：
     1. **人力与工程量完全不匹配**：一个仅由 3–4 名在校学生组成的团队，从未编写过 `vendor/channel-pack` 中那 130 个涵盖 13 家大厂逆向协议、OAuth 握手、WASM 签名与本地 OpenAI 网关的复杂文件——那是上游原作者 Jet 与 30 位社区开发者历时两个多月、连载 23 期开源视频积累的工程成果。
     2. **真假研发团队的试金石**：当腾讯 WorkBuddy 与华为云 CodeArts 调整接口风控时，真正掌握底层协议的上游仓库 [`iJetLi/dsh-providers-hub`](https://github.com/iJetLi/dsh-providers-hub) 早在两周前即通过 PR `!104` / `!105` / `!109` 完成了会话双闸门与 400/11140 状态码适配，至今稳定运行；而本仓库因为只是整包搬运、根本不具备底层协议逆向与维护能力，一旦拷来的旧代码遇到风控变更，唯一的手段就是在 `v2.7` 中将 WorkBuddy 和华为云直接从代码库里物理删除！
     3. **商业变现与责任豁免的双重标准**：在顺风期收割 **54,617 个 Star**、**66.8 万视频播放**及**商业广告收益**（「每周划去服务器的💰我能拿到」）时，对外高调自称「我们团队研发出了最新插件」「我们重磅推出」；一旦代码失修崩盘、遭遇社区追责，便搬出「高中生 / 3–4 人学生团队」身份寻求舆论豁免。学生身份绝不是抹除 30 位开源作者署名、将他人心血据为己有并用于广告引流变现的挡箭牌。

---

### 四、 零上游回馈、单向死胡同分叉与 76 位外部贡献者的精力截留

凭借上述宣发裂变，本仓库在短短两周内暴涨至 **54,617 个 Star** 与 **1,497 个 Fork**（连跳多个版本号至 `v2.7.4` / `v2.8.0`），但在开源协作链条的上下游两端均造成了严重的生态撕裂：

1. **对上游零回馈，基线永久冻结于 10-06 并沦为劣化分叉（等价率跌至 55/141）**：
   - 上游 GitHub 与 Gitee 仓库现有的百余条 Issue、PR 及 30 位 Commit 作者中，来自本仓库维护者任何身份（`Ebony-Vinyl` / `zixin947` / `zouyuxuan` / `Nefert`）的贡献记录为 **0**。
   - 本仓库 `vendor/channel-pack/NOTICE.md` 至今钉死在 `345f0a07`（2026-10-06）。三方逐文件比对显示：在 10-18（141 文件口径）下，本仓相对 10-06 旧基线等价率为 **119/141（84.4%）**，而相对上游最新主线（`origin/master`）等价率暴跌至 **55/141（39.0%）**；在 10-31 删去华为云与 WorkBuddy 渠道后（136 文件口径），在 `v2.7.4`/`v2.8.0` 下相对上游最新主线（127 同名文件）等价率进一步劣化为 **49/127（38.6%）**；偏离的文件中，**0 行代码源自 10-06 之后的上游新版**。
   - 上游在 10-06 之后新增的阿里 `Accio`（全套 4 个文件）、`AutoClaw`（全套 6 个文件）、跨链路聚合（全套 4 个文件）、华为果办 `OfficeAce`、MiniMax 国际站、澳龙、魔塔等全新渠道与 160+ 项缺陷修复，本仓库一个都没有。甚至当本仓用户在 Issue `#362` / `#396` 发帖苦求「能否加入 autoclaw / 华为果办 OfficeAce 的反代」时，维护者束手无策——而这些渠道早在上游主线开发完毕并开源发布了第 22、23 期演示视频（[`BV18cpq62Efk`](https://www.bilibili.com/video/BV18cpq62Efk)、[`BV1gLng6vEns`](https://www.bilibili.com/video/BV1gLng6vEns)）。

2. **76 位外部贡献者沦为「影子分叉」的免费修补匠（181 个外部 PR 中 99 个未合关闭、20 个挂起、62 个被截留）**：
   截至 2026-11-01，本仓库共有 **76 位外部社区贡献者**无偿提交了 **181 个 PR**（全仓总计 275 个 PR）：
   | 维度 | 核心成员 (`Ebony-Vinyl` / `zixin947`) | 外部社区贡献者 (76 人) |
   | :--- | :---: | :---: |
   | **提交 PR 总数** | 94 个 | **181 个** |
   | **已合并 PR 数（合并率）** | 92 个 (**97.9%**) | **62 个 (34.3%)** |
   | **未合并直接关闭（废弃率）** | 2 个 (2.1%) | **99 个 (54.7%)** |
   | **至今仍被晾在 Open 状态** | 0 个 | **20 个** |

   即便本仓库近期在 `v2.7.4` 中突击合并了 19 个社区修复试图改善形象，依然无法掩盖两项残酷事实：
   - **高达 65.7%（119/181）的外部贡献被直接废弃或无限期挂起**：99 个外部 PR 未经合并即被关闭；另有 20 个外部 PR 至今仍挂在 Open 列表（例如 `@yudukongchen` 的 `#102` 已挂起 26 天，`@9376E` 修复商汤 Raccoon 与讯飞 Loomy 额度用尽不切号的 `#383` 已挂起 16 天，`@R227BOUT` 的 `#459`、`@Shen-18` 的 `#511`、`@KoishiMint` 的 `#514` 等均未合入），而此前诸多反应渠道故障与质疑的 Issue（如 `#702`、`#706`、`#708`、`#713`）则被直接批量关闭。
   - **被合入的 62 个外部 PR，本质是欺瞒不知情开发者替被盗旧代码「重复造轮子」**：
     无论是在 `v2.7.4` 中被合入的 `@coco`（`#610` `fix(gateway): 修复工具结果消息并兼容新旧 DSH 内核`）、`@在虎`（`#650` `fix(channel-pack): 给 ChannelNetworkError 补上 code`、`PR #658 修复 Issue #549`）、`@menghuanshiguang`（27 次提交，曾连续提 `#127`–`#136` 十一条审计指出 `vendor/channel-pack` 是整仓拷贝的影子仓库、包名仍停留在 `dsh-codearts-auth`），还是曾为被盗网关与渠道提交补丁的 `@spearzificial`（`#310`、`#520`、`#521`、`#525`）、`@baojingyu`（`#513` 修复被盗 `openai-gateway` 工具调用）、`@orchie`（`#526`）、`@CaiYan12`（`#518`、`#524`）、`@startuo`（`#377`、`#512`）、`@Gyl1219`（`#126`），这 **76 位外部贡献者**都是在不知道真实上游存在的情况下，为一个抹去原作者名字、落后上游数百个 Commit、遇到风控只会删渠道的死胡同分叉无偿打工，而他们的修复成果没有一行能够回流到真实主线。

---

### 五、 致全体 76 位外部贡献者与报障用户的真实上游直通指引（GitHub 同平台官方主仓已开启）

正如本仓第 6 期视频评论区已有觉醒用户公开指出的那样（「*你们家自维护的通道使用体验太差了，如果只是要用聚合的话，还不如就退回去用更轻量的 Jethub*」），如果你正在为上述商业账号渠道、本地 OpenAI 兼容网关排查故障或编写修复 PR，**无需跨平台，即可直接在 GitHub 官方上游仓库使用完整功能并提交贡献**：

- **GitHub 官方上游主仓库（首选，同平台零门槛）**：**[`https://github.com/iJetLi/dsh-providers-hub`](https://github.com/iJetLi/dsh-providers-hub)**
- **Gitee 官方同源主仓库**：**[`https://gitee.com/iJetLi/deepseek-harness-codearts`](https://gitee.com/iJetLi/deepseek-harness-codearts)**
- **上游作者 B 站技术主页（23 期开源开发实录）**：**[`https://space.bilibili.com/384916748`](https://space.bilibili.com/384916748)**（最新第 23 期上架 GitHub 官宣视频：[`BV1gLng6vEns`](https://www.bilibili.com/video/BV1gLng6vEns)）
- **上游维护现状（WorkBuddy 与华为云 CodeArts 均正常可用）**：由原作者 Jet 及社区核心协作者持续高频维护（领先本仓 10-06 影子基线逾 **300 个 Commit**，原作者在 B 站技术视频评论区亲自回复解答技术问题逾 440 条）。**在本仓库 `v2.7` 中因无力维护而被直接删除的腾讯 WorkBuddy 与华为云 CodeArts 渠道，在上游官方仓库中（Gitee 镜像仓主线 PR !104 / !105 / !109，提交 `b554b73`、`42b90f7`）早在 10-16~10-17 即已合入同类双闸门风控修复并稳定运行至今**，且上游已额外上线阿里 Accio、华为果办 OfficeAce、AutoClaw、MiniMax 国际站、澳龙、魔塔、非临期聚合等全套新渠道。
- **贡献迁移指引**：参与过本仓 PR 的 76 位外部贡献者（如 `@menghuanshiguang`、`@spearzificial`、`@coco`、`@baojingyu`、`@orchie`、`@CaiYan12`、`@DQ-Look`、`@startuo`、`@Gyl1219`、`@9376E`、`@yudukongchen`、`@R227BOUT`、`@Shen-18`、`@KoishiMint`、`@eghrhegpe`、`@LaughSmiles`、`@Alore111`、`@XiaoBinGan`、`@xuaosen13-lgtm`、`@xdr531955724` 等），你们的排障分析与补丁如果提交至上述 GitHub 官方上游 [`iJetLi/dsh-providers-hub`](https://github.com/iJetLi/dsh-providers-hub)，将直接进入真正具备逆向维护能力的活跃主线，而非消耗在一个抹除原作者署名的影子目录里。

---

### 六、 事实纠正要求

MIT 许可证赋予了复制、修改与再分发的权利，本核查报告**不主张著作权侵权**；但开源许可的底线合规，绝不赋予任何人将他人历时两个多月开发的 130 个核心渠道与网关文件抹除品牌代号后在视频中宣称为「我们团队研发」「我们重磅推出」的权利，更不能一边以「团队自研」人设收割 54,600+ Star 与广告费、一边在代码失修时以「3–4 人学生团队」推卸责任并截留 76 位外部贡献者的心血。

本仓库维护者必须正视并完成以下两项合规纠正：

1. **补齐显著位置署名并停止自研冒领**：在 `README.md`、`README_EN.md` 核心特性列表首位及客户端 `client.js` 设置页显著位置，对标同文件第 266 行 `9router` 的署名规格，明确标注「账号渠道包与本地 OpenAI 兼容网关实现源自 [`github.com/iJetLi/dsh-providers-hub`](https://github.com/iJetLi/dsh-providers-hub)（[`gitee.com/iJetLi/deepseek-harness-codearts`](https://gitee.com/iJetLi/deepseek-harness-codearts)）」，停止在视频与宣发中使用「我们团队研发」「我们重磅推出」等虚假口径。
2. **公开建立渠道与网关 Issue 上游重定向指引，停止截留外部排障劳动**：针对现有的渠道与网关故障 Issue 及外部 PR，在显著位置公开标注真实 GitHub 上游地址，引导用户与社区开发者前往具备完整维护能力的真实上游主线。
