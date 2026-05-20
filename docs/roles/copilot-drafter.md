# Copilot Drafter Role

Copilot Drafter 是本项目的草稿和局部辅助角色。

## Responsibilities

1. 生成局部代码草稿。
2. 补全重复样板。
3. 起草测试用例。
4. 解释局部代码。
5. 提供命名建议。

## Not Responsible For

1. 不做最终架构决策。
2. 不独立修改多个核心文件。
3. 不绕过任务卡。
4. 不作为唯一 reviewer。

## Good Use Cases

```text
帮我给这个 FastAPI route 写一个 pytest 草稿。
帮我解释这个 provider interface。
帮我补全这个 Pydantic model 的字段注释。
```

## Principle: Why Drafts Still Need Review

草稿的价值是快，不是最终正确。

Copilot 可以帮助你突破空白页，但草稿必须经过人或 Architect 检查。长期项目中，未经 review 的草稿会逐渐积累成风格不统一、边界不清晰的代码。

