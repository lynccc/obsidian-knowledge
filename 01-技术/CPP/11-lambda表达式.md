---
tags: [C++, 现代C++, lambda]
aliases: [lambda表达式, 匿名函数]
created: 2026-06-25
---

# 🎯 lambda 表达式

## 核心概念

- Lambda 是匿名函数（C++11），常用于短小的回调
- 语法：`[捕获列表](参数列表) -> 返回类型 { 函数体 }`
- 与 STL 算法配合使用非常强大

## 基本语法

```cpp
// 最简单的 lambda
auto greet = []() { std::cout << "Hello!"; };
greet();  // 调用

// 带参数
auto add = [](int a, int b) { return a + b; };
int result = add(3, 5);  // 8

// 指定返回类型
auto divide = [](double a, double b) -> double {
    if (b == 0) return 0;
    return a / b;
};
```

## 捕获列表

```cpp
int x = 10;
int y = 20;

auto f1 = [x]() { return x; };       // 值捕获（拷贝）
auto f2 = [&x]() { x++; return x; }; // 引用捕获（可修改）
auto f3 = [=]() { return x + y; };   // 值捕获所有外部变量
auto f4 = [&]() { x++; y++; };       // 引用捕获所有
auto f5 = [x, &y]() { return x + y; }; // 混合捕获
```

## mutable lambda

```cpp
int count = 0;
auto counter = [count]() mutable {
    return ++count;  // mutable 允许修改值捕获的副本
};
counter();  // 1
counter();  // 2
// count 仍然是 0（修改的是副本）
```

## 配合 STL 算法

```cpp
std::vector<int> v = {3, 1, 4, 1, 5, 9};

// 排序（自定义比较）
std::sort(v.begin(), v.end(), [](int a, int b) {
    return a > b;  // 降序
});

// 查找
auto it = std::find_if(v.begin(), v.end(), [](int x) {
    return x > 4;
});

// 转换
std::transform(v.begin(), v.end(), v.begin(),
    [](int x) { return x * 2; });

// 过滤
v.erase(std::remove_if(v.begin(), v.end(),
    [](int x) { return x < 3; }), v.end());
```

## 泛型 Lambda（C++14）

```cpp
auto print = [](const auto& x) {
    std::cout << x << std::endl;
};

print(42);        // int
print("hello");   // const char*
print(3.14);      // double
```

## 相关笔记

- [[08-STL算法]] — 算法配合 lambda
- [[44-自动类型推导]] — auto 推导 lambda 类型
- [[17-函数基础-CPP]] — 函数基础

---

*由奶茶一号整理 🧋*

## 📚 参考
- 基于 C++ 内训知识
  补充：[[04-CPP环境搭建]] / [[43-编译与链接]]
