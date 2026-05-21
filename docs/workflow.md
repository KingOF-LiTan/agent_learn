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
  -> Debugger 验证或处理失败
  -> 更新任务卡和系统结构记录
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

开始实现前，Implementer 应先阅读：

```text
docs/system-map.md
docs/tasks/<task-id>.md
```

如果 `docs/system-map.md` 无法定位相关模块，Implementer 可以进行有限搜索，并在完成报告中说明搜索原因。

实现完成后必须说明：

```text
改了什么：
为什么这样改：
如何验证：
后续可以怎么扩展：
```

## Step 4: Debugger Handles Failures

如果运行失败或测试失败，交给 Debugger。即使 Implementer 自己的验证通过，重要任务也应由 Debugger 或等价验证做一次独立确认。

Debugger 必须按顺序做：

1. 复现失败。
2. 记录失败命令和错误信息。
3. 定位根因。
4. 做最小修复。
5. 重新运行验证。

如果验证通过，Debugger 必须把验证命令和结果写回任务卡的 `Verification` 部分。

## Step 5: Update Records

Debugger 验证通过后，才能更新完成记录。

必须更新：

```text
docs/tasks/<task-id>.md
```

如果本次任务改变了目录、模块职责或调用关系，还必须更新：

```text
docs/system-map.md
```

如果只是修改局部实现，没有改变系统结构，不需要更新 system map，但要在任务卡中说明。

## Step 6: Review and Merge

Architect review 时重点看：

1. 是否满足验收标准。
2. diff 是否足够小。
3. 是否引入不必要复杂度。
4. 是否有测试或合理验证。
5. 是否解释了修改原因。
6. 任务卡、system map、ADR 是否按需更新。

最终是否 merge 由用户决定。

## Principle: Why Workflow Comes Before Code

AI 很容易“一句话生成一坨代码”。短期看很快，长期看会让项目变成无法解释、无法维护、无法学习的状态。

工作流的价值是把每次开发变成可观察的学习过程：

1. 需求为什么拆成这样。
2. 代码为什么这样写。
3. 验证为什么能证明它有效。
4. 下次扩展应该接在哪里。

这比一次性生成完整系统更慢，但更适合长期维护和研究生阶段的系统性学习。

## Principle: Why System Map Comes After Verification

`docs/system-map.md` 描述的是已经成立的系统结构，不是实现计划。

如果代码还没通过验证就更新 system map，后续 agent 会把未验证的设计当成事实，反而更容易走错方向。

所以本项目规定：

```text
先验证代码真的工作
再记录系统结构已经改变
```
