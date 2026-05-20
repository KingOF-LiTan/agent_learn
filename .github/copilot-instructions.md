Follow the repository rules in `AGENTS.md`.

# Copilot Instructions

Copilot 在本项目中主要用于草稿生成、局部补全、测试样例草稿和代码解释。

## Rules

1. Prefer small, local changes.
2. Match the existing project style.
3. Do not invent architecture that is not documented.
4. Do not make large cross-file edits unless the task explicitly asks for them.
5. Add or update tests when behavior changes.
6. Explain assumptions when generating drafts.

## Principle: Why Copilot Is a Drafter

Copilot 很适合快速生成局部代码，但不适合作为最终架构决策者。

本项目把 Copilot 定位为 drafter，是为了让它发挥速度优势，同时避免它在上下文不足时扩大设计范围。草稿可以快，但最终实现必须经过任务卡、验证和 review。

