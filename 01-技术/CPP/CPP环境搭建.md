---
tags: [C++, 环境, 工具]
aliases: [C++环境配置, 编译器安装]
created: 2026-06-25
---

# 🔧 C++ 环境搭建

## 核心概念

- C++ 需要编译器将源码编译为可执行文件
- 常用编译器：g++（Linux/Mac）、MSVC（Windows）、Clang
- 推荐 IDE：VS Code、CLion、Visual Studio

## 编译器安装

### Linux (Ubuntu/Debian)

```bash
sudo apt update
sudo apt install g++ build-essential
g++ --version  # 验证安装
```

### macOS

```bash
xcode-select --install
g++ --version
```

### Windows

- 安装 [MinGW-w64](https://www.mingw-w64.org/) 或使用 Visual Studio 自带的 MSVC
- 或安装 WSL2 后使用 Linux 方式

## VS Code 配置

1. 安装 VS Code
2. 安装扩展：**C/C++**（Microsoft 官方）
3. 安装扩展：**Code Runner**（一键运行）
4. 配置 `tasks.json` 和 `launch.json` 实现调试

## CLion

- JetBrains 出品，开箱即用
- 自带 CMake 构建系统
- 学生可申请免费许可证

## 验证环境

```cpp
// test.cpp
#include <iostream>
int main() {
    std::cout << "C++ 环境配置成功！" << std::endl;
    return 0;
}
```

```bash
g++ test.cpp -o test && ./test
```

## 相关笔记

- [[HelloWorld-CPP]] — 第一个程序
- [[编译与链接]] — 编译过程详解

---

*由奶茶一号整理 🧋*

## 📚 参考
- 基于 C++ 内训知识
  补充：[[CPP环境搭建]] / [[编译与链接]]
