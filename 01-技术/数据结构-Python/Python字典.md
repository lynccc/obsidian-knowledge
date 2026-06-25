---
tags: [数据结构, Python, Miller, 字典, 散列表]
aliases: [Python dict, 字典, 散列表]
---

# Python字典

## 核心概念

Python的`dict`是基于**散列表**实现的键值对映射，提供近乎O(1)的查找性能。

## 底层实现

- **数据结构**：散列表（哈希表）
- **冲突解决**：开放寻址法
- **扩容策略**：装载因子超过阈值时扩容
- **键要求**：必须是可哈希对象（不可变类型）

## 常用操作

### 核心操作
| 操作 | 说明 | 平均时间复杂度 |
|------|------|---------------|
| `d[key]` | 获取值 | O(1) |
| `d[key] = value` | 设置值 | O(1) |
| `key in d` | 成员检测 | O(1) |
| `del d[key]` | 删除键值对 | O(1) |
| `d.get(key, default)` | 安全获取 | O(1) |

### 视图方法
| 方法 | 说明 | 返回类型 |
|------|------|---------|
| `d.keys()` | 所有键 | 视图对象 |
| `d.values()` | 所有值 | 视图对象 |
| `d.items()` | 所有键值对 | 视图对象 |
| `len(d)` | 键值对数量 | int |

### 其他操作
| 操作 | 说明 |
|------|------|
| `d.update(other)` | 合并字典 |
| `d.pop(key)` | 删除并返回值 |
| `d.clear()` | 清空字典 |
| `d.copy()` | 浅拷贝 |

## 关键要点

1. **查找O(1)**：散列函数直接定位，无需遍历
2. **键必须可哈希**：`int`、`str`、`tuple`可做键，`list`、`dict`不可
3. **空间换时间**：用额外内存换取查找效率
4. **无序→有序**：Python 3.7+保持插入顺序

## 与其他概念的联系

- [[Python数据结构性能]] - 详细性能分析
- [[Python数据类型概览]] - 与其他类型对比
- [[异序词检测]] - 字典在算法中的应用

## 代码示例

```python
# 创建字典
student = {"name": "Alice", "age": 20, "grade": "A"}

# 基本操作
student["age"] = 21          # 设置值
name = student["name"]       # 获取值
student.get("email", "N/A")  # 安全获取

# 成员检测
if "name" in student:
    print(student["name"])

# 遍历
for key, value in student.items():
    print(f"{key}: {value}")

# 字典解析式
squares = {x: x**2 for x in range(5)}
# {0: 0, 1: 1, 2: 4, 3: 9, 4: 16}
```

## 参考
- 《Python数据结构与算法分析》第2版 §1.4.5