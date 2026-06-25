---
tags: [数据结构, Python, Miller, 动态规划, 递归]
aliases: [Fibonacci优化, 背包问题, Dynamic Programming]
---

# 动态规划（Python）

## 🗣️ 通俗讲解

> 核心思想就是「记住已经算过的答案」。就像做数学题时把中间步骤写在草稿纸上，下次遇到同样的子问题直接抄答案，不用重新算。斐波那契数列是最经典的例子：朴素递归慢得要死（指数级），加个缓存就变线性了。

📖 **想看更深入的理论分析？** → [[动态规划与记忆化]]（邓俊辉 C++ 版）

## 核心概念

动态规划（Dynamic Programming, DP）是优化递归问题的技术，核心思想是**避免重复计算**。当递归函数多次计算相同的子问题时，使用缓存（记忆化）存储已计算的结果。

## Fibonacci 数列：从低效到高效

### 朴素递归（指数级）

```python
def fib(n):
    if n == 0: return 0
    if n == 1: return 1
    return fib(n - 1) + fib(n - 2)
```

**问题**：`fib(5)` 重复计算 `fib(3)` 两次、`fib(2)` 三次。时间复杂度 **O(2ⁿ)**。

### 记忆化递归（自顶向下）

```python
def fib_memo(n, memo=None):
    if memo is None:
        memo = {}
    if n in memo:
        return memo[n]
    if n == 0: return 0
    if n == 1: return 1
    memo[n] = fib_memo(n - 1, memo) + fib_memo(n - 2, memo)
    return memo[n]
```

时间复杂度降为 **O(n)**。

### 迭代 DP（自底向上）

```python
def fib_dp(n):
    if n == 0: return 0
    dp = [0] * (n + 1)
    dp[1] = 1
    for i in range(2, n + 1):
        dp[i] = dp[i - 1] + dp[i - 2]
    return dp[n]
```

空间可进一步优化为 O(1)（只保留前两个值）。

## 背包问题（0/1 Knapsack）

给定背包容量 W 和 n 个物品（各有重量和价值），求最大价值。

```python
def knapsack(weights, values, W):
    n = len(weights)
    # dp[i][w] = 前 i 个物品、容量 w 时的最大价值
    dp = [[0] * (W + 1) for _ in range(n + 1)]

    for i in range(1, n + 1):
        for w in range(W + 1):
            dp[i][w] = dp[i - 1][w]  # 不选第 i 个
            if weights[i - 1] <= w:
                # 选第 i 个
                dp[i][w] = max(dp[i][w],
                    dp[i - 1][w - weights[i - 1]] + values[i - 1])
    return dp[n][W]
```

- 时间复杂度：**O(nW)**
- 空间复杂度：**O(nW)**（可优化为 O(W)）

## 动态规划 vs 递归

| 特性 | 朴素递归 | 记忆化递归 | 迭代 DP |
|------|---------|-----------|---------|
| 方向 | 自顶向下 | 自顶向下 | 自底向上 |
| 重复计算 | 有 | 无 | 无 |
| 空间 | O(栈深度) | O(n) + 缓存 | O(n) |
| 实现 | 最简单 | 较简单 | 需要状态定义 |

## 关键要点

- 动态规划的两个条件：**最优子结构** + **重叠子问题**
- 记忆化（memoization）是最简单的优化手段：加个字典缓存
- Python 可用 `functools.lru_cache` 装饰器实现自动记忆化
- 背包问题展示了二维 DP 表的构建思路

## 与其他概念的联系

- [[递归基础]] — 理解递归是学习动态规划的前提
- [[递归应用]] — 递归问题的优化路径
- [[动态规划与记忆化]] — 邓俊辉版对 DP 的更深入讨论

## 参考
- 《Python数据结构与算法分析》第2版 §4.7
