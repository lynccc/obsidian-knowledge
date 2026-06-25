---
tags: [数据结构, Python, Miller, 排序]
aliases: [希尔排序, Shell Sort, 缩小增量排序]
---

# 希尔排序（Python）

## 🗣️ 通俗讲解

> 插入排序对几乎排好序的数据很快，希尔排序就利用了这一点：先隔几个数排一次（大间隔预排序），再缩小间隔继续排，最后间隔为 1 时数据已基本有序，插入排序就飞快了。就像先把大件行李归位，再整理小物件。

📖 **想看更深入的理论分析？** → [[希尔排序]]（邓俊辉 C++ 版）

## 核心概念

希尔排序（Shell Sort）是[[插入排序]]的改进版，由 Donald Shell 于 1959 年提出。核心思想是通过**间隔序列（gap sequence）** 将列表分成多个子序列，对每个子序列进行插入排序，逐步缩小间隔直到为 1。

## 为什么有效

插入排序对近乎有序的数据效率高（接近 O(n)）。希尔排序通过大间隔的预排序，使数据逐渐趋于有序，最后的间隔为 1 的插入排序就能快速完成。

## Python 实现

```python
def shell_sort(a_list):
    sublist_count = len(a_list) // 2
    while sublist_count > 0:
        for start_position in range(sublist_count):
            gap_insertion_sort(a_list, start_position, sublist_count)
        sublist_count //= 2  # 间隔减半

def gap_insertion_sort(a_list, start, gap):
    """对间隔为 gap 的子序列进行插入排序"""
    for i in range(start + gap, len(a_list), gap):
        current_value = a_list[i]
        position = i
        while position >= gap and a_list[position - gap] > current_value:
            a_list[position] = a_list[position - gap]
            position -= gap
        a_list[position] = current_value
```

## 间隔序列

最简单的是 **Knuth 序列**：1, 4, 13, 40, 121, ...（`h = 3*h + 1`）

```python
# 使用 Knuth 序列
def shell_sort_knuth(a_list):
    gap = 1
    while gap < len(a_list) // 3:
        gap = gap * 3 + 1  # 生成最大间隔
    while gap > 0:
        for start in range(gap):
            gap_insertion_sort(a_list, start, gap)
        gap //= 3
```

## 时间复杂度

- 使用简单间隔（每次减半）：**O(n^(3/2))** 到 O(n²) 之间
- 使用 Knuth 序列：**O(n^(3/2))**
- 最优间隔序列可达到 O(n^(4/3)) 或更好
- 空间复杂度：**O(1)**
- **不稳定排序**

## 过程示例

```
[5, 3, 8, 1, 2, 9, 4, 7, 6]
gap=4: 比较 (5,2), (3,9), (8,4), (1,7), (2,6)
       → [2, 3, 4, 1, 5, 9, 8, 7, 6]
gap=2: 对间隔2的子序列排序
       → [2, 1, 4, 3, 5, 7, 8, 9, 6]
gap=1: 普通插入排序（数据已基本有序）
       → [1, 2, 3, 4, 5, 6, 7, 8, 9]
```

## 关键要点

- 间隔序列的选择对性能影响很大
- 虽然最坏仍是 O(n²)，但实际性能远好于简单 O(n²) 排序
- 是第一个突破 O(n²) 的排序算法（历史上）
- 实现简单，不需要额外空间
- 对中等规模数据集是个好选择

## 与其他概念的联系

- [[插入排序]] — 希尔排序的基础
- [[冒泡排序Python]] — 同为 O(n²) 级别但希尔排序更快
- [[归并排序Python]] — 归并排序有更好的理论复杂度
- [[希尔排序]] — 邓俊辉版对希尔排序的更深入分析

## 参考
- 《Python数据结构与算法分析》第2版 §5.3.4
