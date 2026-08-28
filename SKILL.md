---
name: a-org-rules
description: 整理项目根目录下的 CLAUDE.md 和 README.md 规则文件，确保内容与实际项目结构保持同步。当项目添加了新应用、技术栈更新、目录结构变化时使用此技能。
---

# 整理规则文件

## 概述

自动检查并更新项目的 `CLAUDE.md` 和 `README.md`，确保文档与实际项目结构一致，包括：目录结构、命令、技术栈版本、应用列表等信息。同时自动给 `src/` 目录下的代码文件添加注释。

## 工作流程

### 1. 读取现有规则文件

读取项目根目录下的 `CLAUDE.md` 和 `README.md` 当前内容，了解现有结构和描述。

### 2. 检查实际项目状态

扫描项目目录，获取：
- 根目录下的文件夹结构
- `package.json` 中的脚本命令和技术栈版本
- 应用入口文件（如 `main.ts`、`index.js` 等）
- 配置文件（如 `.gitignore`、`tsconfig.json` 等）

### 2.1 整理 .gitignore

检查 `.gitignore` 文件，确保包含以下常见不需要 Git 追踪的文件和目录：

```
# Node
node_modules/
dist/
dist-ssr/
dist-electron/
*.local

# Logs
logs/
*.log

# Environment
.env
.env.local
.env.*.local

# Build output
release/

# Editor
.vscode/
.idea/
.DS_Store
```

### 3. 自动添加代码注释（自动执行）

扫描 `src/` 目录下的 `.ts`、`.tsx`、`.css` 文件，检查是否已有注释，如有则跳过。给未添加注释的文件添加顶部注释。

### 4. 更新 CLAUDE.md

确保以下内容与实际项目一致：

- **目录结构** - 更新 `## 目录结构` 部分，反映实际的目录层级
- **常用命令** - 从 `package.json` 的 `scripts` 字段提取命令列表
- **技术栈** - 从 `package.json` 的 `dependencies`/`devDependencies` 提取主要技术版本
- **开发说明** - 更新应用入口、构建输出等路径信息

### 5. 更新 README.md

同步更新以下内容：

- **项目简介** - 确保描述准确
- **技术栈徽章** - 更新版本信息
- **目录结构** - 与 CLAUDE.md 保持一致
- **快速开始** - 更新安装和启动命令
- **项目结构说明** - 各目录/文件的用途说明

### 6. 维护记录

在项目根目录创建或更新 `memory/rule-file-maintenance.md`，记录：
- 整理日期
- 更新了哪些内容
- 是否有人工确认

### 7. Skill 自身更新（仅当 skill 有变更时执行）

当此 skill 的 SKILL.md 内容发生变更时，必须同步更新 README 文件：

- **README.md** - 更新"整理规则"部分，说明新增或变更的功能
- **README_en.md** - 更新英文版本，与中文版保持同步
- **更新日志** - 在两个 README 顶部添加 version 或 changelog 记录本次变更

## 代码注释规则

整理规则文件时自动执行，无需用户请求。

### 应用范围

处理以下目录下的 `.ts`、`.tsx`、`.css` 文件：
- `src/` 目录
- `electron/` 目录

### 文件顶部注释格式

- `.ts`、`.tsx` 文件：
```typescript
/**
 * 文件名.tsx
 * 文件用途简述
 */
```

- `.css` 文件：
```css
/* 文件名.css 用途说明 */
```

### 代码注释转换（自动执行）

当扫描到已添加注释的文件时，检查其中的英文注释并转换为中文：

**转换规则**：
- `// Restore enabled scripts on startup` → `// 启动时恢复启用的脚本`
- `{/* Starry Background */}` → `{/* 星空背景 */}`
- 保持 `//` 和 `{/* */}` 注释符号
- 将英文转换为简洁的中文短语
- 转换整个文件中所有英文注释

**注释类型**：
- `//` 单行注释
- `{/* */}` JSX/TSX 注释

**执行顺序**：

1. 扫描 `src/` 目录下所有 `.ts`、`.tsx`、`.css` 文件
2. 检查文件是否已有顶部注释，如有则跳过
3. 分析文件内容，生成文件用途说明
4. 添加文件顶部注释
5. 检查文件中是否存在英文注释，如有则转换为中文
6. 跳过 `node_modules`、`dist` 等目录

### 原则

- **简洁** - 注释不超过 2 行
- **中文** - 全部使用中文
- **不重复** - 已有注释的文件不重复添加
- **保守** - 不确定时不添加，保留原样

### macOS 无标题栏窗口

Electron 创建无标题栏窗口时，需要同时配置拖拽区域：

**1. 主进程配置** (`electron/main.ts`)：
```typescript
win = new BrowserWindow({
  frame: false,           // 禁用原生窗口框架
  titleBarStyle: 'hidden', // macOS 隐藏标题栏
})
```

**2. 渲染进程配置** (React)：
```tsx
// 主布局设为拖拽区域
<div style={{ WebkitAppRegion: 'drag' } as React.CSSProperties}>
  {/* 可交互元素设为不可拖拽 */}
  <button style={{ WebkitAppRegion: 'no-drag' } as React.CSSProperties}>点击</button>
  <aside style={{ WebkitAppRegion: 'no-drag' } as React.CSSProperties}>...</aside>
</div>
```

## GitHub 推送流程

当 skill 更新完成后，自动推送到 GitHub（无需确认）：

```bash
cd ~/.claude/skills/a-org-rules
git add .
git commit -m "Update: 描述本次变更"
git remote set-url origin git@github.com:linzhifen5/claude-skill-org-rules.git
git push -u origin main --force
```

推送成功后显示：
> ✅ 已推送到 https://github.com/linzhifen5/claude-skill-org-rules

## 验证

更新完成后，使用 `grep` 或 `Read` 工具抽查关键内容是否正确匹配实际项目文件。
