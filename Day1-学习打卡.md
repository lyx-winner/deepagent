# Day 1 学习打卡：从零部署 AgentSeek 深度研究环境

本次学习我成功在 WSL2 (Ubuntu) 环境下跑通了 AgentSeek 的 deepagents/research 项目，并成功接入 DeepSeek 模型。以下是我的踩坑与总结：

## 🛠️ 踩坑填坑记录
1. **Python 版本冲突**：Windows 下的 Python 3.14 导致 `langchain-oceanbase` 无法安装，果断迁移到 WSL2，降级使用 Python 3.12 后解决。
2. **数据库限制**：项目底层的 `pylibseekdb` 仅支持 Linux，在 Windows 原生环境下报 `Embedded Client is not available` 错误。**结论：不要再试图在 Windows 原生环境跑这个项目，直接拥抱 WSL2。**
3. **Node.js 与 Vite 权限**：项目要求 Node.js ≥ 22.12.0。通过 nvm 配合国内镜像安装 Node，并解决了从前端跨系统复制导致的 `vite: Permission denied` 权限问题（删掉 `node_modules` 重新 `npm install`）。
4. **网络与代理配置**：成功使用 Watt Toolkit 配合 WSL2 的网关 IP (`172.17.112.1`) 解决了 Git 与 npx 的代理连接问题。

## 💡 学习心得
WSL2 是 Windows 下跑 AI Agent 项目的唯一真神！跨系统复制 `node_modules` 和 `.venv` 是灾难。另外，接入 DeepSeek API 替代 Claude 官方 API 大大降低了成本，配置 `~/.claude/settings.json` 即可完美兼容。


##打卡截图

<img width="572" height="522" alt="89e5e58618d16e790e31c8393e0f4988" src="https://github.com/user-attachments/assets/889880ab-6882-4f0d-a455-a858d5246569" />
<img width="613" height="533" alt="202f39d2fdcd573fb8d1e1c9eb67e9d7" src="https://github.com/user-attachments/assets/ebb24c5e-9fbd-442c-ae91-942794743462" />

<img width="275" height="270" alt="cf125ca58b18d13773d9ab5e134dfbba" src="https://github.com/user-attachments/assets/de03e581-d1d9-4228-a094-3796674887f7" />

<img width="515" height="103" alt="a9fcc89ba62410508fa2ce939fd92cd1" src="https://github.com/user-attachments/assets/2b716cdc-bee4-47d3-8579-3f3342d569d4" />

<img width="923" height="329" alt="e37632eeb1bf6b4a54b1f0f56e3dd486" src="https://github.com/user-attachments/assets/f1766320-c92b-4fc7-bfad-a84a0e81f3e1" />

<img width="899" height="383" alt="2c78390adb4ceab373550d350bfc384b" src="https://github.com/user-attachments/assets/90591ebc-015b-402c-91bb-d167770e4770" />

