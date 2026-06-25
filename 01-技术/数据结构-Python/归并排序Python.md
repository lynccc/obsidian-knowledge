---
tags: [数据结构, Python, Miller, 排序]
aliases: [归并排序, Merge Sort, 分治排序]
---

# 归并排序（Python）

## 🗣️ 通俗讲解

> 核心思路是「先拆后合」：把列表一分为二，各自排好序，然后像拉拉链一样把两个有序列表合在一起。时间稳定在 O(n log n)，不像快排那样有退化风险，但代价是需要额外空间。Python 内置的 `sorted()` 就是基于归并排序的改进版（TimSort）。

📖 **想看更深入的理论分析？** → [[向量排序]]（邓俊辉 C++ 版，含归并排序详解）

## 核心概念

归并排序（Merge Sort）是**分治法（Divide and Conquer）** 的经典应用：将列表分成两半，递归排序每一半，然后将两个有序子列表**合并（merge）** 成一个有序列表。

## Python 实现

```python
def merge_sort(a_list):
    if len(a_list) > 1:
        mid = len(a_list) // 2
        left_half = a_list[:mid]
        right_half = a_list[mid:]

        merge_sort(left_half)
        merge_sort(right_half)

        # 合并
        i = j = k = 0
        while i < len(left_half) and j < len(right_half):
            if left_half[i] <= right_half[j]:
                a_list[k] = left_half[i]
                i += 1
            else:
                a_list[k] = right_half[j]
                j += 1
            k += 1

        while i < len(left_half):
            a_list[k] = left_half[i]
            i += 1
            k += 1

        while j < len(right_half):
            a_list[k] = right_half[j]
            j += 1
            k += 1
```

## 时间复杂度

- **所有情况**：O(n log n)
  - 分割：log n 层
  - 每层合并：O(n)
- 空间复杂度：**O(n)**（需要额外空间存放子列表）
- **稳定排序**

## 与其他 O(n log n) 排序对比

| 特性 | 归并排序 | 快速排序 |
|------|---------|---------|
| 最坏 | O(n log n) | O(n²) |
| 平均 | O(n log n) | O(n log n) |
| 空间 | O(n) | O(log n) |
| 稳定性 | **稳定** | 不稳定 |
| 适用 | 需要稳定排序 | 通用场景 |

## 关键要点

- 时间复杂度**恒定** O(n log n)，不受输入数据影响
- 稳定排序，相等元素保持原始顺序
- 缺点是需要 O(n) 额外空间
- Python 的 `sorted()` 和 `list.sort()` 使用 **TimSort**（归并+插入的混合），正是基于归并排序
- 适合**链表排序**（无需随机访问，合并操作天然适合链表）

## 与其他概念的联系

- [[快速排序Python]] — 另一个 O(n log n) 排序，实践中通常更快
- [[插入排序]] — TimSort 在小分区时切换为插入排序
- [[递归基础]] — 归并排序是递归分治的典型示例
- [[向量排序]] — 邓俊辉版对归并排序的更深入讨论

## 参考
- 《Python数据结构与算法分析》第2版 §5.3.5
