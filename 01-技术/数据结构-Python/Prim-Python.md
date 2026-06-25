---
tags: [数据结构, Python, Miller, 最小支撑树, 图]
aliases: [Prim算法Python, 最小生成树]
---

# Prim算法（Python）

## 🗣️ 通俗讲解

> 想象你要在几个城市之间修铁路，目标是所有城市都能互通，但总花费最少。Prim 算法的思路是：从任意一个城市开始，每次选一条连接「已修好」和「没修好」城市的最便宜铁路，逐步扩展，直到所有城市连通。跟 Dijkstra 长得很像，但目的不同——Dijkstra 找最短路，Prim 找最小成本网络。

📖 **想看更深入的理论分析？** → [[最小支撑树]]（邓俊辉 C++ 版）

## 核心概念

Prim算法求**最小支撑树（MST）**：从一个起始顶点出发，每次选择连接已选顶点集和未选顶点集的**最小权重边**，逐步扩展，直到所有顶点都被包含。

贪心策略：局部最优 → 全局最优。

## 关键要点

### 实现

```python
import heapq

def prim(graph, start):
    mst = []
    visited = set()
    edges = [(0, start, None)]  # (权重, 当前顶点, 来源顶点)
    total_cost = 0

    while edges and len(visited) < len(graph):
        weight, u, from_v = heapq.heappop(edges)
        if u in visited:
            continue
        visited.add(u)
        if from_v is not None:
            mst.append((from_v, u, weight))
            total_cost += weight

        for v, w in graph[u].get_connections_with_weights():
            if v not in visited:
                heapq.heappush(edges, (w, v, u))

    return mst, total_cost
```

### 书中实现（基于dist数组）

```python
def prim(g, start):
    pq = PriorityQueue()
    for v in g:
        v.set_distance(sys.maxsize)
        v.set_pred(None)
    start.set_distance(0)
    pq.build_heap([(v.get_distance(), v) for v in g])
    while not pq.is_empty():
        current_vert = pq.del_min()
        for next_vert in current_vert.get_connections():
            new_cost = current_vert.get_weight(next_vert)
            if next_vert in pq and new_cost < next_vert.get_distance():
                next_vert.set_pred(current_vert)
                next_vert.set_distance(new_cost)
                pq.decrease_key(next_vert, new_cost)
```

### 复杂度

- 二叉堆实现：O(E log V)
- 与 [[Dijkstra-Python]] 结构几乎相同，区别仅在于：Dijkstra用 **起点到当前的距离** 累加，Prim用 **边的权重** 直接比较

### Prim vs Kruskal

| 特性 | Prim | Kruskal |
|------|------|---------|
| 策略 | 顶点扩展 | 边排序选取 |
| 数据结构 | 优先队列 | 并查集 |
| 适用 | 稠密图 | 稀疏图 |

## 与其他概念的联系

- ← [[最小支撑树]]：邓俊辉版理论（Prim + Kruskal）
- ← [[二叉堆Python]]：堆优化关键
- ← [[图的实现Python]]：基于Graph类
- 与 [[Dijkstra-Python]] 算法结构高度相似

## 参考
- 《Python数据结构与算法分析》第2版 §7.8
