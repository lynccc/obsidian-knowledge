---
tags: [算法导论, CLRS, 图算法, BFS, DFS, 拓扑排序, 强连通分量]
aliases: [Elementary Graph Algorithms, Chapter 20]
---

# 图算法基础（CLRS 第20章）

## 通俗讲解
> 图算法是处理网络、依赖关系、连通性等问题的基础工具。本章从图的两种基本表示（邻接矩阵和邻接链表）出发，介绍两种核心遍历方式——BFS（广度优先搜索）和 DFS（深度优先搜索），然后在此基础上推导出拓扑排序和强连通分量算法。这些算法的时间复杂度都是 O(V+E)，非常高效。

## 图的表示（Graph Representation）

### 邻接矩阵（Adjacency Matrix）
- 用 n×n 矩阵 A 表示，A[i][j] = 1 表示存在边 (i,j)
- **空间**：O(V²)，适合稠密图（Dense Graph）
- **查询边**：O(1)
- **遍历所有邻居**：O(V)

### 邻接链表（Adjacency List）
- 每个顶点维护一个链表，存储其所有邻居
- **空间**：O(V+E)，适合稀疏图（Sparse Graph）
- **查询边**：O(degree(v))
- **遍历所有邻居**：O(degree(v))

> **CLRS 默认使用邻接链表**，因为大多数真实图是稀疏的。

### 边的属性
- **权重**（Weight）：w(u,v)，最短路径问题中使用
- **方向**：有向图（Directed）vs 无向图（Undirected）
- **自环**（Self-loop）：通常不允许

## 广度优先搜索 BFS（Breadth-First Search）

> 🔗 已有笔记：[[广度优先搜索BFS]]

### 核心思想
从源点 s 出发，按**距离递增**的顺序逐层探索顶点。使用**队列**（FIFO）管理待探索顶点。

### 算法伪代码
```
BFS(G, s):
  for each vertex u ∈ V - {s}
    u.color = WHITE; u.d = ∞; u.π = NIL
  s.color = GRAY; s.d = 0; s.π = NIL
  Q = ∅
  ENQUEUE(Q, s)
  while Q ≠ ∅
    u = DEQUEUE(Q)
    for each v ∈ Adj[u]
      if v.color == WHITE
        v.color = GRAY
        v.d = u.d + 1
        v.π = u
        ENQUEUE(Q, v)
    u.color = BLACK
```

### 颜色含义
- **WHITE**：未发现
- **GRAY**：已发现但未完全探索（在队列中）
- **BLACK**：已完全探索

### 时间复杂度
**O(V + E)**——每个顶点入队/出队一次，每条边被检查一次。

### 关键性质
1. **最短路径**：BFS 计算的是从源点到各顶点的**最少边数**（无权图的最短路径）
2. **BFS 树**：前驱子图 G_π 是一棵树
3. **三角不等式**：对于边 (u,v)，有 v.d ≤ u.d + 1
4. **层序性质**：同一层的顶点具有相同的 d 值

### 与邓俊辉版的差异
邓俊辉版中 BFS 作为图遍历的基本方式介绍，重点在于遍历本身；CLRS 版更强调 BFS 作为最短路径算法的性质，以及与后续加权最短路径算法的联系。

## 深度优先搜索 DFS（Depth-First Search）

> 🔗 已有笔记：[[深度优先搜索DFS]]

### 核心思想
从源点出发，沿着一条路径尽可能深入探索，遇到死胡同后**回溯**（Backtrack）。使用**递归**（隐式栈）管理探索过程。

### 算法伪代码
```
DFS(G):
  for each vertex u ∈ V
    u.color = WHITE; u.π = NIL
  time = 0
  for each vertex u ∈ V
    if u.color == WHITE
      DFS-VISIT(G, u)

DFS-VISIT(G, u):
  time = time + 1
  u.d = time          // 发现时间
  u.color = GRAY
  for each v ∈ Adj[u]
    if v.color == WHITE
      v.π = u
      DFS-VISIT(G, v)
  u.color = BLACK
  time = time + 1
  u.f = time          // 完成时间
```

### 时间复杂度
**O(V + E)**——每个顶点被 DFS-VISIT 调用一次，每条边被检查一次。

### 时间戳的性质
- **发现时间 u.d**：顶点 u 被首次发现的时间
- **完成时间 u.f**：顶点 u 的邻接链表被完全探索的时间
- **括号定理**（Parenthesis Theorem）：对于任意两个顶点 u 和 v，以下三种情况恰有一种成立：
  1. [u.d, u.f] 和 [v.d, v.f] 完全不相交
  2. [u.d, u.f] 完全包含在 [v.d, v.f] 内（u 是 v 的后代）
  3. [v.d, v.f] 完全包含在 [u.d, u.f] 内（v 是 u 的后代）

### 边的分类
DFS 将边分为四类：

