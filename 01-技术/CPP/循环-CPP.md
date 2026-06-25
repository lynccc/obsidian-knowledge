---
tags: [C++, 循环, 控制流]
aliases: [for循环, while循环, do-while]
created: 2026-06-25
---

# 🔁 循环 — C++

## 核心概念

- `for`：已知循环次数时使用
- `while`：条件为真时持续执行
- `do-while`：至少执行一次
- `break` 跳出循环，`continue` 跳过本次

## for 循环

```cpp
// 经典 for
for (int i = 0; i < 5; i++) {
    std::cout << i << " ";  // 0 1 2 3 4
}

// 递减
for (int i = 10; i > 0; i--) {
    std::cout << i << " ";
}
```

## while 循环

```cpp
int count = 0;
while (count < 5) {
    std::cout << count << " ";
    count++;
}
```

## do-while 循环

```cpp
int num;
do {
    std::cout << "输入正数: ";
    std::cin >> num;
} while (num <= 0);  // 至少执行一次
```

## break 和 continue

```cpp
// break — 跳出整个循环
for (int i = 0; i < 10; i++) {
    if (i == 5) break;      // 到 5 停止
    std::cout << i << " ";  // 0 1 2 3 4
}

// continue — 跳过本次迭代
for (int i = 0; i < 5; i++) {
    if (i == 2) continue;   // 跳过 2
    std::cout << i << " ";  // 0 1 3 4
}
```

## 范围 for（C++11）

```cpp
std::vector<int> nums = {1, 2, 3, 4, 5};
for (int n : nums) {
    std::cout << n << " ";
}

for (const auto& s : {"hello", "world"}) {
    std::cout << s << " ";
}
```

## 无限循环

```cpp
while (true) {
    // 需要 break 退出
}

for (;;) { }  // 等价写法
```

## 相关笔记

- [[if语句-CPP]] — 条件判断
- [[运算符]] — 关系运算符
- [[范围for]] — 范围 for 详解

---

*由奶茶一号整理 🧋*
