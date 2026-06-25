---
tags: [数据结构, Python, Miller, 跳表, Skiplist]
aliases: [跳表实现, Skiplist-Python]
---

# 跳表 Python 实现

## 🗣️ 通俗讲解

> 想象你在有序链表里找东西，得从头一个个往后看，太慢了。跳表的妙招是：在原始链表上面加几层「快速通道」——高层只保留部分节点，像高速公路的匝道。搜索时先走高速，快到了再下匝道到底层精确定位。通过抛硬币决定每个节点升到第几层，简单又高效。

📖 **想看更深入的理论分析？** → [[跳转表Skiplist]]（邓俊辉 C++ 版）

## 核心概念

**跳表（Skiplist）** 是一种基于**多层链表**的随机化数据结构，用于实现有序映射（Map ADT），支持 O(log n) 的搜索、插入和删除。

核心思想：在原始有序链表之上，建立多层"快速通道"。每层是下层链表的**子采样**，高层节点以概率 p 被提升到上层。搜索时从最高层开始，遇到目标值或过大的节点就下降一层。

## 关键要点

- **随机化**：插入时通过抛硬币决定节点提升到哪一层，期望层数为 O(log n)
- **搜索路径**：从顶层开始，水平移动直到下一个节点太大，然后下降一层
- **空间代价**：每个节点的期望层数为常数倍，总空间 O(n)
- **对比平衡树**：实现更简单，无需旋转操作，且性能期望与 BST 相当

## 与其他概念的联系

- 与 [[跳转表Skiplist]] 的关系：邓俊辉版笔记中有更详细的理论分析
- [[Python字典]] — Python 的 dict 用哈希表实现，跳表是另一种映射实现方式
- [[BST-Python]] — BST 也是有序映射的实现，但需维护平衡
- [[AVL树Python]] — AVL 树提供严格的 O(log n) 保证，跳表是概率保证
- [[散列Python]] — 哈希表 vs 跳表：无序 vs 有序

## 代码示例

```python
import random

class SkipNode:
    def __init__(self, key, value, level):
        self.key = key
        self.value = value
        self.forward = [None] * (level + 1)

class SkipList:
    def __init__(self, max_level=16, p=0.5):
        self.max_level = max_level
        self.p = p
        self.header = SkipNode(-1, -1, max_level)
        self.level = 0

    def random_level(self):
        lvl = 0
        while random.random() < self.p and lvl < self.max_level:
            lvl += 1
        return lvl

    def search(self, key):
        current = self.header
        for i in range(self.level, -1, -1):
            while current.forward[i] and current.forward[i].key < key:
                current = current.forward[i]
        current = current.forward[0]
        if current and current.key == key:
            return current.value
        return None

    def insert(self, key, value):
        update = [None] * (self.max_level + 1)
        current = self.header
        for i in range(self.level, -1, -1):
            while current.forward[i] and current.forward[i].key < key:
                current = current.forward[i]
            update[i] = current
        current = current.forward[0]
        if current and current.key == key:
            current.value = value
        else:
            new_level = self.random_level()
            if new_level > self.level:
                for i in range(self.level + 1, new_level + 1):
                    update[i] = self.header
                self.level = new_level
            new_node = SkipNode(key, value, new_level)
            for i in range(new_level + 1):
                new_node.forward[i] = update[i].forward[i]
                update[i].forward[i] = new_node
```

## 参考
- 《Python数据结构与算法分析》第2版 §8.4
