---
tags: [C++, 基础, 语法]
aliases: [C++语法, C++基本结构]
created: 2026-06-25
---

# 📝 C++ 基础语法

## 核心概念

- C++ 语句以分号 `;` 结尾
- 代码块用花括号 `{}` 包裹
- 缩进不影响程序逻辑，但影响可读性

## 程序结构

```cpp
#include <iostream>  // 预处理指令

int main() {         // 主函数入口
    // 语句
    std::cout << "Hello" << std::endl;
    return 0;        // 返回语句
}
```

## 注释

```cpp
// 单行注释

/*
   多行注释
   可以跨越多行
*/
```

## 基本输出

```cpp
#include <iostream>

int main() {
    std::cout << "Hello";          // 输出文本
    std::cout << 42;               // 输出数字
    std::cout << "Hello" << " " << "World";  // 链式输出
    std::cout << std::endl;        // 换行
    return 0;
}
```

## 基本输入

```cpp
#include <iostream>

int main() {
    int age;
    std::cout << "请输入年龄: ";
    std::cin >> age;               // 从键盘读取
    std::cout << "你输入了: " << age << std::endl;
    return 0;
}
```

## 命名空间

```cpp
// 完整写法
std::cout << "Hello" << std::endl;

// using 声明
using std::cout;
cout << "Hello" << std::endl;

// using 指令（不推荐在头文件中使用）
using namespace std;
cout << "Hello" << endl;
```

## 相关笔记

- [[05-HelloWorld-CPP]] — 第一个程序
- [[43-编译与链接]] — 编译过程
- [[22-变量-CPP]] — 变量基础

---

*由奶茶一号整理 🧋*

## 📚 参考
- 基于 C++ 内训知识
  补充：[[04-CPP环境搭建]] / [[43-编译与链接]]
