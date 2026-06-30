---
aliases: [while, 条件循环]
tags: [技术, Python, 基础, 流程控制]
created: 2026-06-25 01:46
updated: 2026-06-30 01:45
source: Python编程：从入门到实践
related: [[06-for循环]], [[29-用户输入]], [[12-列表基础]]
difficulty: 入门
status: 完成
review: 2026-07-07
---

# 🔄 Python while 循环

## 核心概念

`while` 循环 = **当条件满足时，一直做某件事**

```python
while 条件:
    要做的事
```

类比：**"只要水没烧开，就一直等"**

（如果你熟悉 [[06-for循环]]，可以对比学习：while 循环适合"未知次数"的循环，for 循环适合"已知次数"的循环）

---

## 一、基本用法

```python
# 目标：打印 1 到 5

current_number = 1              # 从 1 开始

while current_number <= 5:      # 只要 current_number <= 5，就继续循环
    print(current_number)       # 打印当前数字
    current_number += 1         # 数字加 1（等同于 current_number = current_number + 1）

# 输出：
# 1
# 2
# 3
# 4
# 5
```

**⚠️ 如果忘记写 `current_number += 1`，数字永远是 1，条件永远满足，变成无限循环！**

（避免无限循环的方法：确保循环体内有"改变条件"的代码，详见 [[无限循环调试]]）

---

## 二、让用户选择退出

```python
prompt = "\nTell me something, and I will repeat it back to you:"
prompt += "\nEnter 'quit' to end the program. "

message = ""                    # 先设一个空字符串

while message != 'quit':        # 只要输入的不是 'quit'，就继续循环
    message = input(prompt)     # 让用户输入
    if message != 'quit':       # 如果输入的不是 'quit'
        print(message)          # 打印用户输入的内容

# 运行效果：
# Tell me something, and I will repeat it back to you:
# Enter 'quit' to end the program. Hello!
# Hello!
# Tell me something, and I will repeat it back to you:
# Enter 'quit' to end the program. quit
# （程序结束）
```

**关键点：**
1. 先定义一个「退出条件」（`message != 'quit'`）
2. 在循环里检查用户输入，如果满足退出条件，就退出循环

（这里的 `input()` 函数详见 [[29-用户输入]]）

---

## 三、用标志（flag）控制循环

```python
prompt = "\nTell me something, and I will repeat it back to you:"
prompt += "\nEnter 'quit' to end the program. "

active = True                    # 标志：程序是否在运行

while active:                   # 只要 active 是 True，就继续循环
    message = input(prompt)
    
    if message == 'quit':       # 如果用户输入 'quit'
        active = False          # 把标志设为 False，下次循环就会退出
    else:                       # 否则
        print(message)

# 运行效果：同上
```

**标志（flag）= 一个开关** —— 可以是 `True`（开）或 `False`（关）。当开关是 `True` 时，循环继续；当开关是 `False` 时，循环结束。

类比：**就像电灯开关** —— 打开开关（`active = True`），灯亮（循环继续）；关闭开关（`active = False`），灯灭（循环结束）。

---

## 四、用 break 退出循环

```python
prompt = "\nTell me something, and I will repeat it back to you:"
prompt += "\nEnter 'quit' to end the program. "

while True:                      # 无限循环（因为条件永远是 True）
    message = input(prompt)
    
    if message == 'quit':        # 如果用户输入 'quit'
        break                   # 立刻退出循环（不管条件是什么）
    else:
        print(message)

# 运行效果：同上
```

**`break` = 立刻退出循环（不执行循环中剩下的代码）**

类比：**就像 fire 演习** —— 不管你在做什么，一听到警报（`break`），立刻停止手头的事，跑出去（退出循环）。

---

## 五、用 continue 跳过本次循环

```python
# 目标：打印 1 到 10 中的偶数

current_number = 0

while current_number < 10:
    current_number += 1              # 数字加 1
    
    if current_number % 2 == 0:    # 如果数字是偶数（能被 2 整除）
        continue                    # 跳过本次循环，回到循环开头
    
    print(current_number)           # 只有奇数才会执行这行

# 输出：
# 1
# 3
# 5
# 7
# 9
```

**`continue` = 跳过本次循环，回到循环开头（不执行循环中剩下的代码）**

类比：**就像跑步** —— 你跑到第 2 圈（`current_number = 2`），教练说"偶数圈不用跑"（[[取模运算|取模运算]] `%` 判断偶数），你就直接开始第 3 圈（`continue`），不跑第 2 圈。

---

## 六、避免无限循环

```python
# ❌ 错误示例：无限循环
x = 1
while x <= 5:
    print(x)
    # 忘记写 x += 1，x 永远是 1，条件永远满足，变成无限循环！

# ✅ 正确示例：确保循环有机会退出
x = 1
while x <= 5:
    print(x)
    x += 1              # 每次循环都让 x 增加 1，最终 x 会变成 6，条件不满足，循环退出
```

**避免无限循环的方法：**
1. 确保循环体内有"改变条件"的代码（如 `x += 1`）
2. 用 `break` 提供"紧急出口"
3. 在测试时，先用小范围测试（如 `while x <= 5:` 而不是 `while x <= 1000000:`）

---

## 总结

| 概念 | 说明 | 类比 | 相关笔记 |
|------|------|------|----------|
| `while 条件:` | 当条件满足时，一直做某件事 | 只要水没烧开，就一直等 | [[06-for循环]] |
| 标志（flag） | 用 `True`/`False` 控制循环 | 电灯开关 | [[布尔值]] |
| `break` | 立刻退出循环 | fire 演习 | [[循环控制语句]] |
| `continue` | 跳过本次循环 | 跑步时跳过某一圈 | [[循环控制语句]] |
| 无限循环 | 条件永远满足，循环不会退出 | 水永远烧不开 | [[无限循环调试]] |

---

## 相关笔记

- [[06-for循环]] — 已知次数的循环
- [[29-用户输入]] — input() 函数
- [[12-列表基础]] — Python 列表
- [[布尔值]] — True/False
- [[取模运算]] — 判断偶数/奇数
- [[循环控制语句]] — break 和 continue
- [[无限循环调试]] — 避免无限循环

---

*由奶茶一号整理 🧋 | 更新：2026-06-30 01:45*
