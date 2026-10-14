# LotusWallet Downloads

LotusWallet Android 客户端的**唯一官方下载入口**。

> ⚠️ 请只从本仓库下载。我们不会通过任何聊天工具、群文件或第三方网盘分发安装包。

---

## 下载最新版

**最新版本：3.0.3（2026-10-14）**

| | |
| --- | --- |
| 下载页（推荐） | <https://github.com/LotusWallet/download/releases/latest> |
| 直链（永远指向最新版） | <https://github.com/LotusWallet/download/releases/latest/download/LotusWallet.apk> |
| 指定版本 | <https://github.com/LotusWallet/download/releases/download/v3.0.3/LotusWallet-v3.0.3.apk> |
| 网页版下载页 | <https://lotuswallet.github.io/download/> |

安装：下载 APK → 在系统设置里允许「安装未知来源应用」→ 打开安装。
首次启动会要求设置主密码，**没有账号、没有注册**。

### 校验下载完整性（可选但推荐）

```bash
# Linux / macOS
shasum -a 256 LotusWallet-v3.0.3.apk

# Windows PowerShell
Get-FileHash .\LotusWallet-v3.0.3.apk -Algorithm SHA256
```

结果与 `versions.json` 里该版本的 `sha256` 对比即可。所有版本的大小与校验值都记录
在该文件里，它是**机器可读的版本清单**：App 的「检查更新」也是读它。

---

## 版本要求

| 项目 | 要求 |
| --- | --- |
| Android 版本 | 8.0（API 26）及以上 |
| 安装包 ID | `com.lotuswallet.app` |
| 架构 | 通用（arm64-v8a / armeabi-v7a / x86_64） |
| 签名 | 见下 |

### 关于签名与升级

APK 用 LotusWallet 的发布密钥签名，**每次发布都用同一把密钥**。
一旦换了密钥，老用户无法覆盖安装（只能卸载重装，而卸载会清掉本地数据）。

> 3.x 是完全重写，与 2.x 之间没有兼容性承诺：包名、签名、本地数据格式都不继承。
> 如果你是从旧版过来的用户，请先导出旧版里需要保留的内容，再安装 3.x。

---

## 版本历史

新版本的更新说明在 [`CHANGELOG.md`](CHANGELOG.md)，或直接看对应的 Release 页面。

| 版本 | 时间 | 说明 |
| --- | --- | --- |
| **3.0.3** | 2026-10-14 | 新增 8 条非 EVM 链（共支持 49 条）；「链管理」可自行增删改；市场板块头部可折叠、DApp 清单改为远端拉取；修 4 处缺陷 |
| 3.0.2 | 2026-10-13 | **全新重写**：Kotlin + Compose，多链（BTC / EVM / TRON），保留加密信息管理与 OTP |
| 2.5.1 | 2023-10-01 | 界面与交互细节优化 |
| 2.5.0 | 2023-09-18 | UI 微调，修复 Gas 显示问题 |
| 2.4.1 | 2023-02-07 | 新增 Bitgert 链支持 |
| 2.4.0 | 2022-11-26 | 交互信息调整；证书切换优化 |
| 2.3.8 | 2022-10-22 | 推荐奖励展示调整；为接入更多 EVM 链做准备 |
| 2.3.6 | 2022-08-08 | 文案调整 |
| 2.3.1 | 2022-06-01 | 修 bug |
| 2.3.0 | 2022-05-29 | 新增 KCC 链支持 |
| 2.2.11 | 2022-05-21 | 更多 DApp 支持细节，修复部分 UI 问题 |
| 2.2.10 | 2022-04-17 | 修 bug，增加更多代币兼容 |
| 2.2.9 | 2022-04-03 | UI 优化 |
| 2.2.8 | 2022-03-08 | 版本优化 |
| 2.2.7 | 2022-02-24 | 改善体验，修复若干 bug |
| 1.9.0 | 2021-11-29 | 新增更多 EVM 链 |
| 1.0.0 | 2021-08-14 | 首个公开版本：钱包、密文、理财、OTP、密码生成器 |

2.x 的安装包仍保留在本仓库根目录（`app-release2.5.1.apk` 等），文件名与旧版一致，
方便老用户回装。**2.x 已停止维护。**

---

## 这个仓库怎么组织的

```
download/
├── README.md          ← 你正在看的文件：下载入口
├── CHANGELOG.md       ← 完整更新日志（每个版本的改动）
├── versions.json      ← 机器可读版本清单（App「检查更新」读它）
├── index.html         ← GitHub Pages 下载页
├── *.apk              ← 2.x 时代的安装包，保留不动
└── .nojekyll
```

**出于稳定性考虑，3.x 的安装包不放仓库里，而是挂在 GitHub Releases 上**：

- git 会永久保存每一个版本的文件，反复提交二进制会让仓库无限膨胀；
- Releases 有独立的 CDN 与下载统计，且能提供一个「永远指向最新版」的固定链接；
- Release 页面的说明正好就是那个版本的更新日志。

发布新版本请走 `lotuswallet-android` 仓库的 `tools/release.py`，它会构建、算校验值、
更新本仓库的 `versions.json` 并调用 `gh release create` 上传。**不要手动往这里扔 APK。**

---

## 常见问题

**装不上 / 提示「应用未安装」**
先确认下载完整（比对 sha256），再确认已允许安装未知来源应用。
如果之前装过 2.x，3.x 是另一个包名，可以共存。

**杀毒软件报毒**
钱包类应用被启发式规则误报很常见。请核对 sha256 与 `versions.json` 是否一致。

**想用测试网**
设置 → 关于 → 显示测试网（默认关闭）。测试网只用于开发验证，不要往里转真实资产。

---

## 关于安全

本仓库只分发编译产物，**不包含任何用户数据**。App 没有账号体系，所有私钥、助记词、
密文、OTP 密钥都只以密文形式保存在你自己的设备上，服务端不存在，也没有任何上传通道。

源码：<https://github.com/LotusWallet/lotuswallet-android>
公共数据（链清单 / DApp 清单）：<https://github.com/LotusWallet/assets>
