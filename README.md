# Agent Learn

这是一个长期迭代的 AI agent backend 学习项目。

项目目标不是一次性生成完整系统，而是通过小任务、小 diff、可解释修改和多 agent 协作，逐步学习后端 agent 项目的工程化开发。

## Current Stage

当前阶段：初始化协作规范。

后续优先级：

1. 建立后端项目骨架。
2. 跑通最小 API 服务。
3. 增加健康检查接口。
4. 增加测试和本地验证流程。
5. 再逐步接入模型 provider、tool calling、memory、RAG、eval 和部署。

## Documents

- `AGENTS.md`: 所有 agent 的主规则。
- `CLAUDE.md`: Claude Code 入口规则。
- `.github/copilot-instructions.md`: GitHub Copilot 规则。
- `docs/workflow.md`: 开发工作流。
- `docs/agent-setup.md`: 各 agent 配置和读取验证方法。
- `docs/system-map.md`: 系统结构地图和模块入口。
- `docs/roles/`: 多 agent 角色说明。
- `docs/tasks/`: 任务卡目录。
- `docs/decisions/`: 架构决策记录目录。
- `docs/progress/`: 月度进展记录。

## Principle: Project-Driven Learning

本项目采用项目式学习，而不是一次性学习完整理论。

每次只做一个小功能，并要求 agent 解释为什么这样改。这样你可以同时学习：

1. 后端工程结构。
2. agent 系统设计。
3. git 分支和 review 流程。
4. 测试和 debug 方法。
5. 多 agent 协作边界。
