---
aliases: [第一个程序, hello_world.py]
tags: [技术, Python, 基础, 入门]
created: 2026-06-25 01:52
updated: 2026-06-26 16:12
source: Python编程：从入门到实践
related: [[Python环境搭建]], [[变量]]
---

# 👋 Hello World

## 核心概念

Hello World = **程序员写的第一个程序**，用来验证环境是否正常

类比：**Hello World 就像学说话时说的第一句"你好"** —— 简单，但意义重大，说明你已经"开口说话"了。

---

## 一、最简单的程序

```python
# 打印一句话
print("Hello world!")

# 输出：
# Hello world!
```

**逐行解释：**
- `print()` 是 Python 自带的"打印"功能，能把括号里的内容显示在屏幕上
- `"Hello world!"` 是一段文字（字符串），用引号括起来
- Python 从上往下执行，看到这行就立刻执行

---

## 二、使用变量

```python
# 把文字存进变量 message
message = "Hello Python world!"

# 打印变量的内容
print(message)

# 输出：
# Hello Python world!
```

**类比：** 就像你先在纸上写下一段话（赋值），然后把纸递给朋友看（打印）。

---

## 三、多条消息

Python 会**从上往下**依次执行每一行代码：

```python
# 第一行：存一段话
message = "Hello Python world!"
# 第二行：打印它
print(message)

# 第三行：改成另一段话
message = "Hello Python Crash Course world!"
# 第四行：再打印
print(message)

# 输出：
# Hello Python world!
# Hello Python Crash Course world!
```

**注意：** 同一个变量可以被反复赋值，每次赋值后旧的值就被新的值替换了。

---

## 四、从终端运行

写好代码后，需要在终端（命令行）中运行：

```bash
# Linux / Mac
python hello_world.py

# Windows
python hello_world.py

# 如果系统装了多个版本的 Python，用 python3 指定版本
python3 hello_world.py
```

**运行后会看到：**
```
Hello world!
```

---

## 五、常见错误

### 错误 1：忘记加引号

```python
# ❌ 没有引号，Python 以为 Hello 是变量名
print(Hello)

# 输出：
# NameError: name 'Hello' is not defined
# 翻译：Python 找不到叫 "Hello" 的变量
```

**原因：** 没有引号的 `Hello` 会被当成变量名，但你没有定义过这个变量。

### 错误 2：引号不匹配

```python
# ❌ 开头用双引号，结尾用单引号
print("Hello')

# 输出：
# SyntaxError: EOL while scanning string literal
# 翻译：Python 在读字符串时遇到了意外的结尾
```

**原因：** Python 要求引号必须配对——双引号对双引号，单引号对单引号。

### 错误 3：函数名拼写错误

```python
# ❌ 把 print 拼成了 primt
primt("Hello")

# 输出：
# NameError: name 'primt' is not defined
# 翻译：Python 找不到叫 "primt" 的函数
```

**原因：** Python 区分大小写，`print` 和 `primt` 对它来说是两个完全不同的东西。

---

## 总结

| 概念 | 说明 | 类比 |
|------|------|------|
| `print()` | 在屏幕上显示内容 | 说话 |
| 字符串 `""` | 用引号括起来的文字 | 写在纸上的字 |
| 变量 | 给值起个名字 | 贴了标签的盒子 |
| 运行程序 | 在终端输入命令 | 按下启动按钮 |

---

## 相关笔记

- [[Python环境搭建]] — 安装 Python
- [[变量]] — 存储数据

---

*由奶茶一号整理 🧋*
