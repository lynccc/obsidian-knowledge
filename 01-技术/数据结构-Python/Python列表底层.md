---
tags: [数据结构, Python, Miller, 动态数组, 均摊分析]
aliases: [Python动态数组, 列表底层实现]
---

# Python列表底层实现

## 核心概念

Python的 `list` 底层是**动态数组**（Dynamic Array），而非链表。它在内存中分配一块**连续空间**，当容量不足时自动扩容。

**扩容策略**：当数组满时，分配一块更大的新空间（通常是原容量的某个倍数），将旧数据复制过去。Python 的增长因子约为 1.125（即 `new_size = old_size + (old_size >> 3) + 6`），比 C++ 的 2 倍更节省内存。

## 关键要点

**时间复杂度对比**：

| 操作 | 时间复杂度 | 说明 |
|------|-----------|------|
| `append(x)` | 均摊 O(1) | 偶尔触发扩容复制 |
| `pop()` | 均摊 O(1) | 从末尾弹出 |
| `insert(0, x)` | O(n) | 需移动所有元素 |
| `pop(0)` | O(n) | 需移动所有元素 |
| `a[i]` | O(1) | 随机访问，偏移量计算 |

**均摊分析**：虽然单次 `append` 可能触发 O(n) 的复制，但连续 n 次 `append` 的总代价为 O(n)，因此均摊每次 O(1)。

## 与其他概念的联系

- 与 [[动态空间管理]] 的关系：动态数组是空间管理的经典案例
- 对比 [[链表]]：链表插入 O(1) 但随机访问 O(n)；动态数组反之
- [[Python列表]] 中有更多列表操作的介绍
- [[散列Python]] 中哈希表底层也用连续数组存储

## 代码示例

```python
import sys

# 观察 Python 列表的容量变化
lst = []
prev_size = sys.getsizeof(lst)
for i in range(32):
    lst.append(i)
    curr_size = sys.getsizeof(lst)
    if curr_size != prev_size:
        print(f"长度 {len(lst)}: 容量变化 {prev_size} → {curr_size}")
        prev_size = curr_size
```

## 参考
- 《Python数据结构与算法分析》第2版 §8.2