| 边类型 | 含义 | 无向图 | 有向图 |
|--------|------|--------|--------|
| **树边**（Tree Edge） | DFS 树中的边 | ✅ | ✅ |
| **后向边**（Back Edge） | 指向祖先的边 | ✅ | ✅ |
| **前向边**（Forward Edge） | 指向后代的非树边 | ❌ | ✅ |
| **横跨边**（Cross Edge） | 其他边 | ❌ | ✅ |

> **关键定理**：无向图中只有树边和后向边（定理 20.10）。

### 白色路径定理（White-Path Theorem）
在 DFS 森林中，顶点 v 是顶点 u 的后代，当且仅当在 u 被发现的时刻 u.d，存在一条从 u 到 v 的全由白色顶点组成的路径。

### 与邓俊辉版的差异
邓俊辉版的 DFS 介绍更侧重于遍历策略和递归结构；CLRS 版增加了边的分类、括号定理、白色路径定理等更深入的理论分析，为后续拓扑排序和 SCC 算法奠定基础。

## 拓扑排序（Topological Sort）

> 🔗 已有笔记：[[拓扑排序]]

### 定义
对有向无环图（DAG, Directed Acyclic Graph）进行线性排序，使得对于每条边 (u,v)，u 在排序中出现在 v 之前。

### 算法
利用 DFS 的**完成时间**：
1. 对 DAG 运行 DFS
2. 按完成时间**降序**排列顶点

```
TOPOLOGICAL-SORT(G):
  call DFS(G)
  output vertices in order of decreasing finish times
```

### 时间复杂度
**O(V + E)**——只需一次 DFS。

### 正确性证明
关键引理：对于 DAG 中的边 (u,v)，必有 u.f > v.f（即 u 在 v 之后完成）。
- 如果 v 在 u 之前完成，且存在边 (u,v)，则当 u 被探索时 v 是灰色的（正在被探索），说明存在从 v 到 u 的路径，加上边 (u,v) 构成环——矛盾。

### 应用
- 任务调度（Task Scheduling）
- 编译顺序（Makefile）
- 课程先修关系

## 强连通分量 SCC（Strongly Connected Components）

### 定义
有向图 G = (V, E) 的**强连通分量**是一个最大顶点集合 C ⊆ V，使得 C 中任意两个顶点互相可达。

### Kosaraju 算法（CLRS 采用）

> 注意：CLRS 采用的是 Kosaraju 算法（归功于 S.R. Kosaraju 和 Sharir），而非 Tarjan 算法。

#### 算法步骤
```
STRONGLY-CONNECTED-COMPONENTS(G):
  1. 对 G 运行 DFS，计算每个顶点的完成时间 u.f
  2. 计算 G 的转置图 G^T
  3. 对 G^T 运行 DFS，按第一轮完成时间降序选择起始顶点
  4. 输出每棵 DFS 树的顶点作为一个强连通分量
```

#### 时间复杂度
**O(V + E)**——两次 DFS。

#### 核心思想
- **第一轮 DFS**：计算完成时间，确定 SCC 的处理顺序
- **转置图**：G 和 G^T 具有相同的 SCC
- **第二轮 DFS**：按完成时间降序处理，保证每个 SCC 的 DFS 树不会"跨越"到其他 SCC

#### 关键引理
**引理 20.14**：设 C 和 C' 是不同的 SCC，若存在边 (u,v) 从 C' 到 C，则 f(C') > f(C)。

**推论 20.15**：若 f(C) > f(C')，则 G^T 中不存在从 C 到 C' 的边。

### SCC 的性质
- SCC 形成 DAG 的"缩点"（Component Graph G_SCC）
- G_SCC 是无环的
- 第二轮 DFS 按拓扑逆序访问 SCC

### 与邓俊辉版的差异
邓俊辉版通常介绍 Tarjan 算法或 Kosaraju 算法的简化版本；CLRS 版对 Kosaraju 算法的正确性给出了严格的数学证明（包括引理 20.13、20.14、推论 20.15 和定理 20.16），并讨论了 SCC 图的拓扑排序性质。

## 总结对比

| 算法 | 时间复杂度 | 数据结构 | 应用场景 |
|------|-----------|----------|----------|
| BFS | O(V+E) | 队列 | 最短路径（无权）、层序遍历 |
| DFS | O(V+E) | 栈（递归） | 拓扑排序、SCC、连通性 |
| 拓扑排序 | O(V+E) | DFS | DAG 的线性排序、任务调度 |
| SCC | O(V+E) | DFS + 转置图 | 有向图的连通性分析 |

## 与其他笔记的联系
- [[广度优先搜索BFS]]：BFS 的详细实现和性质
- [[深度优先搜索DFS]]：DFS 的详细实现和性质
- [[拓扑排序]]：拓扑排序的更多应用
- [[最小生成树CLRS]]：DFS 在图算法中的广泛应用
- [[单源最短路径CLRS]]：BFS 是无权图的最短路径算法

## 参考
- 《算法导论》第四版 第20章（§20.1-20.5）
- §20.1 图的表示（邻接矩阵、邻接链表）
- §20.2 广度优先搜索
- §20.3 深度优先搜索
- §20.4 拓扑排序
- §20.5 强连通分量
