---
tags: [C++, 面向对象, 类]
aliases: [this指针, this]
created: 2026-06-25
---

# 👆 this 指针

## 核心概念

- `this` 是指向当前对象的隐式指针
- 在成员函数内部使用，指向调用该函数的对象
- 用于区分同名的成员变量和参数

## 基本用法

```cpp
class Student {
    std::string name;
    int age;
public:
    Student(const std::string& name, int age) {
        this->name = name;  // this->name 是成员，name 是参数
        this->age = age;
    }

    // 更好的方式：初始化列表
    Student(const std::string& n, int a) : name(n), age(a) {}
};
```

## 返回自身引用

```cpp
class Builder {
    int x, y;
public:
    Builder& set_x(int x) {
        this->x = x;
        return *this;  // 返回自身引用，支持链式调用
    }

    Builder& set_y(int y) {
        this->y = y;
        return *this;
    }
};

// 链式调用
Builder b;
b.set_x(10).set_y(20);
```

## const 成员函数中的 this

```cpp
class Student {
    std::string name;
public:
    // 普通成员函数：this 类型是 Student* const
    void set_name(const std::string& n) {
        this->name = n;  // ✅ 可以修改
    }

    // const 成员函数：this 类型是 const Student* const
    std::string get_name() const {
        // this->name = "x";  // ❌ 不能修改
        return this->name;
    }
};
```

## 什么时候用 this

```cpp
// 1. 参数与成员同名时
void set_age(int age) { this->age = age; }

// 2. 返回自身引用（链式调用）
MyClass& do_something() { /* ... */ return *this; }

// 3. 将自身传递给其他函数
void register(Student* s);
void enroll() { register(this); }
```

## 相关笔记

- [[39-类基础-CPP]] — 类基础
- [[35-构造与析构]] — 构造函数
- [[47-运算符重载]] — 运算符重载

---

*由奶茶一号整理 🧋*

## 📚 参考
- 基于 C++ 内训知识
  补充：[[04-CPP环境搭建]] / [[43-编译与链接]]
