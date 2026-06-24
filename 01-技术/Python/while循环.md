---
aliases: [while, 条件循环]
tags: [技术, Python, 基础, 流程控制]
created: 2026-06-25 01:46
source: Python编程：从入门到实践
related: [[for循环]], [[用户输入]]
---

# 🔄 Python while 循环

## 核心概念

- `while` 循环在条件满足时持续执行
- `break` 立即退出循环
- `continue` 跳过本次迭代
- 避免无限循环

## 基本用法

```python
current_number = 1
while current_number <= 5:
    print(current_number)
    current_number += 1
```

## 让用户选择退出

```python
prompt = "\nTell me something, and I will repeat it back to you:"
prompt += "\nEnter 'quit' to end the program. "

message = ""
while message != 'quit':
    message = input(prompt)
    if message != 'quit':
        print(message)
```

## 使用标志

```python
active = True
while active:
    message = input(prompt)
    if message == 'quit':
        active = False
    else:
        print(message)
```

## break 退出循环

```python
prompt = "\nPlease enter the name of a city you have visited:"
prompt += "\nEnter 'quit' when you are finished. "

while True:
    city = input(prompt)
    if city == 'quit':
        break
    else:
        print("I'd love to go to " + city.title() + "!")
```

## continue 跳过迭代

```python
current_number = 0
while current_number < 10:
    current_number += 1
    if current_number % 2 == 0:
        continue
    print(current_number)
# 输出: 1, 3, 5, 7, 9
```

## 处理列表

```python
# 在列表间移动元素
unconfirmed_users = ['alice', 'brian', 'candace']
confirmed_users = []

while unconfirmed_users:
    current_user = unconfirmed_users.pop()
    print("Verifying user: " + current_user.title())
    confirmed_users.append(current_user)

# 删除特定值
pets = ['dog', 'cat', 'dog', 'goldfish', 'cat', 'rabbit', 'cat']
while 'cat' in pets:
    pets.remove('cat')
print(pets)  # ['dog', 'dog', 'goldfish', 'rabbit']
```

## 相关笔记

- [[for循环]] — 遍历循环
- [[用户输入]] — 获取输入
- [[条件测试]] — 条件判断

---

*由奶茶一号整理 🧋*
