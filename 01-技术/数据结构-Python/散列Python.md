---
tags: [数据结构, Python, Miller, 搜索, 散列]
aliases: [哈希表, Hash Table, 散列表, Hashing]
---

# 散列（Python）

## 🗣️ 通俗讲解

> 就像图书馆的索引卡片——通过书名能直接算出书架位置，不用一本本翻找。散列表就是这个原理：用一个函数把 key 转换成数组下标，直接定位。但偶尔两个 key 会算出同一个位置（冲突），需要额外处理。Python 的 `dict` 和 `set` 底层就是散列表。

📖 **想看更深入的理论分析？** → [[散列表]]（邓俊辉 C++ 版）

## 核心概念

散列（Hashing）通过**散列函数**将键直接映射到数组索引，实现**平均 O(1)** 的搜索、插入和删除。Python 内置的 `dict` 和 `set` 就是基于散列实现的。

## 散列函数

理想的散列函数应满足：
1. **一致性**：相同键总是映射到相同位置
2. **高效性**：计算速度快
3. **均匀性**：键均匀分布在槽中

### 常见方法：取余法

```python
def hash_func(key, size):
    return key % size
```

对于字符串，可将字符的 ASCII 码相加：

```python
def hash_str(a_string, table_size):
    sum_val = 0
    for char in a_string:
        sum_val += ord(char)
    return sum_val % table_size
```

**改进**：引入位置权重，避免相同字母不同顺序的冲突：

```python
def hash_str_weighted(a_string, table_size):
    sum_val = 0
    for pos, char in enumerate(a_string):
        sum_val += (pos + 1) * ord(char)
    return sum_val % table_size
```

## 冲突解决

当两个键映射到同一位置时发生**冲突（collision）**。

### 开放寻址法（Linear Probing）

冲突时向后寻找下一个空槽：

```python
# 查找时：从 hash(key) 开始，逐个检查
# 插入时：找到空槽放入
# 删除时：标记为已删除（不能直接置空）
```

- **聚集（clustering）** 问题：连续占用的槽越来越多
- 改进：**二次探测**（步长为 1², 2², 3²...）

### 链表法（Chaining）

每个槽维护一个链表，冲突的元素放入同一链表：

```python
class HashTable:
    def __init__(self, size=11):
        self.size = size
        self.slots = [[] for _ in range(size)]  # 链表数组
```

- Python 的 `dict` 底层使用类似机制
- 没有聚集问题，但需要额外空间

## 负载因子

$$\lambda = \frac{\text{元素个数}}{\text{表大小}}$$

- λ < 0.5 时性能最佳
- λ 越大，冲突越多，性能越差
- 当 λ 超过阈值时需要**扩容（rehash）**：创建更大的表，重新计算所有元素的位置

## 关键要点

- 平均时间复杂度 **O(1)**，最坏情况 O(n)（所有键冲突）
- 散列函数的质量直接决定性能
- Python 的 `dict` 是高度优化的散列表，使用开放寻址
- 冲突不可避免，关键是选择合适的解决策略
- 负载因子控制表的稀疏程度

## 与其他概念的联系

- [[顺序搜索]] — 散列是顺序搜索的"升级版"
- [[二分搜索Python]] — 散列以空间换时间
- [[散列表]] — 邓俊辉版对散列的更深入讨论（C++ 实现）

## 参考
- 《Python数据结构与算法分析》第2版 §5.2.3
