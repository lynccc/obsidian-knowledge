---
tags: [C++, STL, 字符串]
aliases: [std::string详解, string类]
created: 2026-06-25
---

# 📝 std::string 详解

## 核心概念

- `std::string` 是标准库字符串类，管理字符序列
- 自动管理内存，支持动态增长
- 丰富的成员函数，比 C 风格字符串安全得多

## 基本操作

```cpp
#include <string>

std::string s1 = "Hello";
std::string s2("World");
std::string s3(5, 'A');       // "AAAAA"

s1.size();          // 长度 5
s1.length();        // 同 size()
s1.empty();         // 是否为空
s1.clear();         // 清空
s1 += " World";     // 拼接
s1.append("!");     // 追加
```

## 访问字符

```cpp
std::string s = "Hello";

s[0];           // 'H'（不检查越界）
s.at(1);        // 'e'（越界抛异常）
s.front();      // 'H'
s.back();       // 'o'
s.c_str();      // C 风格字符串指针
```

## 查找与替换

```cpp
std::string s = "Hello World";

s.find("World");           // 6（位置）
s.find("xyz");             // string::npos（未找到）
s.replace(6, 5, "C++");   // "Hello C++"
s.substr(0, 5);            // "Hello"
s.insert(5, ",");          // "Hello, World"
s.erase(5, 2);             // "HelloWorld"
```

## 比较

```cpp
std::string a = "apple";
std::string b = "banana";

a == b;    // false
a != b;    // true
a < b;     // true（字典序）
a.compare(b);  // 负数（a < b）
```

## 字符串与数字转换

```cpp
// 字符串 → 数字
int n = std::stoi("42");
long l = std::stol("123456");
float f = std::stof("3.14");
double d = std::stod("2.718");

// 数字 → 字符串
std::string s1 = std::to_string(42);
std::string s2 = std::to_string(3.14);
```

## 输入

```cpp
std::string s;
std::cin >> s;               // 读到空格停止
std::getline(std::cin, s);   // 读整行
```

## 相关笔记

- [[字符串-CPP]] — C 风格字符串
- [[std-vector]] — vector 详解
- [[STL容器]] — 容器概览

---

*由奶茶一号整理 🧋*
