---
tags: [C++, 文件IO, 基础]
aliases: [fstream, 文件读写, 文件操作]
created: 2026-06-25
---

# 📁 文件操作 — C++

## 核心概念

- C++ 通过流（Stream）进行文件操作
- `ifstream` 读取文件，`ofstream` 写入文件，`fstream` 读写
- 使用 RAII 自动关闭文件

## 写入文件

```cpp
#include <fstream>

// ofstream — 输出文件流
std::ofstream out("output.txt");
if (out.is_open()) {
    out << "Hello, File!" << std::endl;
    out << "第二行" << std::endl;
    out.close();
}

// 追加模式
std::ofstream out2("output.txt", std::ios::app);
out2 << "追加的内容" << std::endl;
```

## 读取文件

```cpp
#include <fstream>
#include <string>

// 逐行读取
std::ifstream in("input.txt");
if (in.is_open()) {
    std::string line;
    while (std::getline(in, line)) {
        std::cout << line << std::endl;
    }
    in.close();
}
```

## 读取所有内容

```cpp
#include <fstream>
#include <sstream>

std::ifstream in("input.txt");
if (in) {
    std::stringstream buffer;
    buffer << in.rdbuf();
    std::string content = buffer.str();
}
```

## 二进制文件

```cpp
// 写入二进制
std::ofstream out("data.bin", std::ios::binary);
int data[] = {1, 2, 3, 4, 5};
out.write(reinterpret_cast<char*>(data), sizeof(data));

// 读取二进制
std::ifstream in("data.bin", std::ios::binary);
int buf[5];
in.read(reinterpret_cast<char*>(buf), sizeof(buf));
```

## 文件模式

| 模式 | 说明 |
|------|------|
| `ios::in` | 读取 |
| `ios::out` | 写入 |
| `ios::app` | 追加 |
| `ios::trunc` | 覆盖（默认） |
| `ios::binary` | 二进制模式 |

## 检查文件状态

```cpp
std::ifstream in("file.txt");
if (!in) {
    std::cout << "文件打开失败" << std::endl;
}
if (in.eof()) { }    // 是否到末尾
if (in.fail()) { }   // 是否失败
```

## 相关笔记

- [[字符串-CPP]] — 字符串处理
- [[异常处理-CPP]] — 错误处理
- [[STL概览]] — 流与 STL

---

*由奶茶一号整理 🧋*
