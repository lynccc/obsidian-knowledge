---
tags: [算法导论, CLRS, 中文翻译, 数据结构, 二叉搜索树]
aliases: [Binary Search Trees, 二叉搜索树, BST]
---

# 二叉搜索树（Binary Search Tree）

## 通俗讲解
> 二叉搜索树（BST）是一种很聪明的数据结构，它的组织规则很简单：**左边的都比根小，右边的都比根大**。这个规则对每个节点都成立。
>
> 想象你在一个有序的猜数字游戏中：对方说"我想了一个数"，你猜一个，对方说"大了"或"小了"。BST 就是这样工作的——每次比较都能排除一半的可能性。
>
> 但 BST 有个问题：如果你按顺序插入 1、2、3、4、5，树会退化成一条链，搜索就变成了 O(n)。这就是为什么我们需要[[红黑树CLRS]]这样的平衡 BST。

## 核心概念（中文，附英文术语）

### BST 性质（Binary Search Tree Property）

对于 BST 中的任意节点 x：
- 如果 y 是 x **左子树**中的节点，则 y.key **≤** x.key
- 如果 y 是 x **右子树**中的节点，则 y.key **≥** x.key

**重要推论**：BST 的**中序遍历**（inorder tree walk）会产生一个**递增的有序序列**。

```
INORDER-TREE-WALK(x):
    if x ≠ NIL:
        INORDER-TREE-WALK(x.left)
        print x.key
        INORDER-TREE-WALK(x.right)
```

**时间复杂度**：Θ(n) —— 每个节点恰好访问一次

---

### 搜索（Search）

```
TREE-SEARCH(x, k):
    if x == NIL or k == x.key:
        return x
    if k < x.key:
        return TREE-SEARCH(x.left, k)
    else:
        return TREE-SEARCH(x.right, k)
```

**迭代版本**（更高效）：
```
ITERATIVE-TREE-SEARCH(x, k):
    while x ≠ NIL and k ≠ x.key:
        if k < x.key:
            x = x.left
        else:
            x = x.right
    return x
```

**时间复杂度**：O(h)，h 为树高

---

### 最小值和最大值

**找最小值**：一直往左走
```
TREE-MINIMUM(x):
    while x.left ≠ NIL:
        x = x.left
    return x
```

**找最大值**：一直往右走
```
TREE-MAXIMUM(x):
    while x.right ≠ NIL:
        x = x.right
    return x
```

**时间复杂度**：O(h)

---

### 前驱和后继（Predecessor and Successor）

**后继**（比 x 大的最小元素）：
```
TREE-SUCCESSOR(x):
    if x.right ≠ NIL:
        return TREE-MINIMUM(x.right)    // 右子树的最小值
    y = x.p
    while y ≠ NIL and x == y.right:     // 沿着右孩子向上
        x = y
        y = y.p
    return y                             // 最近的"左祖先"
```

**两种情况**：
1. x 有右子树 → 后继是右子树的最小值
2. x 没有右子树 → 后继是 x 的最近的"左祖先"

**前驱**（比 x 小的最大元素）：对称处理

**时间复杂度**：O(h)

---

### 插入（Insertion）

```
TREE-INSERT(T, z):
    y = NIL                    // y 是 x 的父节点
    x = T.root
    while x ≠ NIL:            // 找到插入位置
        y = x
        if z.key < x.key:
            x = x.left
        else:
            x = x.right
    z.p = y                    // 设置新节点的父节点
    if y == NIL:
        T.root = z             // 树为空
    elseif z.key < y.key:
        y.left = z
    else:
        y.right = z
```

**时间复杂度**：O(h)

**关键点**：新节点总是作为**叶子节点**插入！

---

### 删除（Deletion）

删除节点 z 有三种情况：

#### 情况 1：z 没有孩子
直接删除 z，将父节点的对应孩子指针置为 NIL。

#### 情况 2：z 只有一个孩子
用 z 的唯一孩子替换 z 的位置。

#### 情况 3：z 有两个孩子
1. 找到 z 的**后继** y（z 右子树的最小值，y 一定没有左孩子）
2. 用 y 替换 z 的位置
3. 如果 y 不是 z 的右孩子，先用 y 的右孩子替换 y，再将 z 的右孩子变为 y 的右孩子

```
TREE-DELETE(T, z):
    if z.left == NIL:
        TRANSPLANT(T, z, z.right)
    elseif z.right == NIL:
        TRANSPLANT(T, z, z.left)
    else:
        y = TREE-MINIMUM(z.right)       // z 的后继
        if y.p ≠ z:
            TRANSPLANT(T, y, y.right)
            y.right = z.right
            y.right.p = y
        TRANSPLANT(T, z, y)
        y.left = z.left
        y.left.p = y
```

**时间复杂度**：O(h)

**注意**：情况 3 中，如果后继 y 就是 z 的右孩子，可以简化处理。

## BST 的性能

| 操作 | 平均（随机插入） | 最坏（退化成链） |
|------|----------------|-----------------|
| 搜索 | O(log n) | O(n) |
| 插入 | O(log n) | O(n) |
| 删除 | O(log n) | O(n) |
| 最小/最大 | O(log n) | O(n) |
| 前驱/后继 | O(log n) | O(n) |

**关键问题**：最坏情况下 BST 退化为链表，性能变差。

**解决方案**：
- **随机 BST**：随机插入时，期望树高为 O(log n)
- **平衡 BST**：[[红黑树CLRS]]、AVL 树等保证树高为 O(log n)

## 关键要点

1. **BST 性质**：左 ≤ 根 ≤ 右，中序遍历产生有序序列
2. **所有操作都是 O(h)**：性能取决于树高
3. **插入在叶子，删除分三种情况**：有两个孩子的删除最复杂
4. **随机 BST 期望平衡**：但无法保证最坏情况
5. **需要平衡机制**：红黑树通过旋转和着色保证 O(log n)

## BST vs 其他数据结构

| 特性 | BST | 散列表 | 有序数组 |
|------|-----|--------|---------|
| 搜索 | O(h) | O(1) 期望 | O(log n) |
| 插入 | O(h) | O(1) 期望 | O(n) |
| 删除 | O(h) | O(1) 期望 | O(n) |
| 有序遍历 | O(n) | 不支持 | O(n) |
| 范围查询 | O(h + k) | 不支持 | O(log n + k) |

## 与其他概念的联系

- [[红黑树CLRS]]：自平衡 BST，保证 O(log n)
- [[AVL树]]：另一种平衡 BST
- [[散列表CLRS]]：另一种实现字典的数据结构
- [[堆排序CLRS]]：堆不支持高效的有序遍历
- [[顺序统计量]]：可以在 BST 上扩展支持 rank/select

## 参考
- 《算法导论》第四版 §12.1-12.3
- §12.1 什么是二叉搜索树（What is a binary search tree?）
- §12.2 查询二叉搜索树（Querying a binary search tree）
- §12.3 插入和删除（Insertion and deletion）
