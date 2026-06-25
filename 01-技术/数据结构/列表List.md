---
tags: [数据结构, C++, 邓俊辉]
aliases: [List, 链表, 双向链表]
---

# 列表 List

## 核心概念

列表是采用**动态存储策略**的线性结构，通过指针链接各元素，与[[向量Vector]]的连续存储形成对比。

### 从向量到列表的演进

| 维度 | [[向量Vector]] | 列表 |
|------|---------------|------|
| 存储方式 | 连续空间 | 离散节点 + 指针链接 |
| 访问方式 | 循秩访问（O(1)） | 循位置访问（O(n)） |
| 插入/删除 | O(n)（需移位） | O(1)（修改指针） |
| 空间 | 紧凑，可能浪费 | 每节点额外指针开销 |

### 节点结构 ListNode

```cpp
template <typename T> struct ListNode {
    T data;                // 数据域
    ListNode<T>* pred;     // 前驱指针
    ListNode<T>* succ;     // 后继指针
    ListNode() {}          // 默认构造
    ListNode(T e, ListNode<T>* p = nullptr, ListNode<T>* s = nullptr)
        : data(e), pred(p), succ(s) {}
};
```

双向链表结构：每个节点同时持有前驱 `pred` 和后继 `succ` 指针，支持双向遍历。

### 循位置访问

列表以**位置（position）**为基本访问单元，即节点指针。不同于向量以整数秩（rank）索引，列表通过节点间的指针导航实现访问。

## 关键要点

- 列表适配器 `List<T>` 封装了头尾哨兵节点和规模 `size`
- 查找操作 `find(e, n, p)`：从节点 `p` 出发向前驱方向搜索 `n` 个节点
- 插入操作 `insertBefore(p, e)` / `insertAfter(p, e)`：O(1)
- 删除操作 `remove(p)`：O(1)
- 基于复制的构造：通过 `copyNodes()` 从已有节点列表复制构建

## 与其他概念的联系
- [[向量Vector]] — 对比：静态 vs 动态，循秩 vs 循位置
- [[哨兵节点]] — 列表实现的关键技巧
- [[有序列表]] — 列表的有序特化
- [[列表排序]] — 列表上的排序算法
- [[二分查找]] — 适用于向量，列表无法直接使用

## 代码示例

```cpp
// 列表的典型操作
List<int> L;              // 创建空列表
L.insertAsLast(5);        // 尾部插入
L.insertAsFirst(1);       // 头部插入
ListNode<int>* p = L.first()->succ; // 定位到某节点
L.insertBefore(p, 3);     // 在 p 前插入
L.remove(p);              // 删除节点
```

## 🆚 C++ vs Python 实现对比

> 💡 **小白提示：** 这个概念在两本书里都有讲，但用的语言不同。
> - **C++ 版**（邓俊辉）：更偏理论，讲底层原理，适合考研/面试深入理解
> - **Python 版**（Miller）：更偏实践，代码简洁易读，适合快速上手
>
> 📖 Python 版笔记：[[链表]]

## 参考
- 《数据结构（C++语言版）》第3版 邓俊辉 §3.1-§3.3
