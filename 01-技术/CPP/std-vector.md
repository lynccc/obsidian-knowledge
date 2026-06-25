---
tags: [C++, STL, 容器]
aliases: [std::vector, vector, 动态数组]
created: 2026-06-25
---

# 📊 std::vector

## 核心概念

- `std::vector` 是动态数组，大小可自动扩展
- 连续内存存储，随机访问 O(1)
- 是 C++ 中最常用的容器

## 基本用法

```cpp
#include <vector>

std::vector<int> v1;                // 空 vector
std::vector<int> v2(5, 10);        // 5 个元素，都是 10
std::vector<int> v3 = {1, 2, 3};   // 列表初始化

v1.push_back(42);     // 尾部添加
v1.pop_back();        // 删除尾部
v1.size();            // 元素数量
v1.empty();           // 是否为空
v1.clear();           // 清空
```

## 访问元素

```cpp
std::vector<int> v = {10, 20, 30, 40, 50};

v[0];           // 10（不检查越界）
v.at(1);        // 20（越界抛异常）
v.front();      // 10（第一个）
v.back();       // 50（最后一个）
v.data();       // 底层数组指针
```

## 增删改查

```cpp
std::vector<int> v = {1, 2, 3};

v.push_back(4);                // {1,2,3,4}
v.insert(v.begin() + 1, 10);   // {1,10,2,3,4}
v.erase(v.begin() + 2);        // {1,10,3,4}
v[0] = 100;                    // {100,10,3,4}
```

## 遍历

```cpp
// 范围 for
for (int val : v) { }

// 引用方式（可修改）
for (auto& val : v) { val *= 2; }

// 索引方式
for (size_t i = 0; i < v.size(); i++) { }
```

## 容量管理

```cpp
std::vector<int> v;

v.size();       // 当前元素数
v.capacity();   // 当前容量（已分配空间）
v.reserve(100); // 预分配空间（避免频繁扩容）
v.shrink_to_fit();  // 释放多余空间
```

## 性能提示

- `push_back` 均摊 O(1)
- 中间插入/删除 O(n)
- 随机访问 O(1)
- 扩容时会重新分配内存并拷贝

## 相关笔记

- [[std-array]] — 固定大小数组
- [[STL容器]] — 容器概览
- [[动态内存]] — 内存管理

---

*由奶茶一号整理 🧋*
