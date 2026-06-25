---
tags: [数据结构, Python, Miller, 数论, 密码学, RSA]
aliases: [RSA加密, 同余定理, 快速幂取模, 扩展欧几里得算法]
---

# RSA加密与数论

## 核心概念

RSA公钥加密算法建立在数论基础之上，核心思想是：某些数学运算正向容易、逆向困难。

### 同余定理

若 `a ≡ b (mod m)` 且 `c ≡ d (mod m)`，则：
- `a + c ≡ b + d (mod m)`
- `a × c ≡ b × d (mod m)`

这意味着**可以在每一步取模**，避免大数溢出。

### 快速幂取模

朴素计算 `b^n mod m` 需要 O(n) 次乘法。利用**平方-乘法**策略可降至 O(log n)：

```python
def fast_power(base, exp, mod):
    """快速幂取模: base^exp mod mod"""
    result = 1
    base = base % mod
    while exp > 0:
        if exp % 2 == 1:        # 指数为奇数
            result = (result * base) % mod
        exp = exp >> 1           # 指数减半
        base = (base * base) % mod  # 底数平方
    return result
```

### 扩展欧几里得算法

求 `gcd(a, b)` 及满足 `ax + by = gcd(a, b)` 的整数 x, y。这是求**模逆元**的基础。

```python
def extended_gcd(a, b):
    if b == 0:
        return a, 1, 0
    else:
        gcd, x, y = extended_gcd(b, a % b)
        return gcd, y, x - (a // b) * y
```

### RSA算法流程

1. 选两个大素数 p, q，计算 `n = p × q`
2. 计算 `φ(n) = (p-1)(q-1)`
3. 选 e 使得 `gcd(e, φ(n)) = 1`（公钥指数）
4. 求 d 使得 `e × d ≡ 1 (mod φ(n))`（私钥指数）
5. **加密**：`c = m^e mod n`，**解密**：`m = c^d mod n`

## 关键要点

- 安全性基于**大整数分解困难**：知道 n 很难分解出 p 和 q
- 快速幂取模是核心工具，贯穿加解密过程
- 扩展欧几里得是求私钥 d 的关键

## 与其他概念的联系

- [[递归基础]] — 扩展欧几里得算法是递归的经典应用
- [[递归应用]] — 更多递归实例
- [[散列Python]] — 哈希函数也涉及取模运算
- [[Python数据类型概览]] — Python 原生支持大整数，无需额外库

## 参考
- 《Python数据结构与算法分析》第2版 §8.3
