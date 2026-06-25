---
tags: [C++, STL, 容器]
aliases: [std::array, array]
created: 2026-06-25
---

# 📦 std::array

## 核心概念

- `std::array` 是固定大小的数组容器（C++11）
- 大小在编译时确定，栈上分配
- 比原生数组更安全，支持 STL 接口

## 基本用法

```cpp
#include <array>

std::array<int, 5> arr = {1, 2, 3, 4, 5};

arr[0] = 10;           // 访问（不检查越界）
arr.at(1) = 20;        // 访问（越界抛异常）
arr.front();           // 第一个元素
arr.back();            // 最后一个元素
arr.size();            // 大小（5）
arr.empty();           // 是否为空
arr.fill(0);           // 全部填充为 0
```

## 遍历

```cpp
std::array<int, 5> arr = {1, 2, 3, 4, 5};

// 范围 for
for (int val : arr) {
    std::cout << val << " ";
}

// 迭代器
for (auto it = arr.begin(); it != arr.end(); ++it) {
    std::cout << *it << " ";
}
```

## std::array vs 原生数组

| 特性 | 原生数组 | std::array |
|------|---------|-----------|
| 知道大小 | ❌ | ✅ `.size()` |
| 越界检查 | ❌ | ✅ `.at()` |
| 可复制 | ❌ | ✅ |
| STL 兼容 | ❌ | ✅ |
| 性能 | 相同 | 相同 |

## 多维 std::array

```cpp
std::array<std::array<int, 3>, 2> matrix = {{
    {1, 2, 3},
    {4, 5, 6}
}};

matrix[1][2] = 100;
```

## 相关笔记

- [[数组-CPP]] — 原生数组
- [[std-vector]] — 动态数组
- [[STL容器]] — STL 容器概览

---

*由奶茶一号整理 🧋*
