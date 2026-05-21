# Task Cards

本目录用于保存开发任务卡。

## Task Card Template

```md
# Task: <name>

## Status

Planned | In Progress | Blocked | Verified | Done

## Goal

...

## Background

...

## Files In Scope

...

## Out of Scope

...

## Requirements

...

## Acceptance Criteria

...

## Verification

## Verified By

...

## Commands

...

## Result

...

## Completed Changes

...

## System Map Update

Required | Not Required

Reason:

...

## Learning Notes

...

## Follow-ups

...
```

## Principle: Why Task Cards Matter

任务卡把一句自然语言需求变成可执行边界。

对初学者来说，任务卡能帮助你看到工程开发不是“想到什么写什么”，而是：

1. 明确目标。
2. 限定范围。
3. 设计验收标准。
4. 再进入实现。

对 agent 来说，任务卡能减少幻觉和过度发挥。

## Principle: Why Done Requires Verification

`Done` 不是“代码写完了”，而是“代码写完、验证通过、记录更新完”。

本项目推荐状态流转：

```text
Planned
  -> In Progress
  -> Verified
  -> Done
```

如果 Debugger 验证失败，任务不能进入 `Done`。这能防止 agent 把未验证的实现和未确认的系统结构写成事实。
