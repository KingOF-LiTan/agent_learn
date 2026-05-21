# System Map

本文档是项目的系统结构地图。它帮助 Architect、Implementer 和 Debugger 快速理解代码入口、模块职责和常见任务应该从哪里开始。

当前项目还处于初始化阶段，后端代码尚未建立。下面是预期的起步结构，实际实现后需要由验证通过的任务更新。

## Directory Overview

| Path | Responsibility | Status |
| --- | --- | --- |
| `AGENTS.md` | 所有 agent 的主规则 | Active |
| `CLAUDE.md` | Claude Code 入口规则 | Active |
| `.github/copilot-instructions.md` | Copilot 仓库级规则 | Active |
| `docs/workflow.md` | 开发流程 | Active |
| `docs/agent-setup.md` | agent 配置和 smoke test | Active |
| `docs/roles/` | agent 角色边界 | Active |
| `docs/tasks/` | 任务卡和完成记录 | Active |
| `docs/decisions/` | 架构决策记录 | Active |
| `docs/progress/` | 月度项目进展 | Active |

## Planned Backend Areas

这些目录是后续后端骨架的推荐方向。只有在对应任务实现并验证通过后，才能从 planned 变成 active。

| Planned Path | Responsibility |
| --- | --- |
| `src/app/` | FastAPI app 创建和启动入口 |
| `src/api/` | HTTP route 层 |
| `src/core/` | 配置、日志和共享基础设施 |
| `src/agents/` | agent 编排逻辑 |
| `src/providers/` | 模型 provider 适配层 |
| `tests/` | 自动化测试 |

## Module Boundary Rules

1. API route 不应直接调用外部模型 SDK。
2. Provider 负责隐藏模型供应商差异。
3. Agent 层负责编排 provider、tool、memory 等能力。
4. Core 层只放共享配置、日志和基础设施。
5. 测试应跟随行为边界，而不是只跟随文件名。

## Where To Start

| Task Type | Start Here | Avoid |
| --- | --- | --- |
| 修改协作规则 | `AGENTS.md` | 直接改各工具适配文件造成规则漂移 |
| 修改 Claude Code 行为 | `CLAUDE.md` | 复制整份 `AGENTS.md` |
| 修改 Copilot 行为 | `.github/copilot-instructions.md` | 让 Copilot 承担架构决策 |
| 修改开发流程 | `docs/workflow.md` | 只改角色文件导致流程不一致 |
| 新增任务卡模板 | `docs/tasks/README.md` | 把任务状态只写进聊天记录 |
| 新增架构选择记录 | `docs/decisions/` | 把重大选择藏在 commit message |

## Update Rules

只有在 Debugger 验证通过，或用户明确接受等价验证后，才能把结构变化记录到本文档。

需要更新本文档的情况：

1. 新增或删除顶层目录。
2. 新增核心模块。
3. 改变模块职责。
4. 改变模块调用关系。
5. 新增常见任务入口。

不需要更新本文档的情况：

1. 只修复局部 bug。
2. 只调整注释或文案。
3. 只修改测试数据。
4. 没有改变模块职责或目录结构。

## Principle: Why This File Exists

当系统变大后，agent 如果每次任务都全仓库搜索，会浪费上下文，也更容易误改无关模块。

System map 的作用是提供第一入口：

```text
先看结构地图
  -> 找到可能相关模块
  -> 只阅读必要文件
  -> 如果地图不足，再有限搜索
  -> 把不足反馈进文档
```

它不是代码百科全书，不记录每个函数。它只记录能帮助 agent 正确进入系统的结构信息。
