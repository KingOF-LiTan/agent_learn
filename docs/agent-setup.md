# Agent Setup and Verification

本文档说明如何配置 Codex、Claude Code、VS Code Copilot 和 GitHub Copilot，并验证它们是否读到了本仓库规则。

## Configuration Map

| Agent | Entry File | Purpose |
| --- | --- | --- |
| Codex | `AGENTS.md` | 主规则入口 |
| Claude Code | `CLAUDE.md` | Claude Code 入口，并通过 `@AGENTS.md` 引入主规则 |
| VS Code Copilot | `.github/copilot-instructions.md` | Copilot 仓库级自定义指令 |
| GitHub Copilot coding agent | `.github/copilot-instructions.md` | GitHub 侧 Copilot agent 的仓库级指令 |

## Principle: Why Use One Main Rule File

长期项目里，规则比代码更容易失控。如果每个 agent 都维护一份完整规则，几次修改后就会出现冲突。

本项目采用一个主规则文件：

```text
AGENTS.md
```

其他工具只放入口适配：

```text
CLAUDE.md
.github/copilot-instructions.md
```

这样做的好处是：

1. 规则只有一个事实来源。
2. 修改协作规范时不用同步多份长文档。
3. 各工具仍然能使用自己支持的入口文件。
4. 新 agent 加入项目时，只需要说明它应该读哪个入口。

## Codex Setup

### How to Open

在 Codex 桌面版中新建对话时，选择本仓库目录：

```text
E:\Users\caiyu\Documents\Agent learn
```

这个对话可以作为 Architect。

### Smoke Test Prompt

新建 Codex Architect 对话后，先发送：

```text
请先不要写代码。请根据 AGENTS.md 回答：
1. 本项目的主目标是什么？
2. 修改代码后必须解释哪四类内容？
3. Architect 不应该负责什么？
如果你没有读取到 AGENTS.md，请直接说没有读取到。
```

### Expected Result

它应该能回答：

1. 项目目标是长期迭代的 AI agent backend 学习项目。
2. 修改后要解释改了什么、为什么改、影响行为、如何验证。
3. Architect 不负责大规模实现、不绕过任务卡、不为了高级而引入复杂架构。

## Claude Code Setup

### How to Open

在 VS Code 里打开仓库目录，然后在 Claude Code 中使用该目录作为工作区。

Claude Code 应该读取：

```text
CLAUDE.md
```

而 `CLAUDE.md` 第一行会引入：

```text
@AGENTS.md
```

### Smoke Test Prompt

```text
请先不要写代码。请根据 CLAUDE.md 和它引入的 AGENTS.md 回答：
1. 本项目为什么要保持最小 diff？
2. Implementer 修改完成后的报告必须包含什么？
3. 什么情况下你必须停止并询问用户？
如果你没有读到这些文件，请直接说没有读到。
```

### Expected Result

它应该提到：

1. 小 diff 有利于 review、定位 bug、回滚和多 agent 协作。
2. 报告要包含修改文件、修改原因、验证结果、风险和后续。
3. 删除大量文件、重写核心架构、引入新框架或数据库、验证失败原因不明等情况要停止。

## VS Code Copilot Setup

### How to Enable

在 VS Code 中打开仓库后，确认 Copilot Chat 启用了 repository custom instructions。

本项目的 Copilot 指令文件是：

```text
.github/copilot-instructions.md
```

### Smoke Test Prompt

在 Copilot Chat 中发送：

```text
根据本仓库的 Copilot instructions 回答：
1. Copilot 在本项目中的定位是什么？
2. 它不应该做哪两类事情？
3. 生成草稿时需要说明什么？
```

### Expected Result

它应该回答 Copilot 是 drafter，负责草稿、局部补全、测试样例草稿和解释；不应该做最终架构决策或大范围跨文件修改；生成草稿时要说明 assumptions。

## GitHub Copilot Coding Agent Setup

### How to Use

GitHub 网页端的 Copilot coding agent 通常会读取仓库里的：

```text
.github/copilot-instructions.md
```

如果你让它处理 issue 或 PR，建议 issue 里也显式引用任务卡。

### Smoke Test Prompt

在 issue 或 Copilot agent 请求中写：

```text
请先只阅读仓库规则，不要改代码。请根据 .github/copilot-instructions.md 总结你在本项目中的职责边界。
```

### Expected Result

它应该把自己定位为草稿和局部辅助角色，而不是架构师或最终 reviewer。

## Recommended First Architect Prompt

当你新开 Codex Architect 对话后，可以直接使用：

```text
你是本项目的 Architect。请先读取 AGENTS.md、docs/workflow.md 和 docs/roles/architect.md。

目标：把“初始化 FastAPI 后端骨架并提供 /health 接口”拆成 3 到 5 个小任务卡。

要求：
1. 不要写代码。
2. 每个任务卡包含目标、涉及文件、不涉及、实现要求、验收标准、验证命令、学习点。
3. 保持任务足够小，适合交给 Implementer 独立完成。
4. 如果你认为目标过大，请先说明如何缩小范围。
```

## Recommended First Implementer Prompt

当 Architect 产出任务卡后，给 Claude Code Implementer：

```text
你是本项目的 Implementer。请读取 AGENTS.md、CLAUDE.md、docs/workflow.md 和 docs/roles/implementer.md。

只完成下面这张任务卡，不要做额外重构。

<粘贴任务卡>

完成后请报告：
1. 修改了哪些文件。
2. 为什么这样改。
3. 如何验证。
4. 风险和后续。
```

## Recommended Debugger Prompt

当测试或运行失败时，给 Claude Code Debugger：

```text
你是本项目的 Debugger。请读取 AGENTS.md、CLAUDE.md、docs/workflow.md 和 docs/roles/debugger.md。

当前失败命令：
<粘贴命令>

错误输出：
<粘贴错误>

请按顺序执行：
1. 复现失败。
2. 定位根因。
3. 提出最小修复。
4. 补充回归验证。
5. 重新运行验证命令。
```

## Verification Checklist

配置完成后，逐个检查：

```text
[ ] Codex Architect 能总结 AGENTS.md 规则。
[ ] Claude Code 能读取 CLAUDE.md，并知道它引用 AGENTS.md。
[ ] VS Code Copilot 能说出自己是 drafter。
[ ] GitHub Copilot coding agent 能根据 .github/copilot-instructions.md 总结职责。
[ ] 每个 agent 都知道修改后必须解释原因和验证方式。
```

## Troubleshooting

### Agent Says It Cannot Read the File

检查当前工作区是否打开的是仓库根目录，而不是上级或下级目录。

正确目录：

```text
E:\Users\caiyu\Documents\Agent learn
```

### Agent Ignores the Rules

在 prompt 里显式要求它先读取具体文件：

```text
请先读取 AGENTS.md 和 docs/workflow.md，再回答。
```

### Copilot Gives Generic Answers

Copilot 有时不会主动展示它读到的 instructions。验证时要问具体问题，而不是问“你读到了吗”。

好的验证问题：

```text
根据本仓库规则，Copilot 在本项目中为什么只是 drafter？
```

不好的验证问题：

```text
你读到配置了吗？
```

