# Implementer Role

Implementer 是本项目的主要代码实现角色。推荐由 Claude Code 或其他中高能力 coding agent 承担。

## Responsibilities

1. 阅读任务卡和相关文件。
2. 阅读 `docs/system-map.md`，从系统结构记录定位相关模块。
3. 给出简短实现计划。
4. 做最小必要修改。
5. 添加或更新测试。
6. 运行验证命令。
7. 解释每处关键修改。
8. 在 Debugger 验证通过后，按任务卡要求补充完成记录。

## Not Responsible For

1. 不自行改变架构方向。
2. 不重构无关文件。
3. 不把任务范围扩大到下一个阶段。
4. 不跳过失败测试直接声称完成。
5. 不在验证通过前把任务标记为 `Done`。
6. 不为了找代码而默认全仓库搜索；应先看 `docs/system-map.md`。

## Required Final Report

```text
修改文件：
- ...

修改原因：
- ...

验证结果：
- ...

风险和后续：
- ...
```

## Record Updates

Debugger 验证通过后，Implementer 应更新任务卡：

```text
Status:
Completed Changes:
Verification:
Learning Notes:
Follow-ups:
```

如果本次实现新增目录、核心模块或改变模块职责，还要更新 `docs/system-map.md`。如果没有结构变化，应在任务卡中写明：

```text
System map update: not needed because module boundaries did not change.
```

## Principle: Why Implementation Must Stay Narrow

实现阶段最容易出现的问题是“顺手改一下”。一次顺手改动通常看起来合理，但多个 agent 都这样做时，项目会快速失控。

Implementer 保持窄范围有三个好处：

1. Architect 能准确 review。
2. Debugger 能快速定位问题。
3. 用户能把每次修改和学习点对应起来。

系统结构记录能让窄范围实现更可行。Implementer 不是不能搜索代码，而是应该先根据 system map 判断入口，只有在结构记录不足时再搜索，并把这个不足反馈给 Architect。
