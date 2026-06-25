---
tags: [算法导论, CLRS, 中文翻译, 排序, 堆]
aliases: [Heapsort, 堆排序]
---

# 堆排序（Heapsort）

## 通俗讲解
> 想象你有一堆数字，想把它们从小到大排好。堆排序的思路是：先把这堆数字整理成一个"大顶堆"——最大的数在最顶上，然后把最大的数和最后一个数交换，这样最大的数就到了最后面。接着缩小堆的范围，重新整理堆，再把第二大的数放到倒数第二个位置……如此反复，直到所有数都排好。整个过程就像从一堆东西里不断挑出最大的那个放到最后。

## 核心概念（中文，附英文术语）

### 堆（Heap）
堆是一个**近似完全二叉树**（nearly complete binary tree），可以用数组高效表示：
- 对于下标为 `i` 的节点：
  - **父节点**：`PARENT(i) = ⌊i/2⌋`
  - **左孩子**：`LEFT(i) = 2i`
  - **右孩子**：`RIGHT(i) = 2i + 1`
- **堆的高度**：Θ(log n)

### 最大堆性质（Max-Heap Property）
对于除根以外的每个节点 i，都有：
```
A[PARENT(i)] ≥ A[i]
```
即**父节点的值 ≥ 子节点的值**。最大元素在根节点。

### 最小堆性质（Min-Heap Property）
对于除根以外的每个节点 i，都有：
```
A[PARENT(i)] ≤ A[i]
```
最小元素在根节点。

### MAX-HEAPIFY（维护最大堆性质）
**输入**：数组 A、堆大小 heap-size、下标 i
**作用**：假设以 LEFT(i) 和 RIGHT(i) 为根的子树都是最大堆，但 A[i] 可能小于其子节点，违反最大堆性质。MAX-HEAPIFY 让 A[i] "下沉"（float down），使以 i 为根的子树重新满足最大堆性质。

```
MAX-HEAPIFY(A, i):
    l = LEFT(i)
    r = RIGHT(i)
    if l ≤ A.heap-size and A[l] > A[i]:
        largest = l
    else:
        largest = i
    if r ≤ A.heap-size and A[r] > A[largest]:
        largest = r
    if largest ≠ i:
        exchange A[i] with A[largest]
        MAX-HEAPIFY(A, largest)
```

**时间复杂度**：O(log n) —— 递归深度最多为堆的高度。

### BUILD-MAX-HEAP（建堆）
**输入**：数组 A[1..n]
**作用**：将无序数组转换为最大堆

```
BUILD-MAX-HEAP(A, n):
    A.heap-size = n
    for i = ⌊n/2⌋ downto 1:
        MAX-HEAPIFY(A, i)
```

**关键洞察**：叶子节点（下标 ⌊n/2⌋+1 到 n）本身就是大小为 1 的最大堆，所以只需从最后一个非叶子节点开始，自底向上调用 MAX-HEAPIFY。

**时间复杂度**：O(n) —— 虽然看起来是 O(n log n)，但严格分析表明是线性的，因为大部分节点的高度很小。

### HEAPSORT（堆排序）
```
HEAPSORT(A, n):
    BUILD-MAX-HEAP(A, n)
    for i = n downto 2:
        exchange A[1] with A[i]
        A.heap-size = A.heap-size - 1
        MAX-HEAPIFY(A, 1)
```

**时间复杂度**：O(n log n)
- 建堆：O(n)
- n-1 次 MAX-HEAPIFY：每次 O(log n)，共 O(n log n)

## 关键要点

1. **原地排序**：堆排序是原地排序算法，只需要常数级别的额外空间
2. **最坏情况 O(n log n)**：不像快速排序，堆排序的最坏情况仍然是 O(n log n)
3. **不稳定排序**：堆排序不是稳定排序
4. **数组即堆**：堆用数组表示，不需要指针，空间效率高

## 优先队列（Priority Queue）

堆的一个重要应用是实现**优先队列**。最大优先队列支持以下操作：

| 操作 | 说明 | 时间复杂度 |
|------|------|-----------|
| INSERT(S, x, k) | 插入元素 x，键值为 k | O(log n) |
| MAXIMUM(S) | 返回键值最大的元素 | O(1) |
| EXTRACT-MAX(S) | 删除并返回键值最大的元素 | O(log n) |
| INCREASE-KEY(S, x, k) | 将元素 x 的键值增加到 k | O(log n) |

**应用场景**：
- 操作系统任务调度（高优先级任务先执行）
- 事件驱动模拟
- [[Dijkstra算法]] 中的最短路径计算
- [[Huffman编码]] 中的贪心选择

## 与其他概念的联系

- [[二叉堆]]：堆排序的底层数据结构
- [[快速排序CLRS]]：另一种 O(n log n) 排序算法，实践中通常更快
- [[归并排序]]：同样是 O(n log n)，但是稳定排序
- [[优先队列]]：堆的经典应用
- [[斐波那契堆]]：更高效的优先队列实现

## 参考
- 《算法导论》第四版 §6.1-6.5
- §6.1 堆（Heaps）
- §6.2 维护堆性质（Maintaining the heap property）
- §6.3 建堆（Building a heap）
- §6.4 堆排序算法（The heapsort algorithm）
- §6.5 优先队列（Priority queues）
