---
tags: [数据结构, Python, Miller, 图]
aliases: [图的Python实现, 邻接表实现, Vertex类, Graph类]
---

# 图的实现（Python）

## 核心概念

### 两种存储方式

**邻接矩阵**：二维数组，`matrix[i][j]` 表示边。空间 O(V²)，适合稠密图。

**邻接表**：Python中用 **dict of dict** 实现，空间 O(V+E)，适合稀疏图。

```python
class Vertex:
    def __init__(self, key):
        self.id = key
        self.connected_to = {}  # {neighbor_id: weight}

    def add_neighbor(self, nbr, weight=0):
        self.connected_to[nbr] = weight

    def get_connections(self):
        return self.connected_to.keys()

    def get_weight(self, nbr):
        return self.connected_to[nbr]

class Graph:
    def __init__(self):
        self.vert_list = {}  # {vertex_id: Vertex对象}
        self.num_vertices = 0

    def add_vertex(self, key):
        self.num_vertices += 1
        new_vertex = Vertex(key)
        self.vert_list[key] = new_vertex
        return new_vertex

    def add_edge(self, f, t, weight=0):
        if f not in self.vert_list:
            self.add_vertex(f)
        if t not in self.vert_list:
            self.add_vertex(t)
        self.vert_list[f].add_neighbor(self.vert_list[t], weight)
```

## 关键要点

- **Python特色**：用 `dict` 而非数组实现邻接表，天然支持任意可哈希的顶点标识符（字符串、数字等）
- `vert_list` 是核心：`{id: Vertex}` 字典
- 每个 `Vertex` 内部的 `connected_to` 也是字典：`{Vertex: weight}`
- 有权图和无权图统一处理（无权边 weight=0）
- 有向图只 `add_edge` 一次；无向图需调用两次（双向）

### `__contains__` 和 `__iter__`

```python
def __contains__(self, n):
    return n in self.vert_list

def __iter__(self):
    return iter(self.vert_list.values())
```

## 与其他概念的联系

- ← [[图的存储]]：邓俊辉版理论（邻接矩阵/邻接表/关联矩阵）
- ← [[图的基本概念]]：图的术语
- → [[BFS-Python]]、[[DFS-Python]]：基于此实现的遍历
- → [[Dijkstra-Python]]、[[Prim-Python]]：基于此实现的算法

## 参考
- 《Python数据结构与算法分析》第2版 §7.2-7.3
