# issueLogUpdate

「@记录助手（issueLog）」的**自动更新发布仓**：这里只存放每次发版的产物，源码与开发文档不在本仓库。

客户端（`IssueLog.exe`）启动后会静默检查本仓库的最新 release，发现新版本时按需下载其中一个包；本页的文件也都可以直接下载手动使用。

## 每个 release 的资产

| 资产 | 内容 | 体积（实测） | 什么时候用 |
|---|---|---|---|
| `issue-log-<版本>-full.zip` | 全部程序文件 + `node.exe`、`node_modules`、WebView2 DLL | 约 40 MB | 新机器，或本机运行时内容与清单不一致 |
| `issue-log-<版本>-update.zip` | 混淆后的程序文件、页面与 `IssueLog.exe`，不含运行时 | 约 200 KB | 本机运行时一致的常规更新 |
| `update-manifest.json` | 版本、逐文件大小与 SHA-256、两个包的指纹 | 约 0.5 MB | 客户端比对用；手动更新时不需要选它 |

- 客户端**一次只下载其中一个包**：逐个比较本地运行时文件的大小与 SHA-256，一致就下更新包，不一致才下完整包；不比较文件修改时间。
- 两个包内都带 `package-manifest.json`，手动更新时只需选 ZIP，不用另外挑清单。
- 包内只有程序文件，不会覆盖 `records.xlsx`、`settings.json`、`memo-data.json`、`timelog-data.json`、`memo-images/`、`reply-images/` 和窗口状态文件等本地数据。
- 下载后会先校验整包 sha256，再逐文件校验，并拒绝清单之外的文件与路径穿越；全部通过才落到 `update/pending/`。

## 怎么用

- **常规更新**：程序自己检查 → 提示条点「立即更新」→ 下载校验 → 重启应用；也可以在「设置 → 关于」里手动检查并查看更新内容。
- **手动更新**：下载本页任一 ZIP，在「设置 → 关于 → 手动更新」里选中它。
- **全新机器**：下载 `-full.zip` 解压到任意目录，双击 `IssueLog.exe` 即可，不需要另装 Node.js；已有数据想沿用，把原来的 `records.xlsx` 等文件复制进去。

## 说明

- 本仓库必须保持**公开**：客户端不携带任何凭据。
- release 由源码仓的 `npm run release:publish` 创建，资产与清单全部由脚本生成；请勿手工改动或删除其中的文件，否则客户端会校验失败。
- 刚发版时 `releases/latest/download/` 受 GitHub CDN 缓存影响，客户端通常要等几十秒到几分钟才看到新版本，这属正常现象。
