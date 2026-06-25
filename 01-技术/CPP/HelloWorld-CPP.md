---
tags: [C++, 入门, 基础]
aliases: [Hello World C++, 第一个C++程序]
created: 2026-06-25
---

# 👋 Hello World — C++

## 核心概念

- 第一个 C++ 程序
- 验证编译环境是否正确
- 理解 C++ 程序的基本结构

## 最简单的程序

```cpp
#include <iostream>

int main() {
    std::cout << "Hello, World!" << std::endl;
    return 0;
}
```

输出：`Hello, World!`

## 代码解析

- `#include <iostream>` — 引入输入输出流头文件
- `int main()` — 程序入口函数，每个 C++ 程序必须有且只有一个
- `std::cout` — 标准输出流，`<<` 是输出运算符
- `std::endl` — 换行并刷新缓冲区
- `return 0` — 返回 0 表示程序正常结束

## 编译运行

```bash
# 编译
g++ hello.cpp -o hello

# 运行
./hello
```

## 常见变体

```cpp
#include <iostream>
using namespace std;  // 省略 std:: 前缀

int main() {
    cout << "Hello, World!" << endl;
    return 0;
}
```

> ⚠️ 小项目可以用 `using namespace std`，大项目建议显式写 `std::` 避免命名冲突。

## 常见错误

```cpp
// ❌ 忘记 #include
int main() {
    cout << "Hello";  // 编译错误：cout 未定义
}

// ❌ main 拼写错误
int mian() { }  // 链接错误：找不到 main
```

## 相关笔记

- [[CPP环境搭建]] — 安装编译器
- [[编译与链接]] — 理解编译过程
- [[CPP基础语法]] — C++ 语法基础

---

*由奶茶一号整理 🧋*

## 📚 参考
- 基于 C++ 内训知识
  补充：[[CPP环境搭建]] / [[编译与链接]]
