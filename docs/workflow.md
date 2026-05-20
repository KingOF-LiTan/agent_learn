# Development Workflow

本文档描述本项目的日常开发流程。目标是让初学者可以通过真实项目学习 agent backend，同时让多个 AI agent 的协作保持可控。

## Standard Flow

```text
idea
  -> Architect 拆任务
  -> 写任务卡
  -> 创建分支或 worktree
  -> Implementer 实现
  -> 本地验证
  -> Debugger 处理失败
  -> Architect review
  -> 用户确认 merge
```

## Step 1: Idea

用户提出一个目标，例如：

```text
我想先让 FastAPI 后端跑起来，并提供 /health 接口。
```

这个阶段不直接写代码。先判断目标是否足够小。

## Step 2: Architect Breaks Down Work

Architect 负责把目标拆成任务卡。

任务卡必须包含：

```text
目标：
背景：
涉及文件：
不涉及：
实现要求：
验收标准：
验证命令：
学习点：
```

## Step 3: Implementer Makes a Small Patch

Implementer 只做任务卡里的事情。

实现完成后必须说明：

```text
改了什么：
为什么这样改：
如何验证：
后续可以怎么扩展：
```

## Step 4: Debugger Handles Failures

如果运行失败或测试失败，交给 Debugger。

Debugger 必须按顺序做：

1. 复现失败。
2. 记录失败命令和错误信息。
3. 定位根因。
4. 做最小修复。
5. 重新运行验证。

## Step 5: Review and Merge

Architect review 时重点看：

1. 是否满足验收标准。
2. diff 是否足够小。
3. 是否引入不必要复杂度。
4. 是否有测试或合理验证。
5. 是否解释了修改原因。

最终是否 merge 由用户决定。

## Principle: Why Workflow Comes Before Code

AI 很容易“一句话生成一坨代码”。短期看很快，长期看会让项目变成无法解释、无法维护、无法学习的状态。

工作流的价值是把每次开发变成可观察的学习过程：

1. 需求为什么拆成这样。
2. 代码为什么这样写。
3. 验证为什么能证明它有效。
4. 下次扩展应该接在哪里。

这比一次性生成完整系统更慢，但更适合长期维护和研究生阶段的系统性学习。

