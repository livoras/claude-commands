---
allowed-tools: Write, Read, LS, Bash(mkdir*)
description: 自动创建 Claude Code 自定义 slash 命令
---

## 任务
根据用户描述自动创建 Claude Code slash 命令文件。

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

### 示例

#### Example: 项目命令
```markdown
# 文件: .claude/commands/optimize.md
Analyze this code for performance issues and suggest optimizations:
```

#### Example: 用户命令
```markdown
# 文件: ~/.claude/commands/security-review.md
Review this code for security vulnerabilities:
```

#### Example: 带参数的命令
```markdown
# 文件: .claude/commands/fix-issue.md
Fix issue #$ARGUMENTS following our coding standards
```

#### Example: 带 YAML Frontmatter 的高级命令
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

#### 创建命令的方式
```bash
# 项目命令
mkdir -p .claude/commands
echo "Analyze this code for performance issues and suggest optimizations:" > .claude/commands/optimize.md

# 用户命令
mkdir -p ~/.claude/commands
echo "Review this code for security vulnerabilities:" > ~/.claude/commands/security-review.md
```
