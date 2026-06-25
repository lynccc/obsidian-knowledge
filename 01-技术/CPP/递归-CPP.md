---
tags: [C++, 函数, 递归]
aliases: [递归函数, C++递归]
created: 2026-06-25
---

# 🔄 递归 — C++

## 核心概念

- 递归（Recursion）：函数调用自身
- 必须有**基准情况**（终止条件）防止无限递归
- 适合处理树形结构、分治问题

## 基本示例

```cpp
// 阶乘：n! = n * (n-1)!
int factorial(int n) {
    if (n <= 1) return 1;       // 基准情况
    return n * factorial(n - 1); // 递归调用
}

// 斐波那契数列
int fibonacci(int n) {
    if (n <= 1) return n;
    return fibonacci(n - 1) + fibonacci(n - 2);
}
```

## 递归执行过程

```
factorial(4)
= 4 * factorial(3)
= 4 * 3 * factorial(2)
= 4 * 3 * 2 * factorial(1)
= 4 * 3 * 2 * 1
= 24
```

## 递归 vs 迭代

```cpp
// 递归版
int sum_recursive(int n) {
    if (n == 0) return 0;
    return n + sum_recursive(n - 1);
}

// 迭代版（更高效）
int sum_iterative(int n) {
    int sum = 0;
    for (int i = 1; i <= n; i++) sum += i;
    return sum;
}
```

## 注意事项

- 每次递归调用都会占用栈空间
- 递归太深会导致**栈溢出**（Stack Overflow）
- 可用**尾递归优化**或改为迭代

## 相关笔记

- [[函数基础-CPP]] — 函数基础
- [[递归]] — 递归概念详解（数据结构笔记）

---

*由奶茶一号整理 🧋*
