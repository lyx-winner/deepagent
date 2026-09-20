#Day 2 学习打卡：多工具 Agent 踩坑实录
在 Day 1 跑通 hello_agent.py 基础上，尝试编写带 calculate 和 convert_currency 两个工具的 math_cal.py，记录如下：

#🛠️ 踩坑填坑记录
1.ModuleNotFoundError: langchain_openai：装过包却找不到，原因是没激活虚拟环境，用到了系统 Python。解决：source .venv/bin/activate 后用 python 运行，验证命令 which python 应指向 .venv/bin/python。
2.KeyError: SILICONFLOW_API_KEY：export 是临时的，关终端就丢了。解决：写入 ~/.bashrc 做永久配置。
3.externally-managed-environment（PEP 668）：Ubuntu 24.04+ 禁止往系统 Python 装包。解决：只用 uv pip install（虚拟环境里）或 pipx
4.模型问题：在处理复杂逻辑的问题时，需要更强的多步推理和工具调用能力

#🎯 一句话总结（可直接作为笔记结尾）
本地搭 AI Agent 踩的坑 80% 不在代码逻辑，而在环境隔离（虚拟环境、环境变量）、网络通道（WSL、代理）和模型能力边界（小模型的多步工具调用）。

<img width="500" height="600" alt="image" src="https://github.com/user-attachments/assets/f35b40df-f3a9-4077-ba1b-1d0650a1bad4" />

<img width="500" height="300" alt="f55d5df12b8bd42dd8dd84d6687f1596" src="https://github.com/user-attachments/assets/7c8b8721-e384-4aa5-af4f-e70d27ca5931" />
