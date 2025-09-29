---
allowed-tools:
  - Bash
  - Read
  - Glob
description: 咨询 codex 编码助手，根据项目上下文提供技术建议
---

# Codex 咨询助手

向 codex 编码助手咨询技术问题。

Bash(codex exec "...根据问题整理上下问题...")

* 用户直接 `/codex` 则根据上下文对话整理信息和问题传入 `codex exec "...."`
* /codex $ARGUMENTS 根据需求 $ARGUMENTS 整理相关的内容传给 codex
* 传给 codex 的问题要精准，问出正确的问题；符合事实，包含必要的上下文信息

