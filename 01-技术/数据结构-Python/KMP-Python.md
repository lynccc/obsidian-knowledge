---
tags: [数据结构, Python, Miller, 字符串, KMP, 自动机]
aliases: [KMP算法Python实现, DFA模式匹配]
---

# KMP算法 Python实现

## 🗣️ 通俗讲解

> 想象你在文章里找一个单词。暴力方法是每次匹配失败就往后挪一位重来。KMP 的聪明之处在于：它会记住「已经匹配了哪些部分」，失配时不用从头来，直接跳到下一个可能匹配的位置。就像你已经知道前三个字母对了，第四个错了，就不用从第二个字母重新比较。

📖 **想看更深入的理论分析？** → [[KMP算法]]（邓俊辉 C++ 版）

## 核心概念

**KMP算法**（Knuth-Morris-Pratt）是一种高效的字符串模式匹配算法，核心思想是：当匹配失败时，利用已匹配的信息**跳过不可能成功的比较**，避免回溯主串指针。

### 生物学背景

模式匹配源于生物信息学中的 DNA 序列比对——在长序列中搜索特定碱基片段。

### DFA 确定有限自动机

KMP 的前身是基于 **DFA**（Deterministic Finite Automaton）的匹配：
- 为模式串构建状态转移表
- 从状态 0 开始，每读入一个字符就转移到下一个状态
- 到达接受状态即匹配成功
- 缺点：需要 O(m×|Σ|) 空间构建转移表（m 为模式长度，|Σ| 为字符集大小）

### KMP 的改进

KMP 不显式构建转移表，而是计算**部分匹配表**（failure function / next 数组）：
- `next[j]` 表示模式串 `pattern[0..j]` 的最长相等前后缀长度
- 匹配失败时，根据 next 数组决定模式串滑动多远

## 关键要点

- **时间复杂度**：O(n + m)，n 为主串长度，m 为模式串长度
- **空间复杂度**：O(m) 存储 next 数组
- next 数组的计算本身也用 KMP 的跳转思想，是递推过程
- 朴素算法最坏 O(n×m)，KMP 保证线性

## 与其他概念的联系

- [[KMP算法]] — 邓俊辉版笔记中的 C++ 实现与理论分析
- [[递归基础]] — next 数组的递推思想
- [[Python列表]] — next 数组用列表存储
- [[异序词检测]] — 另一个字符串处理问题

## 代码示例

```python
def build_next(pattern):
    """构建 KMP 的 next 数组（部分匹配表）"""
    m = len(pattern)
    next_arr = [0] * m
    j = 0  # 当前最长相等前后缀长度
    for i in range(1, m):
        while j > 0 and pattern[i] != pattern[j]:
            j = next_arr[j - 1]  # 回退
        if pattern[i] == pattern[j]:
            j += 1
        next_arr[i] = j
    return next_arr

def kmp_search(text, pattern):
    """KMP 模式匹配，返回所有匹配位置"""
    n, m = len(text), len(pattern)
    if m == 0:
        return []
    next_arr = build_next(pattern)
    results = []
    j = 0  # 模式串指针
    for i in range(n):  # 主串指针不回退
        while j > 0 and text[i] != pattern[j]:
            j = next_arr[j - 1]
        if text[i] == pattern[j]:
            j += 1
        if j == m:
            results.append(i - m + 1)
            j = next_arr[j - 1]
    return results

# 示例
print(kmp_search("ABABDABACDABABCABAB", "ABABCABAB"))  # [9]
```

## 参考
- 《Python数据结构与算法分析》第2版 §8.6
