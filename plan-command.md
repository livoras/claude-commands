---
allowed-tools: Read
description: 设计 Claude Code 自定义 slash 命令结构
---

## 任务
根据用户描述分析需求并设计 Claude Code slash 命令结构，提供设计方案和建议，但不直接创建文件。

用户需求：$ARGUMENTS

## Custom Slash Commands 文档

### 位置
- 项目级命令：`.claude/commands/`
- 用户级命令：`~/.claude/commands/`

### 语法
```
/<command-name> [arguments]
```

### 主要特性
- 命令是 Markdown (`.md`) 文件
- 支持 YAML frontmatter：
  - `allowed-tools`: 允许的工具
  - `description`: 命令描述

### 命名空间示例
- `.claude/commands/frontend/component.md` 创建 `/frontend:component`
- `~/.claude/commands/component.md` 创建 `/component`

### 参数处理
- 使用 `$ARGUMENTS` 占位符用于动态值
- 示例：`/fix-issue 123`

### 高级功能
- 用 `Bash(xxx)` 执行 bash 命令
- 用 `@` 前缀引用文件
- 支持扩展思考关键词

### 设计要点
分析用户需求后，我将提供：
1. **命令名称建议** - 简洁且具有描述性
2. **文件位置建议** - 项目级还是用户级
3. **YAML frontmatter 设计** - 所需工具权限和描述
4. **命令内容结构** - 提示词设计和参数使用
5. **实现建议** - 具体的创建步骤和注意事项

### 示例参考

#### 简单命令
```markdown
# 文件: .claude/commands/optimize.md
Analyze this code for performance issues and suggest optimizations:
```

#### 带参数的命令
```markdown
# 文件: .claude/commands/fix-issue.md
Fix issue #$ARGUMENTS following our coding standards
```

#### 高级命令
```markdown
---
allowed-tools: Bash(git add:*), Bash(git status:*), Bash(git commit:*)
description: Create a git commit
---

## Context

- Current git status: Bash(git status)
- Current git diff (staged and unstaged changes): Bash(git diff HEAD)
- Current branch: Bash(git branch --show-current 2>/dev/null || echo "Not a git repository")
- Recent commits: Bash(git log --oneline -10)

## Your task

Based on the above changes, create a single git commit.
```

