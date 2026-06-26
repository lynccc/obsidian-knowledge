---
aliases: [while, 条件循环]
tags: [技术, Python, 基础, 流程控制]
created: 2026-06-25 01:46
updated: 2026-06-26 16:05
source: Python编程：从入门到实践
related: [[for循环]], [[用户输入]], [[列表基础]]
---

# 🔄 Python while 循环

## 核心概念

`while` 循环 = **当条件满足时，一直做某件事**

```python
while 条件:
    要做的事
```

类比：**"只要水没烧开，就一直等"**

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

---

## 二、让用户选择退出

```python
prompt = "\n跟我说点什么，我会复述给你："
prompt += "\n输入 'quit' 退出程序。"

message = ""                        # 先给 message 一个空值

while message != 'quit':            # 只要用户没输入 quit，就继续
    message = input(prompt)         # 获取用户输入
    if message != 'quit':           # 如果不是 quit
        print(message)              # 就打印出来

# 运行效果：
# 跟我说点什么，我会复述给你：
# 输入 'quit' 退出程序。
# > hello
# hello
# > quit
# （程序结束，没有打印 quit）
```

---

## 三、使用标志（flag）

当有**多个条件**可能结束循环时，用一个变量作为"开关"：

```python
active = True                       # 标志 = True 表示"程序在运行"

while active:                       # 只要 active 是 True，就继续
    message = input("说点什么：")

    if message == 'quit':           # 用户输入 quit
        active = False              # 把标志改成 False → 循环结束
    else:
        print(message)              # 否则打印消息

# active = True  → while active → 条件成立 → 继续循环
# active = False → while active → 条件不成立 → 退出循环
```

---

## 四、break 立即退出

`break` = **立刻停止，不管条件是什么**

```python
while True:                         # 条件永远为 True（无限循环）
    city = input("你去过哪个城市？输入 quit 退出：")

    if city == 'quit':
        break                       # 立刻退出循环

    print("我也想去 " + city + "！")

# 运行效果：
# 你去过哪个城市？输入 quit 退出：> 北京
# 我也想去 北京！
# 你去过哪个城市？输入 quit 退出：> quit
# （程序立刻结束）
```

---

## 五、continue 跳过本次

`continue` = **跳过这次循环的剩余代码，回到循环开头**

```python
current_number = 0

while current_number < 10:
    current_number += 1             # 先加 1（变成 1, 2, 3, ...）

    if current_number % 2 == 0:     # 如果是偶数（% 是取余数）
        continue                    # 跳过下面的 print，回到 while 重新判断

    print(current_number)           # 只有奇数才会执行到这里

# 输出：
# 1
# 3
# 5
# 7
# 9
```

**执行流程（以 current_number = 2 为例）：**
```
current_number = 2
→ 2 % 2 == 0 ？ → 是偶数 → continue → 跳过 print → 回到 while 判断
→ 不会打印 2！
```

---

## 六、处理列表（重点！）

在学这部分之前，先认识两个**列表方法**：

### 📌 先认识：append() — 在列表末尾添加元素

```python
fruits = ['苹果', '香蕉']
fruits.append('橘子')               # 在末尾添加 '橘子'
print(fruits)

# 输出：['苹果', '香蕉', '橘子']
```

### 📌 先认识：pop() — 取出列表末尾的元素

```python
fruits = ['苹果', '香蕉', '橘子']
last_fruit = fruits.pop()           # 取出末尾的 '橘子'，列表里就没有它了
print(last_fruit)
print(fruits)

# 输出：
# 橘子
# ['苹果', '香蕉']
```

**`pop()` = 取走最后一个 → 列表变短了**

### 📌 先认识：remove() — 删除指定元素

```python
pets = ['狗', '猫', '鱼', '猫']
pets.remove('猫')                   # 删除第一个找到的 '猫'
print(pets)

# 输出：['狗', '鱼', '猫']（只删了第一个猫，第二个还在）
```

---

### 实战 1：在列表间移动元素

**场景：** 把"未确认用户"逐个移到"已确认用户"

