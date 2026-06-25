---
tags: [数据结构, Python, Miller, 排序]
aliases: [快速排序, Quick Sort, 快排]
---

# 快速排序（Python）

## 🗣️ 通俗讲解

> 选一个数当「标杆」（pivot），比它小的扔左边，比它大的扔右边，然后左右两边各自再选标杆、再分……这就是分治。平均情况下是最快的通用排序（O(n log n)），但如果运气差选到最大或最小的数当标杆，就会退化成 O(n²)。所以实战中常用「三数取中」来选标杆。

📖 **想看更深入的理论分析？** → [[快速排序]]（邓俊辉 C++ 版）

## 核心概念

快速排序（Quick Sort）由 C.A.R. Hoare 于 1960 年提出，是实践中**最快的排序算法**。采用分治策略：选择一个**枢轴（pivot）**，将列表分为"小于枢轴"和"大于枢轴"两部分，递归排序。

## Python 实现

```python
def quick_sort(a_list):
    quick_sort_helper(a_list, 0, len(a_list) - 1)

def quick_sort_helper(a_list, first, last):
    if first < last:
        split_point = partition(a_list, first, last)
        quick_sort_helper(a_list, first, split_point - 1)
        quick_sort_helper(a_list, split_point + 1, last)

def partition(a_list, first, last):
    pivot_value = a_list[first]
    left_mark = first + 1
    right_mark = last
    done = False

    while not done:
        while left_mark <= right_mark and a_list[left_mark] <= pivot_value:
            left_mark += 1
        while right_mark >= left_mark and a_list[right_mark] >= pivot_value:
            right_mark -= 1
        if right_mark < left_mark:
            done = True
        else:
            a_list[left_mark], a_list[right_mark] = a_list[right_mark], a_list[left_mark]

    a_list[first], a_list[right_mark] = a_list[right_mark], a_list[first]
    return right_mark
```

## 分区过程

```
[3, 5, 2, 8, 1, 9, 4, 7, 6]  pivot=3
  ↑left                    ↑right
向右找>3的，向左找<3的，交换
分区后: [1, 2, 3, 8, 5, 9, 4, 7, 6]
        [1,2]  3  [8,5,9,4,7,6]
```

## 时间复杂度

| 情况 | 复杂度 | 说明 |
|------|--------|------|
| 最好 | O(n log n) | 每次恰好平分 |
| 平均 | O(n log n) | 随机数据 |
| 最坏 | O(n²) | 已有序 + 选首元素为枢轴 |

- 空间复杂度：**O(log n)**（递归栈）
- **不稳定排序**

## 枢轴选择策略

1. **首元素**：简单但对有序数据退化为 O(n²)
2. **随机选择**：避免最坏情况
3. **三数取中（Median of Three）**：取首、中、末三数的中位数

```python
def median_of_three(a_list, first, last):
    mid = (first + last) // 2
    candidates = [(a_list[first], first), (a_list[mid], mid), (a_list[last], last)]
    candidates.sort(key=lambda x: x[0])
    return candidates[1][1]  # 返回中位数的索引
```

## 关键要点

- 实践中最快的通用排序算法
- 平均 O(n log n)，常数因子比[[归并排序Python]]小
- Python 的 `list.sort()` 内部不直接用快排，而是 TimSort
- 最坏情况可通过随机化或三数取中避免
- **原地排序**，不需要额外数组空间

## 与其他概念的联系

- [[归并排序Python]] — 归并排序最坏也是 O(n log n) 但需要额外空间
- [[插入排序]] — 小规模子数组可切换为插入排序
- [[递归基础]] — 快速排序是递归分治的另一经典示例
- [[快速排序]] — 邓俊辉版对快速排序的更深入分析（Lomuto/Hoare 分区方案对比）

## 参考
- 《Python数据结构与算法分析》第2版 §5.3.6
