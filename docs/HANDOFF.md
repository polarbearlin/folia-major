# 交接文档：music.topsiai.com（Folia fork）

> 写给接手这个仓库的新会话。2026-10-31 由上一个会话整理。项目规则以 `AGENTS.md` 为准，这里只记“这个 fork 发生过什么、下一步做什么”。

## 这是什么
- 站长 Vasanti 的公开音乐播放器，基于开源项目 **Folia**（上游 `chthollyphile/folia-major`，**AGPL-3.0**）。
- 部署：Cloudflare Worker `folia-major`，自定义域名 `music.topsiai.com`。部署命令和变量见 `DEPLOY-NOTES.md`。
- 主站（北极熊的提示词 prompts.topsiai.com，仓库 `polarbearlin/polarbear-prompts`）页脚和手机菜单里有「音乐」入口指向这里。

## 已完成
1. **网易云**：接口在 Vercel（`folia-netease-api-lppppoi`，香港区），已加 `ENABLE_RANDOM_CN_IP=true` 解决海外 IP 拿不到播放链接的问题。会员歌未登录只能试听 30 秒；站长已用自己的会员账号在播放器里扫码登录。
2. **跳过首次启动引导**：新增 `VITE_SKIP_STARTUP_EXPERIENCE=true`（`src/hooks/useStartupExperienceGate.ts`，已写入 `.env.production`），已合并 main 并部署。原因：手机访客会卡在 5–6 步的引导里。
3. **QQ / 酷狗**：代码没坏。QQ 匿名搜索常被上游以 2001 拒绝（程序会自动回退匿名直连），播放需要扫码登录；酷狗取播放链接返回 20028“需要验证”，也需要扫码登录。

## 下一步（站长想做的）
1. **把界面做得“正常、好玩”**：手机首页默认是空的“无限墙”（Bravais），新用户看不懂。考虑默认改为经典网格、首页给出明显的搜索入口。
2. **更多歌词样式 / 背景**：现有 17 种样式、6 种背景（见 `src/types/visualizerModes.ts`）。可走两条路：
   - 「网页」背景（url）：任意网页当背景，零代码。
   - **mod 插件系统**：参考 `mods/sample-aurora-visualizer` 写新样式。设想做一个“冰层之下”样式：歌词冻在冰里，唱到哪句哪句的冰融化，背景是极光（主站正在做同主题的首页，原型在 `polarbear-prompts` 仓库的 `design/beneath-the-ice` 分支 `src/pages/lab/`）。
3. **页面上注明原项目出处**（AGPL）：在“关于 / 帮助”里写明基于 Folia（github.com/chthollyphile/folia-major），并链接本 fork 源码。
4. **QQ 音乐**：如登录后仍有问题，继续排查（`worker/qq.ts`、`src/services/onlineMusic/qq/`、`docs/qq-music-deployment.md`）。

## 规则（站长定的）
- 改动先放分支；**合并 main 和部署前要站长本人在对话里确认**。
- 不花钱；不动根域名 topsiai.com 的邮件记录；加子域名 DNS 前先说。
- 本会话没有 Cloudflare / Vercel 权限：部署和改 Vercel 环境变量交给 **Grok Bot**（在 `polarbearlin/polarbear-prompts` 的 Issue #2 里用 `[Claude→Grok]` 开头留言，它用 `[Grok→Claude]` 回复）。
- 网易云 / QQ / 酷狗是非官方逆向接口，公开播放有版权和封号风险，站长已知情并决定启用。
- 和站长沟通用中文，少用术语。
