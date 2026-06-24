---
aliases: [if, 条件分支, if-else]
tags: [技术, Python, 基础, 流程控制]
created: 2026-06-25 01:44
source: Python编程：从入门到实践
related: [[条件测试]], [[for循环]]
---

# 🔀 Python if 语句

## 核心概念

- `if` — 条件满足时执行
- `if-else` — 二选一
- `if-elif-else` — 多选一
- 缩进和冒号很重要

## 简单 if

```python
age = 19
if age >= 18:
    print("You are old enough to vote!")
```

## if-else

```python
age = 17
if age >= 18:
    print("You are old enough to vote!")
else:
    print("Sorry, you are too young to vote.")
```

## if-elif-else

```python
age = 12
if age < 4:
    print("Your admission cost is $0.")
elif age < 18:
    print("Your admission cost is $25.")
else:
    print("Your admission cost is $40.")
```

## 多个 elif

```python
age = 12
if age < 4:
    price = 0
elif age < 18:
    price = 25
elif age < 65:
    price = 40
else:
    price = 20
print("Your admission cost is $" + str(price) + ".")
```

## 省略 else

```python
age = 12
if age < 4:
    price = 0
elif age < 18:
    price = 25
elif age < 65:
    price = 40
elif age >= 65:
    price = 20
# 没有 else，但覆盖了所有情况
```

## 测试多个条件

```python
requested_toppings = ['mushrooms', 'extra cheese']
if 'mushrooms' in requested_toppings:
    print("Adding mushrooms.")
if 'pepperoni' in requested_toppings:
    print("Adding pepperoni.")
if 'extra cheese' in requested_toppings:
    print("Adding extra cheese.")
```

## 处理列表

```python
# 检查特殊元素
requested_toppings = ['mushrooms', 'green peppers', 'extra cheese']
for topping in requested_toppings:
    if topping == 'green peppers':
        print("Sorry, we are out of green peppers right now.")
    else:
        print("Adding " + topping + ".")

# 检查列表是否为空
requested_toppings = []
if requested_toppings:
    for topping in requested_toppings:
        print("Adding " + topping + ".")
else:
    print("Are you sure you want a plain pizza?")
```

## 相关笔记

- [[条件测试]] — 比较和判断
- [[for循环]] — 循环遍历

---

*由奶茶一号整理 🧋*
