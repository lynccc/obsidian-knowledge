---
aliases: [for循环, 遍历, 循环]
tags: [技术, Python, 基础, 流程控制]
created: 2026-06-25 01:43
source: Python编程：从入门到实践
related: [[列表基础]], [[切片]], [[while循环]]
---

# 🔁 Python for 循环

## 核心概念

- `for` 循环用于遍历列表中的每个元素
- 缩进定义循环体
- 冒号 `:` 不能遗漏

## 基本用法

```python
magicians = ['alice', 'david', 'carolina']
for magician in magicians:
    print(magician.title() + ", that was a great trick!")

# 输出：
# Alice, that was a great trick!
# David, that was a great trick!
# Carolina, that was a great trick!
```

## 循环中执行多条操作

```python
magicians = ['alice', 'david', 'carolina']
for magician in magicians:
    print(magician.title() + ", that was a great trick!")
    print("I can't wait to see your next trick, " + magician.title() + ".\n")
```

## 循环后执行操作

```python
magicians = ['alice', 'david', 'carolina']
for magician in magicians:
    print(magician.title() + ", that was a great trick!")

print("Thank you, everyone! That was a great magic show!")
```

## 数值范围

```python
# range() 生成数字序列
for value in range(1, 5):
    print(value)
# 输出: 1, 2, 3, 4（不包含5）

# 创建数字列表
numbers = list(range(1, 6))
print(numbers)  # [1, 2, 3, 4, 5]

# 指定步长
even_numbers = list(range(2, 11, 2))
print(even_numbers)  # [2, 4, 6, 8, 10]
```

## 列表解析

```python
# 一行创建列表
squares = [value**2 for value in range(1, 11)]
print(squares)  # [1, 4, 9, 16, 25, 36, 49, 64, 81, 100]
```

## 常见错误

```python
# ❌ 忘记缩进
for magician in magicians:
print(magician)  # IndentationError

# ❌ 忘记冒号
for magician in magicians
    print(magician)  # SyntaxError

# ❌ 不必要的缩进
message = "Hello"
    print(message)  # IndentationError
```

## 相关笔记

- [[列表基础]] — 创建和访问列表
- [[切片]] — 列表的一部分
- [[while循环]] — 条件循环

---

*由奶茶一号整理 🧋*
