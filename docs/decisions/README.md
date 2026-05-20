# Architecture Decision Records

本目录用于保存 ADR，也就是 Architecture Decision Record。

ADR 用来记录重要技术选择。

## ADR Template

```md
# ADR-0001: <decision title>

## Status

Accepted

## Context

...

## Decision

...

## Consequences

...

## Learning Notes

...
```

## Principle: Why ADR Exists

长期项目中，很多问题不是“不知道代码怎么写”，而是几个月后忘记当初为什么这样选。

ADR 的作用是保存决策背景。它不需要写得很长，但必须回答：

1. 当时面对什么问题。
2. 选择了什么方案。
3. 为什么不选其他方案。
4. 这个选择带来了什么代价。

这样后续重构时，你不是在猜历史，而是在阅读历史。

