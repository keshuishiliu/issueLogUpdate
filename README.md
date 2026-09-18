# issueLogUpdate

本仓库只用于存放 @记录助手 的自动更新产物。

每个 release 包含三个资产：

- `issue-log-<版本>.zip`：程序包（源码、页面与 IssueLog.exe），每次更新都会下载
- `issue-log-<版本>-runtime.zip`：运行时包（node.exe、node_modules 与 WebView2 DLL），仅在本地不一致时下载
- `update-manifest.json`：更新清单，客户端据此比对版本与哈希

全新机器上没有任何运行依赖时，下载程序包与运行时包解压到同一目录即可直接运行。
