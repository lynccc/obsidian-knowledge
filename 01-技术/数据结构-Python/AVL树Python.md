---
tags: [数据结构, Python, Miller, AVL树, 平衡树]
aliases: [AVL树Python实现]
---

# AVL树（Python）

## 🗣️ 通俗讲解

> 普通 BST 可能退化成一条「歪脖子树」，查找变慢。AVL 树的秘诀是：每次插入/删除后，检查每个节点的左右子树高度差，如果差超过 1，就通过「旋转」把树扶正。就像玩积木一样，把偏重的一边转一下，保持整体平衡。

📖 **想看更深入的理论分析？** → [[AVL树]]（邓俊辉 C++ 版）

## 核心概念

AVL树是自平衡BST：任意节点的左右子树高度差（平衡因子）≤ 1。

**关键**：通过旋转操作在插入/删除后恢复平衡，保证所有操作 O(log n)。

## 关键要点

### 平衡因子

```python
def update_balance(self, node):
    if node.balance_factor > 1 or node.balance_factor < -1:
        self.rebalance(node)
        return
    if node.parent is not None:
        if node.is_left_child():
            node.parent.balance_factor += 1
        elif node.is_right_child():
            node.parent.balance_factor -= 1
        if node.parent.balance_factor != 0:
            self.update_balance(node.parent)
```

### 旋转操作

四种情况：

**左旋（Left Rotation）** — 右子树过高：
```
    A             B
     \           / \
      B    →    A   C
       \
        C
```

```python
def rotate_left(self, rot_root):
    new_root = rot_root.right_child
    rot_root.right_child = new_root.left_child
    if new_root.left_child:
        new_root.left_child.parent = rot_root
    new_root.parent = rot_root.parent
    if rot_root.is_root():
        self.root = new_root
    else:
        if rot_root.is_left_child():
            rot_root.parent.left_child = new_root
        else:
            rot_root.parent.right_child = new_root
    new_root.left_child = rot_root
    rot_root.parent = new_root
    rot_root.balance_factor = rot_root.balance_factor + 1 - min(new_root.balance_factor, 0)
    new_root.balance_factor = new_root.balance_factor + 1 + max(rot_root.balance_factor, 0)
```

**右旋（Right Rotation）** — 左子树过高（对称）

**左右双旋** — 左子树的右子树过高：先左旋再右旋

**右左双旋** — 右子树的左子树过高：先右旋再左旋

### rebalance 逻辑

```python
def rebalance(self, node):
    if node.balance_factor < 0:  # 右重
        if node.right_child.balance_factor > 0:
            self.rotate_right(node.right_child)
            self.rotate_left(node)
        else:
            self.rotate_left(node)
    elif node.balance_factor > 0:  # 左重
        if node.left_child.balance_factor < 0:
            self.rotate_left(node.left_child)
            self.rotate_right(node)
        else:
            self.rotate_right(node)
```

## 与其他概念的联系

- ← [[BST-Python]]：AVL是BST的平衡版本
- ← [[AVL树]]：邓俊辉版理论基础
- ← [[平衡二叉搜索树]]：平衡树概论
- 与红黑树相比，AVL更严格平衡，查找更快，但插入/删除旋转更多

## 参考
- 《Python数据结构与算法分析》第2版 §6.8
