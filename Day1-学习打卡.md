<img width="572" height="522" alt="89e5e58618d16e790e31c8393e0f4988" src="https://github.com/user-attachments/assets/60d7887b-8e54-499c-ad11-c00cd9c246b1" /># Day 1 学习打卡：从零部署 AgentSeek 深度研究环境

本次学习我成功在 WSL2 (Ubuntu) 环境下跑通了 AgentSeek 的 deepagents/research 项目，并成功接入 DeepSeek 模型。以下是我的踩坑与总结：

## 🛠️ 踩坑填坑记录
1. **Python 版本冲突**：Windows 下的 Python 3.14 导致 `langchain-oceanbase` 无法安装，果断迁移到 WSL2，降级使用 Python 3.12 后解决。
2. **数据库限制**：项目底层的 `pylibseekdb` 仅支持 Linux，在 Windows 原生环境下报 `Embedded Client is not available` 错误。**结论：不要再试图在 Windows 原生环境跑这个项目，直接拥抱 WSL2。**
3. **Node.js 与 Vite 权限**：项目要求 Node.js ≥ 22.12.0。通过 nvm 配合国内镜像安装 Node，并解决了从前端跨系统复制导致的 `vite: Permission denied` 权限问题（删掉 `node_modules` 重新 `npm install`）。
4. **网络与代理配置**：成功使用 Watt Toolkit 配合 WSL2 的网关 IP (`172.17.112.1`) 解决了 Git 与 npx 的代理连接问题。

## 💡 学习心得
WSL2 是 Windows 下跑 AI Agent 项目的唯一真神！跨系统复制 `node_modules` 和 `.venv` 是灾难。另外，接入 DeepSeek API 替代 Claude 官方 API 大大降低了成本，配置 `~/.claude/settings.json` 即可完美兼容。
![Uploading 89e5e58618d16e790e31c8393e0f4988.png…]()

