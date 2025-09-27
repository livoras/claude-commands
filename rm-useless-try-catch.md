---
allowed-tools:
  - Read
  - Glob
  - Grep
  - Edit
  - MultiEdit
  - Bash(find:*)
  - Bash(grep:*)
description: 删除只记录日志或重新抛出异常的无用try-catch块
---

# 删除无意义的 try-catch 块

你的任务是删除代码中无意义的 try-catch 块。

**目标文件/目录：** $ARGUMENTS (如果为空则处理整个项目)

## 无意义 try-catch 的定义

以下情况被认为是无意义的 try-catch：

1. **仅记录日志：** catch 块只包含 console.log、console.error、logger.error 等
2. **原地重抛：** catch 块只是重新抛出相同的异常
3. **空 catch 块：** catch 块为空或只有注释

## 处理步骤

### 1. 搜索 try-catch 块
- 搜索项目中所有 TypeScript/JavaScript 文件
- 定位包含 try-catch 的文件

### 2. 分析 catch 块内容
对每个 try-catch 块分析：
- catch 块是否只包含日志记录
- catch 块是否只是重新抛出异常
- catch 块是否为空

### 3. 识别无意义模式
```javascript
// 模式1: 仅记录日志
try {
  // code
} catch (error) {
  console.error(error);
  // 或 logger.error(error);
}

// 模式2: 原地重抛
try {
  // code
} catch (error) {
  throw error;
  // 或 throw e;
}

// 模式3: 空 catch
try {
  // code
} catch (error) {
  // 空的或只有注释
}
```

### 4. 安全删除
- 保留 try 块中的代码
- 删除 try-catch 包装
- 确保代码逻辑不变
- 保持原有缩进格式

## 注意事项

- 仔细检查每个 catch 块，确保真的无意义
- 保留有实际错误处理逻辑的 try-catch
- 删除后验证代码语法正确性
- 处理完成后报告删除的数量和位置