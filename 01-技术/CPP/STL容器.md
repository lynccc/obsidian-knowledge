---
tags: [C++, STL, 容器]
aliases: [vector, list, deque, set, map]
created: 2026-06-25
---

# 📦 STL 容器

## 核心概念

- 容器是存储和管理数据的对象
- 不同容器有不同的性能特征和适用场景
- 选择合适的容器是性能优化的关键

## 序列容器

### vector（动态数组）
```cpp
std::vector<int> v = {1, 2, 3};
v.push_back(4);     // 尾部添加 O(1)
v[0];                // 随机访问 O(1)
v.size();            // 大小
```

### list（双向链表）
```cpp
std::list<int> l = {1, 2, 3};
l.push_front(0);    // 头部添加 O(1)
l.push_back(4);     // 尾部添加 O(1)
// 不支持随机访问，不能用 l[0]
```

### deque（双端队列）
```cpp
std::deque<int> d = {1, 2, 3};
d.push_front(0);    // 头部添加 O(1)
d.push_back(4);     // 尾部添加 O(1)
d[0];               // 支持随机访问 O(1)
```

## 关联容器（有序）

### set（集合）
```cpp
std::set<int> s = {3, 1, 4, 1, 5};  // 自动去重排序
s.insert(2);
s.count(1);         // 1（存在）或 0（不存在）
s.erase(3);
// 遍历有序：1 2 4 5
```

### map（字典）
```cpp
std::map<std::string, int> m;
m["alice"] = 90;
m["bob"] = 85;
m.count("alice");   // 1
m["alice"];          // 90

for (const auto& [key, val] : m) {  // C++17 结构化绑定
    std::cout << key << ": " << val;
}
```

## 无序容器（哈希）

```cpp
std::unordered_map<std::string, int> um;
um["key"] = 42;     // O(1) 查找

std::unordered_set<int> us;
us.insert(1);       // O(1) 插入
```

## 容器适配器

```cpp
std::stack<int> stk;       // 栈（后进先出）
stk.push(1); stk.top(); stk.pop();

std::queue<int> q;         // 队列（先进先出）
q.push(1); q.front(); q.pop();

std::priority_queue<int> pq;  // 优先队列（最大堆）
pq.push(3); pq.top(); pq.pop();
```

## 选择指南

| 需求 | 推荐容器 |
|------|---------|
| 随机访问 | vector |
| 频繁头尾操作 | deque |
| 频繁中间插入 | list |
| 去重+排序 | set |
| 键值对 | map |
| O(1) 查找 | unordered_map |

## 相关笔记

- [[STL概览]] — STL 概览
- [[std-vector]] — vector 详解
- [[STL算法]] — 算法
- [[STL迭代器]] — 迭代器

---

*由奶茶一号整理 🧋*

## 📚 参考
- 基于 C++ 内训知识
  补充：[[CPP环境搭建]] / [[编译与链接]]
