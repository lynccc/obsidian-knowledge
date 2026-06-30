---
aliases: [for循环, 遍历, 循环]
tags: [技术, Python, 基础, 流程控制]
created: 2026-06-25 01:43
updated: 2026-06-30 01:40
source: Python编程：从入门到实践
related: [[12-列表基础]], [[11-切片]], [[08-while循环]]
difficulty: 入门
status: 完成
review: 2026-07-07
---

# 🔁 Python for 循环

## 核心概念

`for` 循环 = **把列表中的每个元素都"过一遍"**

类比：**for 循环就像老师点名** —— 从名单上的第一个人开始，一个一个叫名字，直到最后一个。

（如果你熟悉 [[08-while循环]]，可以对比学习：for 循环适合"已知次数"的循环，while 循环适合"未知次数"的循环）

```python
for 每个元素 in 列表:
    对每个元素做的事
```

**⚠️ 注意：** 冒号 `:` 和缩进（4个空格）不能少！

---

## 一、基本用法

```python
# 创建一个魔术师列表
magicians = ['alice', 'david', 'carolina']

# 对列表中的每个魔术师，执行下面的操作
for magician in magicians:
    print(magician.title() + ", that was a great trick!")

# 输出：
# Alice, that was a great trick!
# David, that was a great trick!
# Carolina, that was a great trick!
```

**逐行解释：**
1. `for magician in magicians:` — 从列表中取出第一个元素，放进 `magician` 变量
2. `print(...)` — 对这个元素执行操作
3. 回到第 1 步，取出下一个元素，直到列表中没有更多元素

（这里的 `magicians` 是一个 [[12-列表基础|列表]]，如果还不熟悉列表，可以先看 [[12-列表基础]]）

**类比：** 就像老师拿着名单，叫到一个同学的名字（`magician`），对他说一句话（`print`），然后叫下一个同学。

---

## 二、循环中执行多条操作

```python
magicians = ['alice', 'david', 'carolina']

for magician in magicians:
    print(magician.title() + ", that was a great trick!")       # 第 1 条操作
    print("I can't wait to see your next trick, " + magician.title() + ".\n")  # 第 2 条操作

# 输出：
# Alice, that was a great trick!
# I can't wait to see your next trick, Alice.
#
# David, that was a great trick!
# I can't wait to see your next trick, David.
#
# Carolina, that was a great trick!
# I can't wait to see your next trick, Carolina.
```

**注意：** 循环体里的所有代码（缩进的部分）都会对每个元素执行一遍。

---

## 三、循环后执行操作

```python
magicians = ['alice', 'david', 'carolina']

for magician in magicians:
    print(magician.title() + ", that was a great trick!")

# 这行代码在循环结束后才执行（没有缩进）
print("Thank you, everyone! That was a great magic show!")

# 输出：
# Alice, that was a great trick!
# David, that was a great trick!
# Carolina, that was a great trick!
# Thank you, everyone! That was a great magic show!
```

**关键：** 缩进决定代码属于循环内还是循环外。有缩进 → 循环内（每个元素执行一次）；无缩进 → 循环外（只执行一次）。

---

## 四、数值范围

### 📌 先认识：range() — 生成一串数字

（[[range函数|range()]] 是 Python 的内置函数，常用于 for 循环中）

```python
# range(1, 5) 生成 1, 2, 3, 4（不包含 5）
for value in range(1, 5):
    print(value)

# 输出：
# 1
# 2
# 3
# 4
```

**`range(起始, 结束)` = 从起始数到结束数（不包含结束）。** 就像数数："1、2、3、4"（数到 5 停下，但不说 5）。

### 📌 先认识：list() — 把 range 转成列表

```python
# 把 range(1, 6) 转成列表
numbers = list(range(1, 6))
print(numbers)

# 输出：
# [1, 2, 3, 4, 5]
```

### 指定步长

```python
# range(2, 11, 2) 从 2 开始，每次加 2，到 11 停下
even_numbers = list(range(2, 11, 2))
print(even_numbers)

# 输出：
# [2, 4, 6, 8, 10]
```

**`range(2, 11, 2)` = 从 2 开始，每次跳 2 步：2、4、6、8、10。** 就像数偶数。

---

## 五、列表解析（一行创建列表）

列表解析 = **用一行代码创建一个列表**

（列表解析的详细用法，参见 [[列表解析]]）

```python
# 普通写法（需要 3 行）
squares = []
for value in range(1, 6):
    squares.append(value ** 2)

# 列表解析（只需要 1 行）
squares = [value ** 2 for value in range(1, 11)]
print(squares)

# 输出：
# [1, 4, 9, 16, 25, 36, 49, 64, 81, 100]
```

**`[对每个元素做的事 for 每个元素 in 范围]`** = 对范围中的每个元素执行操作，把结果收集到一个新列表中。

**类比：** 就像"批量加工" —— 你告诉工厂"对每个苹果都削皮"，工厂一次性把所有苹果都削好，装进箱子里。

---

## 六、常见错误

### 错误 1：忘记缩进

```python
for magician in magicians:
print(magician)   # ❌ 没有缩进

# 输出：
# IndentationError: expected an indented block
# 翻译：需要缩进
```

（关于 Python 的缩进规则，详见 [[Python缩进规则]]）

### 错误 2：忘记冒号

```python
for magician in magicians    # ❌ 没有冒号
    print(magician)

# 输出：
# SyntaxError: invalid syntax
# 翻译：语法错误
```

### 错误 3：不必要的缩进

```python
message = "Hello"
    print(message)   # ❌ 这行不在循环里，不应该缩进

# 输出：
# IndentationError: unexpected indent
# 翻译：意外的缩进
```

---

## 总结

| 概念 | 说明 | 类比 | 相关笔记 |
|------|------|------|----------|
| `for 元素 in 列表:` | 遍历列表中的每个元素 | 老师点名 | [[12-列表基础]] |
| `range(1, 5)` | 生成 1 到 4 的数字 | 数数（1、2、3、4） | [[range函数]] |
| `list(range(...))` | 把 range 转成列表 | 把数出来的数字记在纸上 | [[12-列表基础]] |
| 列表解析 | 一行创建列表 | 批量加工 | [[列表解析]] |
| 缩进 | 定义循环体 | 属于循环内的代码 | [[Python缩进规则]] |
| 冒号 `:` | 循环的标志 | "开始"的信号 | [[Python语法基础]] |

---

## 相关笔记

- [[12-列表基础]] — 创建和访问列表
- [[11-切片]] — 列表的一部分
- [[08-while循环]] — 条件循环
- [[range函数]] — 生成数字范围
- [[列表解析]] — 快速创建列表
- [[Python缩进规则]] — Python 的缩进语法
- [[Python语法基础]] — Python 基础语法

---

*由奶茶一号整理 🧋 | 更新：2026-06-30 01:40*
