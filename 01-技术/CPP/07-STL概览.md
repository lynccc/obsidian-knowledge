---
tags: [C++, STL, 概览]
aliases: [STL, 标准模板库]
created: 2026-06-25
---

# 📚 STL 概览

## 核心概念

- STL（Standard Template Library）是 C++ 的标准模板库
- 三大组件：**容器**（Container）、**算法**（Algorithm）、**迭代器**（Iterator）
- 泛型编程的典范，高效且可复用

## 三大组件

```
┌─────────────────────────────────────┐
│              算法 (Algorithm)         │
│    sort / find / transform / ...     │
├─────────────────────────────────────┤
│           迭代器 (Iterator)           │
│         统一的遍历接口                 │
├─────────────────────────────────────┤
│           容器 (Container)            │
│  vector / list / map / set / ...     │
└─────────────────────────────────────┘
```

## 容器分类

| 类型 | 容器 | 特点 |
|------|------|------|
| 序列 | vector, deque, list | 线性排列 |
| 关联 | set, map, multiset, multimap | 有序，红黑树 |
| 无序 | unordered_set, unordered_map | 哈希表，O(1) |
| 适配器 | stack, queue, priority_queue | 特殊接口 |

## 快速示例

```cpp
#include <vector>
#include <algorithm>
#include <iostream>

int main() {
    std::vector<int> v = {3, 1, 4, 1, 5, 9};

    // 算法：排序
    std::sort(v.begin(), v.end());

    // 算法：查找
    auto it = std::find(v.begin(), v.end(), 5);

    // 输出
    for (int x : v) std::cout << x << " ";
    // 1 1 3 4 5 9
}
```

## 相关笔记

- [[06-STL容器]] — 容器详解
- [[08-STL算法]] — 算法详解
- [[09-STL迭代器]] — 迭代器详解
- [[18-函数模板]] — 模板基础
- [[40-类模板]] — 模板类

---

*由奶茶一号整理 🧋*

## 📚 参考
- 基于 C++ 内训知识
  补充：[[04-CPP环境搭建]] / [[43-编译与链接]]
