---
tags: [数据结构, Python, Miller, 拓扑排序, 图]
aliases: [拓扑排序Python实现]
---

# 拓扑排序（Python）

## 🗣️ 通俗讲解

> 想象你有好多任务，有些任务必须先完成其他任务才能开始（比如得先买菜才能做饭）。拓扑排序就是帮你排出一个合法的执行顺序——保证每个任务都在它依赖的任务之后执行。如果有循环依赖（A 等 B，B 等 A），那就无解了。

📖 **想看更深入的理论分析？** → [[拓扑排序]]（邓俊辉 C++ 版）

## 核心概念

拓扑排序是对**有向无环图（DAG）**的顶点进行线性排序，使得对每条边 (u, v)，u 排在 v 前面。

经典应用：课程先修关系、任务调度、编译依赖。

## 关键要点

### 基于DFS的实现

利用DFS的**完成时间**（finish time），按完成时间**逆序**排列即得拓扑序。

```python
def topological_sort(g):
    # 先做DFS，记录完成时间
    dfs(g)
    # 按完成时间降序排列
    return sorted(g.get_vertices(),
                   key=lambda v: v.get_finish_time(),
                   reverse=True)
```

DFS过程中，完成时间越晚的顶点，在拓扑排序中越靠前（因为它没有后续依赖，或者后续依赖已完成）。

### 为什么需要DAG？

若图有环，则不存在拓扑排序——环上的顶点互相依赖，无法确定先后顺序。

DFS可以检测环：若DFS过程中遇到**灰色**顶点（正在访问中），说明存在后向边 → 有环。

### 另一种实现：Kahn算法（入度法）

```python
from collections import deque

def kahn_topo_sort(g):
    in_degree = {v: 0 for v in g}
    for u in g:
        for v in g[u]:
            in_degree[v] += 1

    queue = deque([v for v in g if in_degree[v] == 0])
    result = []
    while queue:
        u = queue.popleft()
        result.append(u)
        for v in g[u]:
            in_degree[v] -= 1
            if in_degree[v] == 0:
                queue.append(v)

    if len(result) != len(g):
        raise ValueError("Graph has a cycle")
    return result
```

## 与其他概念的联系

- ← [[拓扑排序]]：邓俊辉版理论
- ← [[DFS-Python]]：拓扑排序基于DFS完成时间
- → [[Dijkstra-Python]]：DAG上求最短路径可用拓扑排序替代优先队列

## 参考
- 《Python数据结构与算法分析》第2版 §7.6
