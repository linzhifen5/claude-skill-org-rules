# a-org-rules

自动整理项目根目录下的 `CLAUDE.md` 和 `README.md` 规则文件，确保内容与实际项目结构保持同步。

## 功能

- 自动读取并对比现有规则文件
- 扫描实际项目结构（目录、package.json、入口文件等）
- 同步更新目录结构、技术栈版本、命令列表
- 记录维护日志

## 使用方法

```
/a-org-rules
```

或者直接说：
> 帮我整理 CLAUDE.md 和 README.md

## 整理规则

### CLAUDE.md 更新内容

- **技术栈** - 从 package.json 提取主要依赖版本
- **目录结构** - 完整列出所有文件，与实际项目同步
- **常用命令** - 从 package.json scripts 提取
- **开发说明** - 更新端口、入口路径等

### README.md 更新内容

- **技术栈** - 与 CLAUDE.md 保持一致
- **项目结构** - 目录结构与 CLAUDE.md 完全同步
- **快速开始** - 更新安装和启动命令

### 维护记录

每次整理后会在 `memory/rule-file-maintenance.md` 记录。

## 核心原则

1. CLAUDE.md 和 README.md 的目录结构必须完全一致
2. 技术栈信息必须与 package.json 同步
3. 只记录主要依赖，不过度展开
