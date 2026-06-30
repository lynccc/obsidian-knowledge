---
tags: [C++, 面向对象, 继承]
aliases: [继承, 公有继承, 虚继承]
created: 2026-06-25
---

# 🧬 继承 — C++

## 核心概念

- 继承（Inheritance）让子类复用父类的成员
- `public` 继承最常用，保持 "is-a" 关系
- 支持多重继承，但需注意菱形继承问题

## 基本继承

```cpp
class Animal {
protected:
    std::string name;
public:
    Animal(const std::string& n) : name(n) {}
    void eat() { std::cout << name << " is eating" << std::endl; }
};

class Dog : public Animal {
public:
    Dog(const std::string& n) : Animal(n) {}  // 调用父类构造
    void bark() { std::cout << name << " says woof!" << std::endl; }
};

Dog d("Buddy");
d.eat();    // 继承自 Animal
d.bark();   // Dog 自己的方法
```

## 继承方式

```cpp
class Derived : public Base { };    // 公有继承（最常用）
class Derived : protected Base { }; // 保护继承
class Derived : private Base { };   // 私有继承
```

| 继承方式 | 父类 public | 父类 protected | 父类 private |
|---------|------------|---------------|-------------|
| public | public | protected | 不可访问 |
| protected | protected | protected | 不可访问 |
| private | private | private | 不可访问 |

## 多重继承

```cpp
class Flyable {
public:
    void fly() { }
};

class Swimmable {
public:
    void swim() { }
};

class Duck : public Flyable, public Swimmable {
    // 同时拥有 fly() 和 swim()
};
```

## 虚继承（解决菱形问题）

```cpp
class Animal {
public:
    int age;
};

// 虚继承：避免菱形继承中的数据重复
class Bird : virtual public Animal { };
class Fish : virtual public Animal { };

class FlyingFish : public Bird, public Fish {
    // 只有一份 age
};
```

## 相关笔记

- [[24-多态]] — 虚函数与多态
- [[39-类基础-CPP]] — 类基础
- [[26-封装]] — 访问控制

---

*由奶茶一号整理 🧋*

## 📚 参考
- 基于 C++ 内训知识
  补充：[[04-CPP环境搭建]] / [[43-编译与链接]]
