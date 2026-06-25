---
tags: [C++, 现代C++, 循环]
aliases: [range-based for, 范围for]
created: 2026-06-25
---

# 🔁 范围 for

## 核心概念

- 范围 for（Range-based for）是 C++11 引入的简洁遍历语法
- 自动遍历容器或数组的每个元素
- 底层使用迭代器实现

## 基本语法

```cpp
std::vector<int> v = {1, 2, 3, 4, 5};

// 值拷贝
for (int x : v) {
    std::cout << x << " ";
}

// const 引用（只读，推荐）
for (const auto& x : v) {
    std::cout << x << " ";
}

// 非 const 引用（可修改）
for (auto& x : v) {
    x *= 2;
}
```

## 三种形式对比

```cpp
std::vector<int> v = {1, 2, 3};

for (int x : v) { }          // 值拷贝（适合小类型）
for (const auto& x : v) { }  // const 引用（推荐只读场景）
for (auto& x : v) { }        // 非 const 引用（需要修改时）
```

## 遍历不同容器

```cpp
// 数组
int arr[] = {1, 2, 3};
for (int x : arr) { }

// map
std::map<std::string, int> m = {{"a", 1}, {"b", 2}};
for (const auto& [key, val] : m) {  // C++17 结构化绑定
    std::cout << key << ": " << val;
}

// 初始化列表
for (int x : {1, 2, 3, 4, 5}) { }
```

## 注意事项

```cpp
// ❌ 不要在遍历时修改容器大小
for (auto& x : v) {
    if (x == 0) v.push_back(1);  // 未定义行为！
}

// ✅ 需要删除元素时用迭代器
for (auto it = v.begin(); it != v.end(); ) {
    if (*it == 0) it = v.erase(it);
    else ++it;
}
```

## 相关笔记

- [[循环-CPP]] — 其他循环方式
- [[STL迭代器]] — 迭代器详解
- [[自动类型推导]] — auto 关键字
- [[STL容器]] — 各种容器

---

*由奶茶一号整理 🧋*
