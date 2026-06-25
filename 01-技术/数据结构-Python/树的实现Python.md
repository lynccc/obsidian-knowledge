---
tags: [数据结构, Python, Miller, 树]
aliases: [树的实现, 列表之列表, 节点与引用]
---

# 树的实现（Python）

## 核心概念

Python中实现树有两种主要方式：

### 1. 列表之列表（List of Lists）

用嵌套列表表示树。每个节点是一个列表：`[root, left, right]`。

```python
def BinaryTree(r):
    return [r, [], []]

def insert_left(root, new_branch):
    t = root.pop(1)
    if t:
        root.insert(1, [new_branch, t, []])
    else:
        root.insert(1, [new_branch, [], []])
    return root

def insert_right(root, new_branch):
    t = root.pop(2)
    if t:
        root.insert(2, [new_branch, [], t])
    else:
        root.insert(2, [new_branch, [], []])
    return root
```

**特点**：利用Python列表的灵活性，`root[0]` 存值，`root[1]` 左子树，`root[2]` 右子树。

### 2. 节点与引用（Nodes and References）

用类和对象引用表示树。每个节点是一个 `TreeNode` 对象：

```python
class BinaryTree:
    def __init__(self, root_obj):
        self.key = root_obj
        self.left_child = None
        self.right_child = None

    def insert_left(self, new_node):
        if self.left_child is None:
            self.left_child = BinaryTree(new_node)
        else:
            t = BinaryTree(new_node)
            t.left_child = self.left_child
            self.left_child = t

    def insert_right(self, new_node):
        # 对称操作
        ...

    def get_root_val(self):
        return self.key

    def set_root_val(self, obj):
        self.key = obj
```

**特点**：更符合OOP思想，指针清晰，适合复杂树操作。

## 关键要点

- **列表之列表**：简单直观，适合教学和快速原型
- **节点与引用**：更灵活，便于扩展（如添加父指针、平衡因子等）
- Python的引用语义使得节点与引用实现非常自然
- 基本操作：`get_root_val`、`set_root_val`、`get_left_child`、`get_right_child`、`insert_left`、`insert_right`

## 与其他概念的联系

- → [[解析树]]：解析树基于这两种实现之一构建
- → [[BST-Python]]：BST是节点与引用实现的特化
- → [[二叉树]]：理论基础

## 参考
- 《Python数据结构与算法分析》第2版 §6.4
