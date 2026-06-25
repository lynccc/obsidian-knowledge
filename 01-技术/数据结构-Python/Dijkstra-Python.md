---
tags: [数据结构, Python, Miller, 最短路径, 图]
aliases: [Dijkstra算法Python, 单源最短路径]
---

# Dijkstra算法（Python）

## 🗣️ 通俗讲解

> 想象你用手机地图导航——Dijkstra 就是那个算法。从你的位置出发，每次选「目前最近的」未探索路口，更新它邻居的距离。贪心地一步步扩展，最终得到到所有地点的最短路线。但注意：如果有「负数距离」的路（不现实），这个算法就不灵了。

📖 **想看更深入的理论分析？** → [[最短路径Dijkstra]]（邓俊辉 C++ 版）

## 核心概念

Dijkstra算法求**单源最短路径**：从一个源点出发，到图中所有其他顶点的最短路径。要求**边权非负**。

核心思想：贪心，每次选取**距离最小的未确定顶点**，用它松弛邻接边。

## 关键要点

### 使用优先队列（二叉堆）的实现

```python
import heapq

def dijkstra(graph, start):
    distances = {v: float('inf') for v in graph}
    distances[start] = 0
    predecessors = {v: None for v in graph}
    pq = [(0, start)]  # (距离, 顶点)
    visited = set()

    while pq:
        curr_dist, u = heapq.heappop(pq)
        if u in visited:
            continue
        visited.add(u)

        for v, weight in graph[u].get_connections_with_weights():
            if v not in visited:
                new_dist = curr_dist + weight
                if new_dist < distances[v]:
                    distances[v] = new_dist
                    predecessors[v] = u
                    heapq.heappush(pq, (new_dist, v))

    return distances, predecessors
```

### 使用书中Graph类的实现

基于 `dist` 数组和 `priority_queue`（简化版，无堆优化）：

```python
def dijkstra(aGraph, start):
    pq = PriorityQueue()
    start.set_distance(0)
    pq.build_heap([(v.get_distance(), v) for v in aGraph])
    while not pq.is_empty():
        current_vert = pq.del_min()
        for next_vert in current_vert.get_connections():
            new_dist = current_vert.get_distance() \
                     + current_vert.get_weight(next_vert)
            if new_dist < next_vert.get_distance():
                next_vert.set_distance(new_dist)
                next_vert.set_pred(current_vert)
                pq.decrease_key(next_vert, new_dist)
```

### 复杂度

| 实现方式 | 时间复杂度 |
|----------|-----------|
| 数组 | O(V²) |
| 二叉堆 | O((V+E) log V) |
| 斐波那契堆 | O(V log V + E) |

### 与其他概念的联系

- ← [[最短路径Dijkstra]]：邓俊辉版理论
- ← [[二叉堆Python]]：堆优化的关键
- ← [[图的实现Python]]：基于Graph类
- 负权边 → 用 Bellman-Ford
- 所有顶点对 → Floyd-Warshall

## 参考
- 《Python数据结构与算法分析》第2版 §7.8
