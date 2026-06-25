---
tags: [C++, 字符串, 基础]
aliases: [C字符串, C风格字符串]
created: 2026-06-25
---

# 📝 字符串 — C++

## 核心概念

- C 风格字符串：字符数组，以 `\0` 结尾
- `std::string`：C++ 标准库字符串类，更安全易用
- 推荐使用 `std::string`

## C 风格字符串

```cpp
char str1[] = "Hello";            // 自动添加 \0
char str2[6] = {'H','e','l','l','o','\0'};  // 手动
char str3[] = {'H','e','l','l','o'};        // ⚠️ 没有 \0，危险

#include <cstring>
strlen(str1);        // 长度（不含 \0）
strcpy(dest, src);   // 复制
strcmp(a, b);        // 比较（0=相等）
strcat(dest, src);   // 拼接
```

## std::string（推荐）

```cpp
#include <string>

std::string s1 = "Hello";
std::string s2("World");
std::string s3 = s1 + " " + s2;  // 拼接

s1.size();           // 长度
s1.empty();          // 是否为空
s1[0];               // 访问字符
s1.substr(0, 3);     // 子串 "Hel"
s1.find("ll");       // 查找位置（2）
s1.append("!");      // 追加
```

## 输入字符串

```cpp
std::string name;
std::cin >> name;              // 读到空格停止
std::getline(std::cin, name);  // 读取整行
```

## 字符串与数字转换

```cpp
// 字符串 → 数字
int n = std::stoi("42");
double d = std::stod("3.14");

// 数字 → 字符串
std::string s = std::to_string(42);
```

## 相关笔记

- [[std-string]] — std::string 详解
- [[字符与字符串-Python]] — 对比 Python 字符串
- [[数组-CPP]] — 字符数组

---

*由奶茶一号整理 🧋*
