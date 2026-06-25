---
tags: [数据结构, Python, Miller, 面向对象]
aliases: [Python OOP, 类, 继承]
---

# Python面向对象编程

## 核心概念

Python是面向对象语言，通过**类**封装数据和操作，支持**继承**实现代码复用。

## 类的基本结构

### 类定义
```python
class ClassName:
    def __init__(self, 参数):
        """构造方法，初始化实例"""
        self.属性 = 参数
    
    def 方法名(self, 参数):
        """实例方法"""
        pass
```

### 魔术方法（双下方法）

| 方法 | 触发条件 | 用途 |
|------|---------|------|
| `__init__` | `ClassName()` | 初始化实例 |
| `__str__` | `str(obj)` / `print(obj)` | 用户友好的字符串表示 |
| `__repr__` | `repr(obj)` | 开发者友好的表示 |
| `__add__` | `obj1 + obj2` | 加法运算 |
| `__eq__` | `obj1 == obj2` | 相等比较 |
| `__lt__` | `obj1 < obj2` | 小于比较 |
| `__len__` | `len(obj)` | 长度 |
| `__getitem__` | `obj[key]` | 索引访问 |

## 继承

### IS-A关系（继承）
- 子类是父类的特化
- 使用`class Child(Parent)`语法
- 子类继承父类的所有属性和方法

### HAS-A关系（组合）
- 一个类包含另一个类的实例作为属性
- 通过`self.component = OtherClass()`实现
- 优先于继承（组合优于继承）

## 关键要点

1. **封装**：将数据和操作封装在类中
2. **多态**：同一方法在不同类中有不同实现
3. **继承vs组合**：IS-A用继承，HAS-A用组合
4. **self参数**：实例方法的第一个参数，指向实例本身

## 与其他概念的联系

- [[抽象数据类型与数据结构]] - ADT与类的关系
- [[Python数据类型概览]] - 内建类型的面向对象特性

## 代码示例

### Fraction类示例
```python
class Fraction:
    def __init__(self, numerator, denominator):
        self.num = numerator
        self.den = denominator
    
    def __str__(self):
        return f"{self.num}/{self.den}"
    
    def __add__(self, other):
        new_num = self.num * other.den + self.den * other.num
        new_den = self.den * other.den
        return Fraction(new_num, new_den)
    
    def __eq__(self, other):
        return self.num * other.den == self.den * other.num

# 使用
f1 = Fraction(1, 2)
f2 = Fraction(1, 3)
print(f1 + f2)    # 5/6
print(f1 == f2)   # False
```

### 继承示例
```python
class Animal:
    def __init__(self, name):
        self.name = name
    
    def speak(self):
        pass

class Dog(Animal):  # IS-A关系
    def speak(self):
        return "Woof!"

class Kennel:       # HAS-A关系
    def __init__(self):
        self.dogs = []  # 包含Dog实例
```

## 参考
- 《Python数据结构与算法分析》第2版 §1.4.11-1.4.13