🌤 FreeCloud 自动续期脚本
本项目基于 GitHub Actions 自动运行 JS 脚本，用于定时登录 FreeCloud，自动完成端口续费任务。

✨ 功能简介
- ✅ 自动登录 FreeCloud
- ✅ 自动续费指定端口
- ✅ 每 4 天自动运行一次，也支持手动触发
- ✅ 支持自定义账户信息（通过 GitHub Secrets 管理）

🧰 使用前提
- 你需要有一个 FreeCloud 账户，并至少有一个激活的服务。

你需要知道你的：
- 登录账号（用户名）
- 密码
- 端口 ID（在 FreeCloud 控制台中能看到，例如：12345）
- 单个账号用renew.js(默认) 多个账号使用raw_renew.js(在renew.yml中将node renew.js改为node raw_renew.js)

🚀 快速开始
1️⃣ Fork 本仓库
点击右上角的 Fork，将此仓库复制到你自己的 GitHub 账户。

2️⃣ 配置 GitHub Secrets<br>
- 前往你的 Fork 仓库：
- 进入 Settings → Secrets and variables → Actions → 点击 New repository secret
- 添加以下 3 个变量（名字必须一致）：

| Secret 名称       | 示例值                | 描述         |
| --------------- | ------------------ | ---------- |
| `FC_USERNAME`   | `user@example.com` | 登录用户名      |
| `FC_PASSWORD`   | `mypassword123`    | 登录密码       |
| `FC_MACHINE_ID` | `12345`            | 服务的端口或机器编号 |
| `TG_BOT_TOKEN`(可选) | `12345`            | Telegram 机器人 token |
| `TG_CHAT_ID`(可选) | `12345`            | Telegram 你的 chat ID |
| `FC_ACCOUNTS`(可选) | `[{"username": "user@example.com","password": "mypassword123","machines": [1234,4566]},{"username": "user@example.com","password": "mypassword123","machines": [1234]}]`            | 多个账号登录续费 |

3️⃣ 启用 GitHub Actions
- 点击仓库上方的 Actions 标签页
- 选择左边的 续费 工作流
- 点击右侧的 Run workflow 可手动执行任务，首次建议手动运行一次
- 系统会每 4 天自动运行一次

📂 项目结构说明
.
├── .github/workflows/
│   └── renew.yml         # GitHub Actions 工作流配置
├── renew.js              # 自动续费主程序（JS 编写）
├── README.md             # 本说明文档
🛠 技术栈
- Node.js
- GitHub Actions
- node-fetch

❓常见问题
Q1: 我的端口 ID 哪里看？

登录 FreeCloud 控制台，点击你购买的服务，URL 中类似 /server/detail/12345 中的数字 12345 就是端口 ID。

Q2: GitHub Actions 运行失败怎么办？

请点击失败任务查看日志，常见原因包括账号或密码错误、端口号错误、网络问题等。

Q3: 为什么输出 "Just a moment..." 页面？

有可能是 Cloudflare 验证页面导致暂时无法续期。可尝试使用 Workers 服务绕过（此项目已内置 cloudflare bypass 的接口）。

❤️ 鸣谢
感谢：

FreeCloud 提供免费服务

Cloudflare Workers

GitHub Actions 自动化平台
