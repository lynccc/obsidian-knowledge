---
tags: [数据结构, Python, Miller, 搜索]
aliases: [二分查找, Binary Search, 折半搜索]
---

# 二分搜索（Python）

## 🗣️ 通俗讲解

> 就像猜数字游戏：「大了」「小了」——每次把范围砍掉一半，所以叫「二分」。100 万个数最多猜 20 次就能找到目标。前提是要先排好序，不然没法二分。

📖 **想看更深入的理论分析？** → [[二分查找]]（邓俊辉 C++ 版）

## 核心概念

二分搜索（Binary Search）利用列表**有序**的特性，每次比较中间元素，将搜索范围减半，直到找到目标或范围为空。

## Python 实现

```python
def binary_search(a_list, item):
    first = 0
    last = len(a_list) - 1
    found = False

    while first <= last and not found:
        midpoint = (first + last) // 2
        if a_list[midpoint] == item:
            found = True
        elif item < a_list[midpoint]:
            last = midpoint - 1
        else:
            first = midpoint + 1
    return found
```

### 递归版本

```python
def binary_search_recursive(a_list, item):
    if len(a_list) == 0:
        return False
    midpoint = len(a_list) // 2
    if a_list[midpoint] == item:
        return True
    elif item < a_list[midpoint]:
        return binary_search_recursive(a_list[:midpoint], item)
    else:
        return binary_search_recursive(a_list[midpoint + 1:], item)
```

## 时间复杂度分析

- 每次将搜索范围减半
- n → n/2 → n/4 → ... → 1
- 需要 **log₂n** 次比较
- 时间复杂度：**O(log n)**

| 列表大小 | 顺序搜索（最坏） | 二分搜索（最坏） |
|---------|----------------|----------------|
| 1,024 | 1,024 | 10 |
| 1,048,576 | 1,048,576 | 20 |

## 关键要点

- **前提条件**：列表必须有序
- 对大列表优势明显：100 万个元素只需约 20 次比较
- Python 的 `bisect` 模块提供了高效的二分搜索实现
- 递归版本因切片操作有额外开销，迭代版本更优
- 二分搜索只适用于支持随机访问的数据结构（如列表，不适用于链表）

## 与其他概念的联系

- [[顺序搜索]] — 无序列表只能用顺序搜索
- [[散列Python]] — 散列可实现 O(1) 查找但需要额外空间
- [[二分查找]] — 邓俊辉版的二分查找讨论（更侧重 C++ 实现和复杂度证明）
- [[插入排序]] — 插入排序可用二分搜索优化"找插入位置"步骤

## 参考
- 《Python数据结构与算法分析》第2版 §5.2.2
