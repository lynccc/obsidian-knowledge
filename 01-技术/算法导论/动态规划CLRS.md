# 动态规划 (Dynamic Programming) — CLRS 第14章

> **一句话总结**：动态规划就是"记住已经算过的东西，别重复算"，把指数级暴力搜索变成多项式时间。

---

## 1. 钢条切割 (Rod Cutting)

### 问题描述

给定一根长度为 $n$ 英寸的钢条和一个价格表 $p[i]$（长度 $i$ 的钢条卖 $p[i]$ 美元），求切割方案使总收入最大。

| 长度 $i$ | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 |
|----------|---|---|---|---|---|---|---|---|---|---|
| 价格 $p_i$ | 1 | 5 | 8 | 9 | 10 | 17 | 17 | 20 | 24 | 30 |

### 递推公式

$$r_n = \max_{1 \le i \le n}(p_i + r_{n-i})$$

- $p_i$：第一段切 $i$ 的价格
- $r_{n-i}$：剩余部分的最优解
- 不切也是一种选择（$p_n$ 对应 $i = n$）

### 朴素递归 — 为什么慢？

```python
def cut_rod(p, n):
    if n == 0: return 0
    q = -inf
    for i in range(1, n+1):
        q = max(q, p[i] + cut_rod(p, n-i))
    return q
```

**时间复杂度**：$O(2^n)$ — 指数级！

> **大白话**：每次递归都在重复算同样的子问题，比如算 $r_5$ 时算了 $r_3$，算 $r_4$ 时又算了 $r_3$，白白浪费。

### 两种 DP 实现

#### 自顶向下 + 备忘录 (Top-down with Memoization)

```python
def memoized_cut_rod(p, n):
    r = [-inf] * (n+1)
    return memoized_cut_rod_aux(p, n, r)

def memoized_cut_rod_aux(p, n, r):
    if r[n] >= 0: return r[n]  # 已经算过了，直接返回
    if n == 0: q = 0
    else:
        q = -inf
        for i in range(1, n+1):
            q = max(q, p[i] + memoized_cut_rod_aux(p, n-i, r))
    r[n] = q  # 存起来
    return q
```

#### 自底向上 (Bottom-up)

```python
def bottom_up_cut_rod(p, n):
    r = [0] * (n+1)
    for j in range(1, n+1):
        q = -inf
        for i in range(1, j+1):
            q = max(q, p[i] + r[j-i])
        r[j] = q
    return r[n]
```

**两种方法时间复杂度都是 $O(n^2)$**，比朴素递归的 $O(2^n)$ 快太多了。

### 重构最优解

不仅要最优值，还要知道怎么切：额外记录数组 $s[j]$ = 长度 $j$ 时最优的第一刀位置。

```python
def extended_bottom_up_cut_rod(p, n):
    r = [0] * (n+1)
    s = [0] * (n+1)
    for j in range(1, n+1):
        q = -inf
        for i in range(1, j+1):
            if q < p[i] + r[j-i]:
                q = p[i] + r[j-i]
                s[j] = i
        r[j] = q
    return r, s

def print_cut_rod_solution(p, n):
    r, s = extended_bottom_up_cut_rod(p, n)
    while n > 0:
        print(s[n])
        n -= s[n]
```

---

## 2. 矩阵链乘法 (Matrix-chain Multiplication)

### 问题描述

给定 $n$ 个矩阵 $\langle A_1, A_2, \ldots, A_n \rangle$，其中 $A_i$ 的维度是 $p_{i-1} \times p_i$。矩阵乘法满足结合律，但不同的加括号方式导致的**标量乘法次数**差别巨大。

> **大白话**：$(A_1 A_2) A_3$ 和 $A_1 (A_2 A_3)$ 结果一样，但计算量可能天差地别。

**例子**：$A_1: 10\times100$, $A_2: 100\times5$, $A_3: 5\times50$
- $(A_1 A_2) A_3$：$10\times100\times5 + 10\times5\times50 = 7500$
- $A_1 (A_2 A_3)$：$100\times5\times50 + 10\times100\times50 = 75000$（差10倍！）

### 递推公式

设 $m[i,j]$ 表示计算 $A_i A_{i+1} \cdots A_j$ 所需的最少标量乘法次数：

$$m[i,j] = \begin{cases} 0 & \text{if } i = j \\ \min_{i \le k < j} \{m[i,k] + m[k+1,j] + p_{i-1} p_k p_j\} & \text{if } i < j \end{cases}$$

- 在 $k$ 处"断开"，左边 $A_i \cdots A_k$，右边 $A_{k+1} \cdots A_j$
- 合并代价：$p_{i-1} \cdot p_k \cdot p_j$

### 算法

```python
def matrix_chain_order(p):
    n = len(p) - 1
    m = [[0]*(n+1) for _ in range(n+1)]
    s = [[0]*(n+1) for _ in range(n+1)]
    for l in range(2, n+1):          # l = 链长度
        for i in range(1, n-l+2):    # i = 起始位置
            j = i + l - 1            # j = 结束位置
            m[i][j] = inf
            for k in range(i, j):    # k = 断点
                q = m[i][k] + m[k+1][j] + p[i-1]*p[k]*p[j]
                if q < m[i][j]:
                    m[i][j] = q
                    s[i][j] = k
    return m, s
```

**时间复杂度**：$O(n^3)$，**空间复杂度**：$O(n^2)$

