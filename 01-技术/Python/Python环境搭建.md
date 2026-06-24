---
aliases: [安装Python, Python安装, 环境配置]
tags: [技术, Python, 基础, 环境]
created: 2026-06-25 01:52
source: Python编程：从入门到实践
related: [[Hello World]], [[变量]]
---

# 🛠️ Python 环境搭建

## 核心概念

- Python 2 和 Python 3 有差异
- 推荐使用 Python 3
- 需要安装文本编辑器

## 检查是否安装 Python

```bash
# Linux/Mac
python --version
python3 --version

# Windows
python --version
```

## 安装 Python

### Linux
```bash
sudo apt-get install python3
```

### Mac
```bash
brew install python3
```

### Windows
1. 访问 python.org/downloads
2. 下载 Python 3 安装程序
3. **勾选 "Add Python to PATH"**
4. 安装

## 安装文本编辑器

### 推荐编辑器
- **VS Code** — 免费，功能强大
- **PyCharm** — 专业 Python IDE
- **Sublime Text** — 轻量快速

## 配置编辑器使用 Python 3

如果系统有多个 Python 版本，需要配置编辑器使用 Python 3。

### VS Code
1. 安装 Python 扩展
2. 选择 Python 3 解释器

### Sublime Text
1. Tools → Build System → New Build System
2. 输入：`{"cmd": ["/usr/local/bin/python3", "-u", "$file"]}`
3. 保存为 Python3.sublime-build

## 运行第一个程序

```bash
# 创建文件 hello_world.py
print("Hello world!")

# 运行
python hello_world.py
```

## 常见问题

### 命令找不到
```bash
# 检查 PATH
echo $PATH

# 手动添加路径
export PATH="/usr/local/bin:$PATH"
```

### 权限问题
```bash
# 使用 sudo
sudo python3 hello_world.py
```

## 相关笔记

- [[Hello World]] — 第一个程序
- [[变量]] — 存储数据

---

*由奶茶一号整理 🧋*
