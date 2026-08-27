---
name: a-org-rules
description: 整理项目根目录下的 CLAUDE.md 和 README.md 规则文件，确保内容与实际项目结构保持同步。当项目添加了新应用、技术栈更新、目录结构变化时使用此技能。
---

# 整理规则文件

## 概述

自动检查并更新项目的 `CLAUDE.md` 和 `README.md`，确保文档与实际项目结构一致，包括：目录结构、命令、技术栈版本、应用列表等信息。

## 工作流程

### 1. 读取现有规则文件

读取项目根目录下的 `CLAUDE.md` 和 `README.md` 当前内容，了解现有结构和描述。

### 2. 检查实际项目状态

扫描项目目录，获取：
- 根目录下的文件夹结构
- `package.json` 中的脚本命令和技术栈版本
- 应用入口文件（如 `main.ts`、`index.js` 等）
- 配置文件（如 `.gitignore`、`tsconfig.json` 等）

### 3. 更新 CLAUDE.md

确保以下内容与实际项目一致：

- **目录结构** - 更新 `## 目录结构` 部分，反映实际的目录层级
- **常用命令** - 从 `package.json` 的 `scripts` 字段提取命令列表
- **技术栈** - 从 `package.json` 的 `dependencies`/`devDependencies` 提取主要技术版本
- **开发说明** - 更新应用入口、构建输出等路径信息

### 4. 更新 README.md

同步更新以下内容：

- **项目简介** - 确保描述准确
- **技术栈徽章** - 更新版本信息
- **目录结构** - 与 CLAUDE.md 保持一致
- **快速开始** - 更新安装和启动命令
- **项目结构说明** - 各目录/文件的用途说明

### 5. 维护记录

在项目根目录创建或更新 `memory/rule-file-maintenance.md`，记录：
- 整理日期
- 更新了哪些内容
- 是否有人工确认

### 6. Skill 自身更新（仅当 skill 有变更时执行）

当此 skill 的 SKILL.md 内容发生变更时，必须同步更新 README 文件：

- **README.md** - 更新"整理规则"部分，说明新增或变更的功能
- **README_en.md** - 更新英文版本，与中文版保持同步
- **更新日志** - 在两个 README 顶部添加 version 或 changelog 记录本次变更

## 代码注释功能

当用户要求"添加注释"、"给文件加注释"、"生成 JSDoc" 时执行此功能。

### 应用范围

仅处理 `src/` 目录下的 `.ts` 和 `.tsx` 文件。

### 文件顶部注释规则

在文件顶部添加注释块，包含：
- 文件名
- 文件用途简述

格式：
```typescript
/**
 * 文件名.tsx
 * 文件用途简述
 */
```

### JSDoc 注释规则

给导出函数和组件添加 JSDoc：

```typescript
/**
 * 函数简述
 * @param 参数名 - 参数说明
 * @returns 返回值说明
 */
```

```typescript
/**
 * 组件简述
 * @description 组件详细说明（仅当需要时添加）
 */
```

### 执行顺序

1. 扫描 `src/` 目录下所有 `.ts`、`.tsx` 文件
2. 检查文件是否已有顶部注释，如有则跳过
3. 分析文件内容，生成文件用途说明
4. 添加文件顶部注释
5. 检查导出函数/组件，添加 JSDoc（已有则跳过）
6. 跳过 `node_modules`、`dist` 等目录

### 原则

- **简洁** - 注释不超过 2 行
- **中文** - 全部使用中文
- **不重复** - 已有注释的文件不重复添加
- **保守** - 不确定时不添加，保留原样

## GitHub 推送流程

当 skill 更新完成后，提示用户是否推送到 GitHub：

> ✅ Skill 已更新，是否推送到 GitHub？

用户确认后执行：

```bash
cd ~/.claude/skills/a-org-rules
git init (若未初始化)
git add .
git commit -m "Update: 描述本次变更"
git remote set-url origin https://github.com/linzhifen5/claude-skill-org-rules.git
git push -u origin main --force
```

推送成功后显示：
> ✅ 已推送到 https://github.com/linzhifen5/claude-skill-org-rules

## 验证

更新完成后，使用 `grep` 或 `Read` 工具抽查关键内容是否正确匹配实际项目文件。