---

## 3. DP 的四步法

CLRS 总结的动态规划设计步骤：

| 步骤 | 说明 | 大白话 |
|------|------|--------|
| 1. 刻画最优解的结构 | 找出最优解包含哪些子问题的最优解 | 这道题的"套路"是什么 |
| 2. 递归定义最优解的值 | 写出递推公式（状态转移方程） | 用数学语言描述"套路" |
| 3. 自底向上计算最优解的值 | 按子问题规模从小到大求解 | 从最简单的情况开始往上算 |
| 4. 构造最优解（可选） | 利用保存的中间结果回溯 | 不光要答案，还要过程 |

> **注意**：贪心算法是 DP 的特例 — 只需考虑一个选择（贪心选择），而不是所有选择。

---

## 4. 最长公共子序列 (Longest Common Subsequence, LCS)

### 问题描述

给定序列 $X = \langle x_1, \ldots, x_m \rangle$ 和 $Y = \langle y_1, \ldots, y_n \rangle$，求它们的最长公共子序列。

> **子序列 vs 子串**：子序列不要求连续，子串要求连续。例如 "ABC" 和 "AC" 的 LCS 是 "AC"（长度2）。

### 递推公式

设 $c[i,j]$ 表示 $X_i$ 和 $Y_j$ 的 LCS 长度：

$$c[i,j] = \begin{cases} 0 & \text{if } i=0 \text{ or } j=0 \\ c[i-1,j-1] + 1 & \text{if } x_i = y_j \\ \max(c[i-1,j], c[i,j-1]) & \text{if } x_i \ne y_j \end{cases}$$

**大白话**：
- 如果两个序列的最后一个字符相同 → LCS 长度 +1
- 如果不同 → 舍弃其中一个的最后一个字符，取两种情况的较大值

**时间/空间**：$O(mn)$

---

## 5. 最优二叉搜索树 (Optimal Binary Search Tree)

### 问题描述

给定 $n$ 个关键字 $k_1 < k_2 < \cdots < k_n$，每个关键字 $k_i$ 被搜索的概率为 $p_i$，还有 $n+1$ 个"伪关键字" $d_0, d_1, \ldots, d_n$ 表示不在树中的值，概率为 $q_i$。构造一棵 BST 使**期望搜索代价**最小。

### 期望代价

$$E[\text{搜索代价}] = \sum_{i=1}^{n} p_i \cdot (1 + \text{depth}(k_i)) + \sum_{i=0}^{n} q_i \cdot (1 + \text{depth}(d_i))$$

### 递推公式

设 $e[i,j]$ 表示包含关键字 $k_i, \ldots, k_j$ 的最优 BST 的期望搜索代价：

$$e[i,j] = \begin{cases} q_{i-1} & \text{if } j = i-1 \\ \min_{i \le r \le j} \{e[i,r-1] + e[r+1,j] + w(i,j)\} & \text{if } i \le j \end{cases}$$

其中 $w(i,j) = \sum_{l=i}^{j} p_l + \sum_{l=i-1}^{j} q_l$ 是子树的总概率。

**时间复杂度**：$O(n^3)$（可用 Knuth 优化到 $O(n^2)$）

---

## 6. 备忘录 vs 自底向上 对比

| 特性 | 自顶向下 + 备忘录 | 自底向上 |
|------|-------------------|----------|
| 思路 | 递归 + 缓存 | 迭代，从小到大 |
| 子问题 | 只算需要的子问题 | 算所有子问题 |
| 常数因子 | 递归调用开销大 | 循环开销小 |
| 适用场景 | 子问题空间稀疏时更优 | 子问题空间密集时更优 |
| 代码复杂度 | 更自然，接近递归定义 | 需要确定遍历顺序 |
| 栈溢出风险 | 有（递归深度大时） | 无 |

> **大白话**：备忘录是"用到才算"，自底向上是"全都算一遍"。大多数情况下选自底向上更快，但备忘录写起来更直觉。

---

## 7. 子问题图 (Subproblem Graph)

- 每个子问题是图中的一个顶点
- 如果求解子问题 $x$ 依赖子问题 $y$，则有有向边 $x \to y$
- **自底向上** = 按逆拓扑序遍历子问题图
- **备忘录** = 对子问题图做深度优先搜索
- 运行时间 ≈ 顶点数 + 边数

---

## 关键区别：DP vs 贪心 vs 分治

| 特性 | 动态规划 | 贪心算法 | 分治法 |
|------|----------|----------|--------|
| 子问题 | 重叠子问题 | 一个子问题 | 不重叠子问题 |
| 选择 | 考虑所有选择 | 只考虑贪心选择 | 不涉及选择 |
| 求解顺序 | 自底向上或备忘录 | 自顶向下 | 递归分解 |
| 最优子结构 | ✅ | ✅ | ✅ |

---

## 相关笔记

- [[动态规划与记忆化]] — DP 的通用概念和记忆化技巧
- [[动态规划Python]] — Python 实现各种 DP 问题
- [[贪心算法CLRS]] — 贪心算法，DP 的特例
- [[Huffman编码]] — 贪心构造最优前缀码

---

## 参考

- CLRS 第四版，第14章 Dynamic Programming
- 钢条切割：§14.1
- 矩阵链乘法：§14.2
- 动态规划原理：§14.3
- LCS：§14.4
- 最优 BST：§14.5
