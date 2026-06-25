---
tags: [数据结构, Python, Miller, 堆, 优先级队列]
aliases: [二叉堆实现, 优先级队列Python]
---

# 二叉堆（Python）

## 🗣️ 通俗讲解

> 想象一棵树种在数组里：第 i 个位置的「孩子」在 2i 和 2i+1 位置，「爸爸」在 i/2 位置。最大堆就是爸爸永远比孩子大，所以堆顶就是最大值。插入时新元素「上浮」到该去的位置，删除时把最后一个元素放到堆顶再「下沉」——就像水里的气泡一样。

📖 **想看更深入的理论分析？** → [[二叉堆]]（邓俊辉 C++ 版）

## 核心概念

二叉堆用**列表**实现完全二叉树，是优先级队列的经典实现。

**最小堆性质**：每个节点 ≤ 其子节点。根节点即最小元素。

### 列表存储映射

对于索引 `i` 的节点：
- 父节点：`i // 2`
- 左子节点：`2 * i`
- 右子节点：`2 * i + 1`

列表索引 0 不使用（设为 0），根节点从索引 1 开始。

```python
class BinHeap:
    def __init__(self):
        self.heap_list = [0]
        self.current_size = 0
```

## 关键要点

### 插入操作（上浮 / perc_up）

新元素追加到列表末尾，然后与父节点比较，若小于父节点则交换，直到满足堆性质。

```python
def insert(self, k):
    self.heap_list.append(k)
    self.current_size += 1
    self.perc_up(self.current_size)

def perc_up(self, i):
    while i // 2 > 0:
        if self.heap_list[i] < self.heap_list[i // 2]:
            self.heap_list[i // 2], self.heap_list[i] = \
                self.heap_list[i], self.heap_list[i // 2]
        i = i // 2
```

**时间复杂度**：O(log n)

### 删除最小值（下沉 / perc_down）

用最后一个元素替换根节点，然后与较小的子节点交换，直到满足堆性质。

```python
def del_min(self):
    ret_val = self.heap_list[1]
    self.heap_list[1] = self.heap_list[self.current_size]
    self.current_size -= 1
    self.heap_list.pop()
    self.perc_down(1)
    return ret_val

def perc_down(self, i):
    while (i * 2) <= self.current_size:
        mc = self.min_child(i)
        if self.heap_list[i] > self.heap_list[mc]:
            self.heap_list[i], self.heap_list[mc] = \
                self.heap_list[mc], self.heap_list[i]
        i = mc

def min_child(self, i):
    if i * 2 + 1 > self.current_size:
        return i * 2
    else:
        if self.heap_list[i * 2] < self.heap_list[i * 2 + 1]:
            return i * 2
        else:
            return i * 2 + 1
```

**时间复杂度**：O(log n)

### 建堆（build_heap）

从最后一个非叶子节点开始，依次对每个节点执行 `perc_down`：

```python
def build_heap(self, a_list):
    i = len(a_list) // 2
    self.current_size = len(a_list)
    self.heap_list = [0] + a_list[:]
    while i > 0:
        self.perc_down(i)
        i -= 1
```

**时间复杂度**：O(n) — 非直觉的线性时间！

## 与其他概念的联系

- ← [[二叉堆]]：邓俊辉版理论基础
- → [[Dijkstra-Python]]：Dijkstra用堆优化
- → [[Prim-Python]]：Prim用堆优化
- 优先级队列是抽象数据类型，二叉堆是其一种实现

## 参考
- 《Python数据结构与算法分析》第2版 §6.6