```python
unconfirmed_users = ['alice', 'brian', 'candace']   # 未确认的用户
confirmed_users = []                                  # 已确认的用户（开始是空的）

# 只要未确认列表不为空，就继续循环
while unconfirmed_users:

    # pop() 从末尾取出一个用户 → 列表里就没有这个人了
    current_user = unconfirmed_users.pop()

    print("正在验证用户：" + current_user)

    # append() 把这个人加到已确认列表的末尾
    confirmed_users.append(current_user)

# 循环结束后，看看两个列表
print("\n未确认用户：", unconfirmed_users)   # 空了！
print("已确认用户：", confirmed_users)

# 输出：
# 正在验证用户：candace
# 正在验证用户：brian
# 正在验证用户：alice
#
# 未确认用户： []
# 已确认用户： ['candace', 'brian', 'alice']
```

**每一步发生了什么：**

```
第 1 次循环：
  unconfirmed_users = ['alice', 'brian', 'candace']
  pop() 取出 'candace' → unconfirmed_users 变成 ['alice', 'brian']
  append('candace') → confirmed_users 变成 ['candace']

第 2 次循环：
  unconfirmed_users = ['alice', 'brian']
  pop() 取出 'brian' → unconfirmed_users 变成 ['alice']
  append('brian') → confirmed_users 变成 ['candace', 'brian']

第 3 次循环：
  unconfirmed_users = ['alice']
  pop() 取出 'alice' → unconfirmed_users 变成 []
  append('alice') → confirmed_users 变成 ['candace', 'brian', 'alice']

第 4 次：unconfirmed_users 是空列表 → while 条件不成立 → 循环结束！
```

**💡 空列表在 while 条件中 = False，非空列表 = True**

---

### 实战 2：删除列表中所有指定值

**场景：** 把列表里所有的 '猫' 都删掉

```python
pets = ['狗', '猫', '狗', '金鱼', '猫', '兔子', '猫']
print("删除前：", pets)

while '猫' in pets:                 # 只要列表里还有 '猫'，就继续
    pets.remove('猫')               # 删除找到的第一个 '猫'

print("删除后：", pets)

# 输出：
# 删除前： ['狗', '猫', '狗', '金鱼', '猫', '兔子', '猫']
# 删除后： ['狗', '狗', '金鱼', '兔子']
```

**每一步发生了什么：**

```
第 1 次：列表里有 '猫'？ → 有 → remove 删掉第 1 个猫
  ['狗', '猫', '狗', '金鱼', '猫', '兔子', '猫']
       ↑ 删这个
  → ['狗', '狗', '金鱼', '猫', '兔子', '猫']

第 2 次：列表里有 '猫'？ → 有 → remove 删掉第 1 个猫
  ['狗', '狗', '金鱼', '猫', '兔子', '猫']
                    ↑ 删这个
  → ['狗', '狗', '金鱼', '兔子', '猫']

第 3 次：列表里有 '猫'？ → 有 → remove 删掉第 1 个猫
  ['狗', '狗', '金鱼', '兔子', '猫']
                                 ↑ 删这个
  → ['狗', '狗', '金鱼', '兔子']

第 4 次：列表里有 '猫'？ → 没有了 → 循环结束！
```

**⚠️ 为什么用 while 而不是 for？**

```python
# ❌ 用 for 循环删元素会有 bug！
pets = ['狗', '猫', '狗', '金鱼', '猫', '兔子', '猫']
for pet in pets:
    if pet == '猫':
        pets.remove(pet)    # 删元素的同时在遍历列表 → 会跳过某些元素！
print(pets)
# 输出可能是：['狗', '狗', '金鱼', '兔子', '猫'] → 没删干净！

# ✅ while 循环每次从头检查，不会遗漏
```

---

## 总结

| 关键词 | 作用 | 类比 |
|--------|------|------|
| `while` | 条件满足就一直做 | 只要水没开就一直等 |
| `break` | 立刻停止 | 听到闹钟立刻停手 |
| `continue` | 跳过这次，做下一次 | 这题不会，跳过做下一题 |
| `append()` | 在末尾加东西 | 往书架末尾放一本书 |
| `pop()` | 取出末尾的东西 | 从书架末尾拿走一本书 |
| `remove()` | 删除指定的东西 | 从书架上拿走某一本书 |

---

## 相关笔记

- [[for循环]] — 遍历循环
- [[用户输入]] — 获取输入
- [[条件测试]] — 条件判断
- [[列表基础]] — 列表的基本操作

---

*由奶茶一号整理 🧋*
