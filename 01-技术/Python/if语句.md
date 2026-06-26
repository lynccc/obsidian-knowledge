---
aliases: [if, 条件分支, if-else]
tags: [技术, Python, 基础, 流程控制]
created: 2026-06-25 01:44
updated: 2026-06-26 16:12
source: Python编程：从入门到实践
related: [[条件测试]], [[for循环]]
---

# 🔀 Python if 语句

## 核心概念

`if` 语句 = **根据条件决定做什么事**

类比：**if 语句就像岔路口** —— 你站在路口，根据路标（条件）决定走哪条路。

```python
if 条件:
    条件成立时做的事
else:
    条件不成立时做的事
```

**⚠️ 注意：** 冒号 `:` 和缩进（4个空格）不能少！

---

## 一、简单 if

只有条件成立时才执行：

```python
age = 19

# 如果 age 大于等于 18，就执行下面的代码
if age >= 18:
    print("You are old enough to vote!")

# 输出：
# You are old enough to vote!
```

**逐行解释：**
1. `age = 19` — 把 19 存进 age 变量
2. `if age >= 18:` — 判断：19 >= 18 吗？→ 是的 → 条件成立
3. `print(...)` — 条件成立，执行这行代码

---

## 二、if-else（二选一）

条件成立做一件事，不成立做另一件事：

```python
age = 17

if age >= 18:
    print("You are old enough to vote!")      # 条件成立 → 执行这行
else:
    print("Sorry, you are too young to vote.")  # 条件不成立 → 执行这行

# 输出：
# Sorry, you are too young to vote.
```

**类比：** 就像"如果下雨，就带伞；否则，就不带伞"。两种情况选一种。

---

## 三、if-elif-else（多选一）

有多个条件时，按顺序检查，执行第一个成立的：

```python
age = 12

if age < 4:
    print("Your admission cost is $0.")       # age < 4 → 不成立（12 不小于 4）
elif age < 18:
    print("Your admission cost is $25.")      # age < 18 → 成立！执行这行
else:
    print("Your admission cost is $40.")      # 不会执行（因为上面已经匹配了）

# 输出：
# Your admission cost is $25.
```

**执行流程：**
1. 检查 `age < 4` → 12 < 4？→ 不成立 → 跳过
2. 检查 `age < 18` → 12 < 18？→ 成立！→ 执行 print
3. `else` 不需要检查了（已经找到匹配的条件）

**类比：** 就像医院挂号 —— "你是儿童吗？不是。你是学生吗？是的。好，给你学生票。"

---

## 四、多个 elif

```python
age = 12

if age < 4:
    price = 0           # 4 岁以下免费
elif age < 18:
    price = 25          # 4-17 岁 $25
elif age < 65:
    price = 40          # 18-64 岁 $40
else:
    price = 20          # 65 岁以上 $20

print("Your admission cost is $" + str(price) + ".")

# 输出：
# Your admission cost is $25.
```

**`elif` = "否则如果"**，用来检查多个条件。

---

## 五、省略 else

有时候不需要 `else`，因为所有情况都用 `elif` 覆盖了：

```python
age = 12

if age < 4:
    price = 0
elif age < 18:
    price = 25
elif age < 65:
    price = 40
elif age >= 65:       # 最后一个条件，覆盖了所有剩余情况
    price = 20

print("Your admission cost is $" + str(price) + ".")

# 输出：
# Your admission cost is $25.
```

---

## 六、测试多个条件

有时候需要检查多个独立的条件（不是 elif 那种"只执行一个"的逻辑）：

```python
requested_toppings = ['mushrooms', 'extra cheese']

# 每个 if 都会独立检查
if 'mushrooms' in requested_toppings:
    print("Adding mushrooms.")         # ✅ 执行

if 'pepperoni' in requested_toppings:
    print("Adding pepperoni.")         # ❌ 不执行（没有 pepperoni）

if 'extra cheese' in requested_toppings:
    print("Adding extra cheese.")      # ✅ 执行

# 输出：
# Adding mushrooms.
# Adding extra cheese.
```

**elif vs 多个 if 的区别：**
- `elif`：只执行第一个匹配的（互斥）
- 多个 `if`：每个都会独立检查（可能多个都执行）

---

## 七、处理列表

### 检查列表中的特殊元素

```python
requested_toppings = ['mushrooms', 'green peppers', 'extra cheese']

for topping in requested_toppings:
    if topping == 'green peppers':
        print("Sorry, we are out of green peppers right now.")  # 特殊处理
    else:
        print("Adding " + topping + ".")   # 正常处理

# 输出：
# Adding mushrooms.
# Sorry, we are out of green peppers right now.
# Adding extra cheese.
```

### 检查列表是否为空

```python
requested_toppings = []

# 空列表在 if 条件中 = False
if requested_toppings:
    for topping in requested_toppings:
        print("Adding " + topping + ".")
else:
    print("Are you sure you want a plain pizza?")

# 输出：
# Are you sure you want a plain pizza?
```

**💡 关键知识：**
- 空列表 `[]` 在 if 条件中 = **False**（假）
- 非空列表在 if 条件中 = **True**（真）

**类比：** 就像问"购物车里有东西吗？" —— 空购物车 = 没有 = False；有东西的购物车 = 有 = True。

---

## 总结

| 语法 | 含义 | 类比 |
|------|------|------|
| `if` | 如果 | "如果下雨" |
| `elif` | 否则如果 | "否则如果下雪" |
| `else` | 否则 | "否则（其他情况）" |
| `:` | 代码块开始 | "那么" |
| 缩进 | 属于这个条件的代码 | 条件成立时做的事 |
| 空列表 | False | 购物车是空的 |
| 非空列表 | True | 购物车里有东西 |

---

## 相关笔记

- [[条件测试]] — 比较和判断
- [[for循环]] — 循环遍历

---

*由奶茶一号整理 🧋*
