---
tags: [C++, 异常, 错误处理]
aliases: [try, catch, throw, 异常处理]
created: 2026-06-25
---

# ⚠️ 异常处理 — C++

## 核心概念

- 异常处理用 `try/catch/throw` 机制
- `throw` 抛出异常，`try` 块捕获，`catch` 处理
- 异常沿调用栈向上传播，直到被捕获

## 基本语法

```cpp
#include <stdexcept>

double divide(int a, int b) {
    if (b == 0) {
        throw std::runtime_error("除数不能为零");
    }
    return static_cast<double>(a) / b;
}

int main() {
    try {
        double result = divide(10, 0);
        std::cout << result << std::endl;
    } catch (const std::runtime_error& e) {
        std::cout << "错误: " << e.what() << std::endl;
    } catch (...) {
        std::cout << "未知异常" << std::endl;
    }
}
```

## 标准异常类

```
std::exception
├── std::logic_error        — 逻辑错误（可预防）
│   ├── std::invalid_argument
│   ├── std::out_of_range
│   └── std::domain_error
└── std::runtime_error      — 运行时错误（不可预防）
    ├── std::overflow_error
    ├── std::underflow_error
    └── std::range_error
```

## 抛出自定义异常

```cpp
class MyException : public std::exception {
    std::string msg;
public:
    MyException(const std::string& m) : msg(m) {}
    const char* what() const noexcept override {
        return msg.c_str();
    }
};

throw MyException("自定义错误");
```

## 异常安全

```cpp
void safe_function() {
    std::vector<int> v;
    v.push_back(1);
    // 如果这里抛异常，v 的析构函数会自动调用（RAII）
    // 所以用智能指针和容器比裸指针更安全
}
```

## 注意事项

- 不要在析构函数中抛异常
- 异常有性能开销，不要用于常规控制流
- 优先使用 RAII（智能指针、容器）管理资源
- `noexcept` 标记不抛异常的函数

## 相关笔记

- [[智能指针]] — RAII 原则
- [[类基础-CPP]] — 异常与类
- [[动态内存]] — 内存管理

---

*由奶茶一号整理 🧋*

## 📚 参考
- 基于 C++ 内训知识
  补充：[[CPP环境搭建]] / [[编译与链接]]
