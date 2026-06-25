---
tags: [数据结构, Python, Miller, BST, 搜索树]
aliases: [二叉搜索树Python实现]
---

# 二叉搜索树（Python）

## 🗣️ 通俗讲解

> 想象一个猜数字游戏：根节点是「标准答案」，比它小的放左边，比它大的放右边。这样找数字就像二分查找一样快。但如果数据本身是排好序的，树就会退化成一条链，查找变慢——所以后来有了 AVL 树来「扶正」。

📖 **想看更深入的理论分析？** → [[二叉搜索树BST]]（邓俊辉 C++ 版）

## 核心概念

BST性质：左子树所有节点 < 根 < 右子树所有节点。中序遍历得到有序序列。

用**节点与引用**方式实现：

```python
class TreeNode:
    def __init__(self, key, val=None, left=None, right=None, parent=None):
        self.key = key
        self.payload = val
        self.left_child = left
        self.right_child = right
        self.parent = parent

class BinarySearchTree:
    def __init__(self):
        self.root = None
        self.size = 0
```

## 关键要点

### 核心操作

| 操作 | 平均 | 最坏 |
|------|------|------|
| 查找 | O(log n) | O(n) |
| 插入 | O(log n) | O(n) |
| 删除 | O(log n) | O(n) |

```python
def _put(self, key, val, current_node):
    if key < current_node.key:
        if current_node.has_left_child():
            self._put(key, val, current_node.left_child)
        else:
            current_node.left_child = TreeNode(key, val, parent=current_node)
    else:
        if current_node.has_right_child():
            self._put(key, val, current_node.right_child)
        else:
            current_node.right_child = TreeNode(key, val, parent=current_node)
```

### 删除操作（最复杂）

三种情况：
1. **叶子节点**：直接删除
2. **一个子节点**：用子节点替代
3. **两个子节点**：找右子树最小节点（后继）替代

```python
def splice_out(self):
    """摘取节点（用于删除时替换）"""
    if self.is_leaf():
        if self.is_left_child():
            self.parent.left_child = None
        else:
            self.parent.right_child = None
    elif self.has_any_children():
        if self.has_left_child():
            if self.is_left_child():
                self.parent.left_child = self.left_child
            else:
                self.parent.right_child = self.left_child
            self.left_child.parent = self.parent
        else:
            # 对称处理右子节点
            ...
```

### Python特殊实现：`__contains__` 和 `__getitem__`

```python
def __contains__(self, key):
    if self._get(key, self.root):
        return True
    return False

def __getitem__(self, key):
    return self.get(key)
```

使得可以用 `key in bst` 和 `bst[key]` 语法。

## 与其他概念的联系

- ← [[二叉搜索树BST]]：邓俊辉版理论基础
- → [[AVL树Python]]：BST的平衡版本，解决最坏情况
- → [[平衡二叉搜索树]]：平衡树概论
- BST性能依赖于树的平衡性，退化为链表时最坏 O(n)

## 参考
- 《Python数据结构与算法分析》第2版 §6.7
