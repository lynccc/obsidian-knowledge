---
tags: [C++, STL, 迭代器]
aliases: [iterator, 迭代器概念]
created: 2026-06-25
---

# 🔄 STL 迭代器

## 核心概念

- 迭代器（Iterator）是容器和算法之间的桥梁
- 提供统一的遍历接口，隐藏容器内部实现
- 类似于指针，支持 `*`、`++`、`--`、`==`、`!=`

## 基本用法

```cpp
std::vector<int> v = {10, 20, 30, 40, 50};

// 获取迭代器
auto it = v.begin();   // 指向第一个元素
auto end = v.end();    // 指向末尾（最后一个元素之后）

// 遍历
for (auto it = v.begin(); it != v.end(); ++it) {
    std::cout << *it << " ";  // 解引用获取值
}
```

## 迭代器类型

| 类型 | 支持操作 | 典型容器 |
|------|---------|---------|
| 输入迭代器 | `++`, `*`, `==`, `!=` | istream_iterator |
| 输出迭代器 | `*=` | ostream_iterator |
| 前向迭代器 | 输入+输出 | forward_list |
| 双向迭代器 | 前向+`--` | list, set, map |
| 随机访问迭代器 | 双向+`[]`, `+n`, `-n` | vector, deque |

## 常用操作

```cpp
std::vector<int> v = {1, 2, 3, 4, 5};

auto it = v.begin();

*it;              // 1（解引用）
++it;             // 前进到下一个
--it;             // 后退
it += 3;          // 跳 3 个（随机访问）
it - v.begin();   // 计算距离
it == v.end();    // 判断是否到末尾
```

## 反向迭代器

```cpp
std::vector<int> v = {1, 2, 3, 4, 5};

for (auto it = v.rbegin(); it != v.rend(); ++it) {
    std::cout << *it << " ";  // 5 4 3 2 1
}
```

## const 迭代器

```cpp
std::vector<int> v = {1, 2, 3};

// 只读迭代器
for (auto it = v.cbegin(); it != v.cend(); ++it) {
    // *it = 10;  // ❌ 不能修改
    std::cout << *it;
}
```

## 范围 for 本质

```cpp
// 范围 for 等价于迭代器遍历
for (int x : v) { }

// 等价于
for (auto it = v.begin(); it != v.end(); ++it) {
    int x = *it;
}
```

## 相关笔记

- [[STL概览]] — STL 概览
- [[STL容器]] — 容器
- [[STL算法]] — 算法
- [[指针]] — 指针（迭代器类似指针）

---

*由奶茶一号整理 🧋*

## 📚 参考
- 基于 C++ 内训知识
  补充：[[CPP环境搭建]] / [[编译与链接]]
