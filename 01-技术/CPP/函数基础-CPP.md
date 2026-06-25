---
tags: [C++, 函数, 基础]
aliases: [函数定义, 函数声明, 参数传递]
created: 2026-06-25
---

# 🔧 函数基础 — C++

## 核心概念

- 函数是可复用的代码块
- 函数需先声明（或定义）后调用
- C++ 参数传递有值传递、指针传递、引用传递

## 函数定义

```cpp
// 返回类型 函数名(参数列表) { 函数体 }
int add(int a, int b) {
    return a + b;
}

// 无返回值
void print_hello() {
    std::cout << "Hello!" << std::endl;
}
```

## 函数声明（原型）

```cpp
// 声明（通常放在头文件）
int add(int a, int b);

// 定义（放在源文件）
int add(int a, int b) {
    return a + b;
}
```

## 参数传递

```cpp
// 值传递 — 修改不影响原变量
void change(int x) { x = 100; }

// 引用传递 — 修改会影响原变量
void change_ref(int& x) { x = 100; }

// 指针传递 — 通过地址修改
void change_ptr(int* x) { *x = 100; }

int main() {
    int a = 10;
    change(a);       // a 仍为 10
    change_ref(a);   // a 变为 100
    change_ptr(&a);  // a 变为 100
}
```

## 默认参数

```cpp
void greet(std::string name, std::string greeting = "Hello") {
    std::cout << greeting << ", " << name << std::endl;
}

greet("Alice");              // Hello, Alice
greet("Bob", "Hi");          // Hi, Bob
```

## 函数返回

```cpp
int square(int x) { return x * x; }   // 返回值
void do_something() { return; }        // void 可省略 return

// 返回多个值（用引用参数或结构体）
void get_min_max(int arr[], int n, int& min_val, int& max_val) {
    min_val = arr[0]; max_val = arr[0];
    for (int i = 1; i < n; i++) {
        if (arr[i] < min_val) min_val = arr[i];
        if (arr[i] > max_val) max_val = arr[i];
    }
}
```

## 相关笔记

- [[函数重载]] — 同名不同参
- [[内联函数]] — inline
- [[递归-CPP]] — 递归函数
- [[引用]] — 引用详解

---

*由奶茶一号整理 🧋*

## 📚 参考
- 基于 C++ 内训知识
  补充：[[CPP环境搭建]] / [[编译与链接]]
