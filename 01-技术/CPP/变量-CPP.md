---
tags: [C++, 变量, 基础]
aliases: [C++变量, 变量声明]
created: 2026-06-25
---

# 📦 C++ 变量

## 核心概念

- 变量是命名的内存空间，用于存储数据
- C++ 是**静态类型**语言，变量必须先声明类型
- 变量使用前必须初始化

## 变量声明与初始化

```cpp
int age;              // 声明（未初始化，值不确定）
int score = 100;      // 拷贝初始化
int height(180);      // 直接初始化（C++风格）
int weight{75};       // 列表初始化（C++11，推荐）

// 多变量声明
int a = 1, b = 2, c = 3;
```

## 命名规则

```cpp
// ✅ 合法命名
int student_count = 30;
int _count = 0;
int MAX_SIZE = 100;  // 常量常用全大写

// ❌ 非法命名
int 2name = 0;       // 不能以数字开头
int my name = 0;     // 不能有空格
int int = 0;         // 不能使用关键字
```

## 命名建议

- 使用小写字母和下划线：`student_name`
- 常量用全大写：`MAX_SIZE`
- 类名用大驼峰：`StudentInfo`
- 变量名要有意义，避免单字母（循环变量除外）

## 变量作用域

```cpp
int main() {
    int x = 10;        // 局部变量
    {
        int y = 20;    // 块作用域
        // x 和 y 都可访问
    }
    // y 不可访问
    return 0;
}
```

## 相关笔记

- [[基本数据类型]] — int/float/double/char
- [[常量]] — const、constexpr
- [[CPP基础语法]] — 基本语法

---

*由奶茶一号整理 🧋*

## 📚 参考
- 基于 C++ 内训知识
  补充：[[CPP环境搭建]] / [[编译与链接]]
