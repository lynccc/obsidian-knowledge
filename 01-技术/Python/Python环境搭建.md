---
aliases: [安装Python, Python安装, 环境配置]
tags: [技术, Python, 基础, 环境]
created: 2026-06-25 01:52
updated: 2026-06-26 16:12
source: Python编程：从入门到实践
related: [[Hello World]], [[变量]]
---

# 🛠️ Python 环境搭建

## 核心概念

在写代码之前，需要先"安装 Python"和"准备编辑器"

类比：**环境搭建就像做菜前的准备** —— 你得先有锅（Python）、有灶（编辑器），才能开始做菜（写代码）。

---

## 一、检查是否已安装 Python

打开终端（命令行），输入以下命令：

```bash
# 检查 Python 版本
python --version

# 输出示例：
# Python 3.11.4
```

如果显示 `Python 3.x.x`，说明已经安装了 Python 3，可以跳到第三步。

如果提示"命令找不到"，说明没有安装，继续看第二步。

---

## 二、安装 Python

### Linux（Ubuntu/Debian）

```bash
# 用包管理器安装 Python 3
sudo apt-get install python3
```

### Mac

```bash
# 用 Homebrew 安装 Python 3
brew install python3
```

### Windows

1. 打开浏览器，访问 [python.org/downloads](https://python.org/downloads)
2. 点击下载 Python 3 的安装程序
3. **⚠️ 重要：安装时一定要勾选 "Add Python to PATH"**（这样在终端才能直接用 `python` 命令）
4. 点击"安装"

**安装完成后验证：**
```bash
python --version
# 输出：Python 3.x.x
```

---

## 三、安装文本编辑器

编辑器 = **写代码的"笔记本"**，比普通的记事本更强大（能高亮显示代码颜色、自动补全等）。

### 推荐编辑器

| 编辑器 | 特点 | 适合 |
|--------|------|------|
| **VS Code** | 免费，功能强大，插件丰富 | 所有人（推荐！） |
| **PyCharm** | 专业 Python IDE，功能全面 | 专业开发者 |
| **Sublime Text** | 轻量快速，启动快 | 喜欢简洁的人 |

---

## 四、配置编辑器使用 Python 3

如果你的电脑同时装了 Python 2 和 Python 3，需要告诉编辑器用哪个版本。

### VS Code 配置步骤

1. 打开 VS Code
2. 安装 Python 扩展（在扩展商店搜索 "Python"）
3. 按 `Ctrl+Shift+P`（Mac 用 `Cmd+Shift+P`），输入 "Python: Select Interpreter"
4. 选择 Python 3.x.x

### Sublime Text 配置步骤

1. 点击菜单 Tools → Build System → New Build System
2. 删除原有内容，输入以下代码：
```json
{"cmd": ["/usr/local/bin/python3", "-u", "$file"]}
```
3. 保存为 `Python3.sublime-build`
4. 以后写代码时，选择 Tools → Build System → Python3

---

## 五、运行第一个程序

```bash
# 1. 创建一个文件，命名为 hello_world.py
# 2. 在文件里写一行代码：
print("Hello world!")

# 3. 在终端中运行
python hello_world.py

# 输出：
# Hello world!
```

**恭喜！你已经成功运行了第一个 Python 程序！** 🎉

---

## 六、常见问题

### 问题 1：终端提示"命令找不到"

```bash
# 检查 PATH 环境变量（告诉终端去哪里找命令）
echo $PATH

# 如果 Python 安装路径不在 PATH 里，手动添加：
export PATH="/usr/local/bin:$PATH"
```

**类比：** PATH 就像"通讯录"，终端要在通讯录里找到 `python` 这个"联系人"才能运行它。

### 问题 2：权限不足

```bash
# 在命令前加 sudo（用管理员权限运行）
sudo python3 hello_world.py
```

**⚠️ 注意：** `sudo` 会授予管理员权限，只在必要时使用，平时不要乱用。

---

## 总结

| 步骤 | 做什么 | 类比 |
|------|--------|------|
| 1. 检查 Python | 看有没有装 | 看家里有没有锅 |
| 2. 安装 Python | 下载安装 | 买锅 |
| 3. 安装编辑器 | 选一个写代码的工具 | 买灶 |
| 4. 配置编辑器 | 告诉编辑器用哪个 Python | 把锅放在灶上 |
| 5. 运行程序 | 验证一切正常 | 开火试一下 |

---

## 相关笔记

- [[Hello World]] — 第一个程序
- [[变量]] — 存储数据

---

*由奶茶一号整理 🧋*
