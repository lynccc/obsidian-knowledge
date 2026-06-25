---
tags: [C++, 控制流, 条件]
aliases: [if语句, switch, 条件判断]
created: 2026-06-25
---

# 🔀 if 语句 — C++

## 核心概念

- `if/else if/else` 实现条件分支
- `switch` 实现多路分支（适合离散值判断）
- 条件表达式的结果为 `bool` 类型

## if / else if / else

```cpp
int score = 85;

if (score >= 90) {
    std::cout << "优秀" << std::endl;
} else if (score >= 80) {
    std::cout << "良好" << std::endl;
} else if (score >= 60) {
    std::cout << "及格" << std::endl;
} else {
    std::cout << "不及格" << std::endl;
}
```

## 条件表达式

```cpp
int x = 10;

if (x) { }            // 非零为 true
if (x > 0 && x < 100) { }  // 逻辑组合
if (!x) { }           // 取反
```

## switch

```cpp
int day = 3;

switch (day) {
    case 1:
        std::cout << "周一" << std::endl;
        break;         // 必须 break，否则穿透
    case 2:
        std::cout << "周二" << std::endl;
        break;
    case 3:
        std::cout << "周三" << std::endl;
        break;
    default:
        std::cout << "其他" << std::endl;
        break;
}
```

## switch 注意事项

```cpp
// ❌ switch 只能用于整型或枚举类型
// switch (3.14) { }  // 编译错误

// ⚠️ 忘记 break 会穿透
switch (1) {
    case 1:
        std::cout << "1";   // 执行
    case 2:
        std::cout << "2";   // 也会执行！
        break;
}

// ✅ C++17 初始化语句
switch (int x = get_value(); x) {
    case 1: break;
}
```

## 相关笔记

- [[运算符]] — 关系运算符
- [[循环-CPP]] — 循环控制
- [[枚举]] — enum 配合 switch

---

*由奶茶一号整理 🧋*

## 📚 参考
- 基于 C++ 内训知识
  补充：[[CPP环境搭建]] / [[编译与链接]]
