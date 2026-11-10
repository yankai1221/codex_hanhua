# Codex 界面汉化脚本（备份）

`Enable-CodexI18nCache.ps1` 通过本机调试端口，把 Codex 页面里 Statsig 缓存的 `enable_i18n` 设为 `true`，让 Codex 使用官方中文界面。不改 API Key、登录信息和 Codex 安装目录。

## 来源与审核

- 原始来源：https://gitee.com/zhenglei410/codex-i18n-cache-seeder （第三方个人仓库，非本仓库作者所写）
- 本仓库保存的是 2026-11-10 下载并通读审核过的版本，**未做任何修改**
- 文件大小：26797 字节
- SHA256：`2897c281194f856a00752fa09fe80937835934448e2041278a5d49e8ce5d01d7`
- 审核结论：脚本只访问 `127.0.0.1` 本地调试端口，不外发数据，不下载其他内容
- 已验证 Codex 26.928 和 26.1103 的 `app.asar` 中都存在 `enable_i18n`（层 ID `72216192`）

## 使用

1. **完全退出 Codex**（任务栏托盘里也要退出）
2. 打开 PowerShell，运行：

```powershell
& ([scriptblock]::Create((irm https://raw.githubusercontent.com/yankai1221/codex_hanhua/main/Enable-CodexI18nCache.ps1))) -BootstrapMissing
```

3. 脚本会自动启动 Codex 并写入缓存，看到 `Statsig cache updated` 即成功
4. 再次**完全退出 Codex**，正常启动，界面即为中文

## 注意

- 只改本地缓存，Statsig 服务端刷新后可能把值改回去，界面变回英文时重新运行一次即可
- Codex 已在运行时脚本会报错，必须先完全退出
- 参数：`-Reload` 写入后直接刷新页面；`-NoLaunch` 不自动启动；`-Port` 指定端口
