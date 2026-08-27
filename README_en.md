# a-org-rules

Automatically organize and synchronize `CLAUDE.md` and `README.md` rule files in the project root directory with the actual project structure.

[中文](README.md) | [Changelog](#changelog)

## Changelog

### v1.2.0 (2026-08-28)

- Added: Code comment feature - add file header and JSDoc comments to .ts/.tsx files in src/
- Added: GitHub push feature - auto push after updates, no confirmation needed

### v1.1.0 (2026-08-28)

- Added: Auto-sync README when skill itself is updated
- Added: Maintain both Chinese and English README

### v1.0.0 (2026-08-28)

- Initial release

## Features

### Rule File Organization

- Read and compare existing rule files
- Scan actual project structure (directories, package.json, entry files, etc.)
- Synchronize directory structure, tech stack versions, and command lists
- Maintain update logs

### Code Comments

- Add file header comments to `.ts` and `.tsx` files in `src/`
- Add JSDoc comments to exported functions and components
- Skip files that already have comments

## Usage

```text
/a-org-rules
```

Or simply say：

> Help me organize CLAUDE.md and README.md
> Add comments to src files

## Organization Rules

### CLAUDE.md Updates

- **Tech Stack** - Extract main dependency versions from package.json
- **Directory Structure** - List all files completely, synced with actual project
- **Common Commands** - Extract from package.json scripts
- **Development Notes** - Update port, entry paths, etc.

### README.md Updates

- **Tech Stack** - Consistent with CLAUDE.md
- **Project Structure** - Directory structure fully synced with CLAUDE.md
- **Quick Start** - Update installation and startup commands

### Maintenance Logs

Each organization is recorded in `memory/rule-file-maintenance.md`.

## Code Comment Rules

### File Header

```typescript
/**
 * App.tsx
 * Main application component
 */
```

### JSDoc Comments

```typescript
/**
 * Get user information
 * @param id - User ID
 * @returns User info object
 */
```

## Core Principles

1. CLAUDE.md and README.md directory structures must be identical
2. Tech stack info must sync with package.json
3. Only record main dependencies, don't over-expand
4. Keep comments concise, don't duplicate
