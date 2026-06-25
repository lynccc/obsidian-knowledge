---
tags: [数据结构, Python, Miller, BFS, 图]
aliases: [宽度优先搜索Python, 词梯问题]
---

# 宽度优先搜索 BFS（Python）

## 🗣️ 通俗讲解

> 想象往水里扔一颗石子——波纹从落点一圈一圈向外扩散。BFS 就是这样：从起点开始，先访问所有「距离为 1」的邻居，再访问「距离为 2」的……用队列管理待访问的顶点，保证「先来先服务」。

📖 **想看更深入的理论分析？** → [[广度优先搜索BFS]]（邓俊辉 C++ 版）

## 核心概念

BFS从起始顶点出发，按**层级**逐层探索：先访问所有距离为1的顶点，再距离为2的……使用**队列**管理待访问顶点。

## 关键要点

### 词梯问题（Word Ladder）

将一个单词变换为另一个单词，每次只改一个字母，求最短变换序列。如：`FOOL → SAGE`。

**建图**：将只差一个字母的单词连边，然后BFS求最短路径。

```python
from pythonds.graphs import Graph, Vertex
from pythonds.basic import Queue

def bfs(g, start):
    start.set_distance(0)
    start.set_pred(None)
    vert_queue = Queue()
    vert_queue.enqueue(start)
    while not vert_queue.is_empty():
        current_vert = vert_queue.dequeue()
        for nbr in current_vert.get_connections():
            if nbr.getColor() == 'white':
                nbr.setColor('gray')
                nbr.set_distance(current_vert.get_distance() + 1)
                nbr.set_pred(current_vert)
                vert_queue.enqueue(nbr)
        current_vert.setColor('black')
```

### BFS关键属性

- **颜色标记**：白色=未访问，灰色=已发现待探索，黑色=已完全探索
- **距离**：从起点到每个顶点的最短跳数
- **前驱**：用于重建最短路径

### 路径回溯

```python
def traverse(y):
    x = y
    while x.get_pred():
        print(x.getId())
        x = x.get_pred()
    print(x.getId())
```

### 复杂度

- 时间：O(V + E)
- 空间：O(V)

## 与其他概念的联系

- ← [[广度优先搜索BFS]]：邓俊辉版理论
- ← [[图的实现Python]]：基于Graph/Vertex类
- → [[DFS-Python]]：对比两种遍历策略
- BFS保证无权图最短路径；有权图需 [[Dijkstra-Python]]

## 参考
- 《Python数据结构与算法分析》第2版 §7.4
