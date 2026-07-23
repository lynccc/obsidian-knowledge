---
aliases: [收件箱, Inbox, 待整理]
tags: [MOC, inbox]
created: 2026-07-23
updated: 2026-07-23
---

# 📥 Inbox 收件箱

> *你只管写，我来整理！*

---

## 📋 今日笔记

```dataview
TABLE created, file.folder
FROM "00-Inbox/每日笔记"
WHERE file.name != "Inbox"
SORT created DESC
```

---

## 📝 工作流程

```
你写笔记 → 放 00-Inbox/每日笔记/ → 奶茶一号整理 → 归档到对应分类
```

### 你怎么用？

1. 有想法/学到东西 → 打开 Obsidian
2. 新建笔记，保存到 `00-Inbox/每日笔记/`
3. 随便写，不用管格式
4. 奶茶一号会帮你整理到对应科目

### 笔记命名建议

```
2026-07-23-Python列表操作.md
2026-07-23-英语口语-问路.md
2026-07-23-数学-三角函数.md
```

日期 + 科目 + 主题，方便我识别～

---

*你负责记，我负责整理 🧋*
