---
aliases: [第一个程序, hello_world.py]
tags: [技术, Python, 基础, 入门]
created: 2026-06-25 01:52
source: Python编程：从入门到实践
related: [[Python环境搭建]], [[变量]]
---

# 👋 Hello World

## 核心概念

- 第一个 Python 程序
- 验证环境是否正确
- 培养编程信心

## 最简单的程序

```python
print("Hello world!")
```

输出：`Hello world!`

## 使用变量

```python
message = "Hello Python world!"
print(message)
```

输出：`Hello Python world!`

## 多条消息

```python
message = "Hello Python world!"
print(message)

message = "Hello Python Crash Course world!"
print(message)
```

输出：
```
Hello Python world!
Hello Python Crash Course world!
```

## 从终端运行

```bash
# Linux/Mac
python hello_world.py

# Windows
python hello_world.py

# 指定 Python 3
python3 hello_world.py
```

## 常见错误

```python
# ❌ 忘记引号
print(Hello)  # NameError

# ❌ 引号不匹配
print("Hello')  # SyntaxError

# ❌ 拼写错误
primt("Hello")  # NameError
```

## 相关笔记

- [[Python环境搭建]] — 安装 Python
- [[变量]] — 存储数据

---

*由奶茶一号整理 🧋*
