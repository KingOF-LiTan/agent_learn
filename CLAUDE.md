@AGENTS.md

# Claude Code Notes

本文档是 Claude Code 的入口文件。通用规则在 `AGENTS.md`，这里仅补充 Claude Code 使用习惯。

## Claude Code Specific Rules

1. 大范围修改前先给出简短计划。
2. 实现时严格遵守任务卡，不主动扩大范围。
3. 修 bug 时先复现，再解释根因，再给最小修复。
4. 不要直接启动长时间运行的服务而不说明停止方式。
5. 修改完成后必须解释 diff 的学习价值。

## Principle: Why Import AGENTS.md

`AGENTS.md` 是本仓库的唯一主规则。Claude Code 使用 `CLAUDE.md`，所以这里通过 `@AGENTS.md` 引入主规则。

这样做的原因是避免多份规则互相漂移。长期项目中，如果 Codex、Claude Code、Copilot 各有一套完整说明，几轮迭代后很容易出现冲突。主规则只维护一份，各工具只写适配层。

