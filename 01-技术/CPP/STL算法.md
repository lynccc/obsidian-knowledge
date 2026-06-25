---
tags: [C++, STL, 算法]
aliases: [sort, find, transform, STL算法]
created: 2026-06-25
---

# 🔧 STL 算法

## 核心概念

- STL 算法通过迭代器操作容器，与容器类型无关
- 大多数算法在 `<algorithm>` 头文件中
- 算法不会改变容器大小（需配合容器方法）

## 常用算法

### 排序

```cpp
#include <algorithm>
#include <vector>

std::vector<int> v = {3, 1, 4, 1, 5, 9};

std::sort(v.begin(), v.end());                    // 升序
std::sort(v.begin(), v.end(), std::greater<>());  // 降序

// 部分排序
std::partial_sort(v.begin(), v.begin()+3, v.end());
```

### 查找

```cpp
std::vector<int> v = {1, 2, 3, 4, 5};

auto it = std::find(v.begin(), v.end(), 3);        // 查找 3
auto it2 = std::find_if(v.begin(), v.end(),
    [](int x) { return x > 3; });                   // 查找第一个 > 3

bool has = std::binary_search(v.begin(), v.end(), 3);  // 二分查找（需已排序）
auto cnt = std::count(v.begin(), v.end(), 1);          // 计数
```

### 修改

```cpp
std::vector<int> v = {1, 2, 3, 4, 5};

// 对每个元素执行操作
std::transform(v.begin(), v.end(), v.begin(),
    [](int x) { return x * 2; });    // {2, 4, 6, 8, 10}

std::reverse(v.begin(), v.end());     // 反转

// 删除（需要配合 erase）
auto new_end = std::remove_if(v.begin(), v.end(),
    [](int x) { return x < 4; });
v.erase(new_end, v.end());            // erase-remove 惯用法
```

### 其他

```cpp
std::vector<int> v = {3, 1, 4, 1, 5};

std::accumulate(v.begin(), v.end(), 0);  // 求和（<numeric>）
auto [mn, mx] = std::minmax_element(v.begin(), v.end());
std::for_each(v.begin(), v.end(), [](int x) { std::cout << x; });
```

## 自定义比较器

```cpp
struct Student { std::string name; int score; };

std::vector<Student> students = {{"Alice", 90}, {"Bob", 85}};

std::sort(students.begin(), students.end(),
    [](const Student& a, const Student& b) {
        return a.score > b.score;  // 按分数降序
    });
```

## 相关笔记

- [[STL概览]] — STL 概览
- [[STL迭代器]] — 迭代器
- [[lambda表达式]] — Lambda 与算法配合
- [[STL容器]] — 容器

---

*由奶茶一号整理 🧋*
