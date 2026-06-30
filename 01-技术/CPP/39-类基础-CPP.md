---
tags: [C++, 面向对象, 类]
aliases: [class, 成员变量, 成员函数, 访问控制]
created: 2026-06-25
---

# 🏗️ 类基础 — C++

## 核心概念

- 类（Class）是面向对象编程的基础
- 将数据（成员变量）和操作（成员函数）封装在一起
- 通过访问控制实现封装

## 定义类

```cpp
class Circle {
private:          // 私有：只能在类内访问
    double radius;

public:           // 公开：任何地方都能访问
    Circle(double r) : radius(r) {}   // 构造函数

    double area() {
        return 3.14159 * radius * radius;
    }

    double get_radius() const {       // const 成员函数
        return radius;
    }

    void set_radius(double r) {
        if (r > 0) radius = r;
    }
};
```

## 访问控制

```cpp
class Example {
public:       // 公开：外部可访问
    int a;

protected:    // 保护：类内和子类可访问
    int b;

private:      // 私有：仅类内可访问
    int c;
};
```

## 创建对象

```cpp
Circle c1(5.0);             // 栈上创建
Circle* c2 = new Circle(3.0);  // 堆上创建

c1.area();                  // 调用成员函数
c2->area();                 // 指针用箭头

delete c2;                  // 堆上对象需手动释放
```

## const 成员函数

```cpp
class Student {
    std::string name;
public:
    // const 函数承诺不修改成员
    std::string get_name() const {
        return name;    // 只能读取
    }
};

// const 对象只能调用 const 函数
const Student s{"Alice"};
s.get_name();   // ✅
// s.set_name("Bob");  // ❌
```

## struct vs class

- `struct` 默认 `public`，`class` 默认 `private`
- 纯数据聚合用 `struct`，有行为封装用 `class`

## 相关笔记

- [[35-构造与析构]] — 构造/析构函数
- [[15-this指针]] — this 指针
- [[42-继承-CPP]] — 继承
- [[26-封装]] — 封装详解

---

*由奶茶一号整理 🧋*

## 📚 参考
- 基于 C++ 内训知识
  补充：[[04-CPP环境搭建]] / [[43-编译与链接]]
