---
aliases: [git, 版本控制]
tags: [技术, Git, 工具]
created: 2026-06-24 15:27
source: 奶茶一号整理
related: [[GitHub]]
---

# 🔀 Git

## 核心概念

- **仓库（Repository）** — 项目的版本数据库
- **提交（Commit）** — 一次保存的快照
- **分支（Branch）** — 独立的开发线
- **远程（Remote）** — 远程仓库（如 GitHub）
- **暂存区（Staging Area）** — 准备提交的修改

## 常用命令

```bash
# 基础操作
git init                    # 初始化仓库
git clone <url>             # 克隆仓库
git status                  # 查看状态
git add .                   # 添加所有修改到暂存区
git commit -m "message"     # 提交
git push                    # 推送到远程
git pull                    # 拉取远程更新

# 分支操作
git branch                  # 查看分支
git branch <name>           # 创建分支
git checkout <name>         # 切换分支
git checkout -b <name>      # 创建并切换分支
git merge <name>            # 合并分支
git branch -d <name>        # 删除分支

# 查看历史
git log                     # 查看提交历史
git log --oneline           # 简洁版
git diff                    # 查看修改内容
```

## .gitignore

```
# 忽略所有 .log 文件
*.log

# 忽略 node_modules
node_modules/

# 忽略 .env
.env

# 忽略特定文件
secret.json
```

## 常见场景

### 误提交了大文件
```bash
git reset HEAD~1            # 撤销最后一次提交
git rm --cached <file>      # 从暂存区移除
```

### 想回到某个版本
```bash
git log --oneline           # 找到 commit hash
git checkout <hash>         # 查看该版本
git revert <hash>           # 撤销该提交
```

## 相关笔记

- [[GitHub]] — 远程仓库平台
- [[Docker]] — 常与 Git 配合使用

---

*由奶茶一号整理 🧋*
