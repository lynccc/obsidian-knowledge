---
tags: [算法导论, CLRS, 中文翻译, MOC, 图算法]
aliases: [Part VI Graph Algorithms]
---

# 第六部分：图算法

## 通俗讲解
> 图算法是算法导论中最丰富、最实用的部分之一。从基本的图遍历（BFS/DFS）出发，到最小生成树、最短路径、最大流，再到二分图匹配，这些算法构成了网络优化和组合优化的核心工具箱。与邓俊辉版《数据结构》相比，CLRS 版特别强调了 Bellman-Ford（处理负权边）、Floyd-Warshall（全源最短路径）、Ford-Fulkerson（最大流）和匈牙利算法（最优分配），这些都是邓俊辉版没有覆盖或仅简要提及的重要算法。

## 核心概念（中文，附英文术语）

| 笔记 | 主题 | 核心算法 |
|------|------|----------|
| [[图算法基础CLRS]] | 图的表示与遍历 | BFS、DFS、拓扑排序、强连通分量 |
| [[最小生成树CLRS]] | 最小生成树 | Kruskal、Prim |
| [[单源最短路径CLRS]] | 单源最短路径 | Bellman-Ford、Dijkstra、差分约束 |
| [[全源最短路径]] | 全源最短路径 | 矩阵乘法法、Floyd-Warshall、Johnson |
| [[最大流]] | 最大流问题 | Ford-Fulkerson、Edmonds-Karp、最大二分匹配 |
| [[二分图匹配]] | 二分图匹配 | Hopcroft-Karp、稳定婚姻、匈牙利算法 |

## 各章概览

### 第20章 基本图算法（Elementary Graph Algorithms）
- **图表示**：邻接矩阵（Adjacency Matrix）vs 邻接链表（Adjacency List）
- **BFS**：广度优先搜索，O(V+E)，最短路径（无权图）
- **DFS**：深度优先搜索，O(V+E)，发现/完成时间戳
- **拓扑排序**（Topological Sort）：DAG 的线性排序
- **强连通分量**（SCC）：Kosaraju 算法，两次 DFS

### 第21章 最小生成树（Minimum Spanning Trees）
- **贪心策略**：安全边（Safe Edge）、切割（Cut）、轻边（Light Edge）
- **Kruskal 算法**：O(E log E)，使用并查集（Disjoint-Set）
- **Prim 算法**：O(E log V)（二叉堆）/ O(E + V log V)（斐波那契堆）

### 第22章 单源最短路径（Single-Source Shortest Paths）
- **松弛技术**（Relaxation）：所有最短路径算法的核心
- **Bellman-Ford**：O(VE)，处理负权边，检测负权环
- **DAG 最短路径**：O(V+E)，利用拓扑排序
- **Dijkstra**：O(E log V)（二叉堆）/ O(V log V + E)（斐波那契堆），要求非负权
- **差分约束**（Difference Constraints）：转化为最短路径问题

### 第23章 全源最短路径（All-Pairs Shortest Paths）
- **矩阵乘法法**：O(V³ log V)，重复平方法
- **Floyd-Warshall**：O(V³)，动态规划，处理负权边
- **Johnson 算法**：O(V² log V + VE)，适合稀疏图

### 第24章 最大流（Maximum Flow）
- **流网络**（Flow Network）：容量约束、流守恒
- **残存网络**（Residual Network）、增广路径（Augmenting Path）
- **最大流最小割定理**（Max-Flow Min-Cut Theorem）
- **Ford-Fulkerson 方法**：O(E·|f*|)，Edmonds-Karp 改进为 O(VE²)
- **最大二分匹配**：转化为最大流问题

### 第25章 二分图匹配（Matchings in Bipartite Graphs）
- **Hopcroft-Karp 算法**：O(√V·E)，最大匹配
- **稳定婚姻问题**（Stable Marriage）：Gale-Shapley 算法，O(n²)
- **匈牙利算法**（Hungarian Algorithm）：O(n⁴) / O(n³)，最大权完美匹配

## 关键要点

1. **BFS 与 DFS 是基石**：几乎所有图算法都建立在这两种遍历之上
2. **贪心与动态规划**：最小生成树用贪心，最短路径混合使用贪心（Dijkstra）和动态规划（Floyd-Warshall）
3. **负权边的影响**：Dijkstra 不能处理负权边；Bellman-Ford 可以但更慢；Floyd-Warshall 也可以
4. **最大流的多重应用**：最大流不仅解决流量问题，还能解决匹配、切割等组合优化问题
5. **CLRS 特有内容**：Bellman-Ford、Floyd-Warshall、Ford-Fulkerson、匈牙利算法是邓俊辉版未深入覆盖的

## 与其他概念的联系

- [[图算法基础CLRS]] → [[广度优先搜索BFS]] [[深度优先搜索DFS]] [[拓扑排序]]
- [[最小生成树CLRS]] → [[最小支撑树]] [[并查集]]
- [[单源最短路径CLRS]] → [[最短路径Dijkstra]] [[松弛操作]]
- [[全源最短路径]] → [[Floyd-Warshall]] [[动态规划基础]]
- [[最大流]] → [[流网络]] [[最大流最小割定理]]
- [[二分图匹配]] → [[匈牙利算法]] [[稳定婚姻问题]]

## 参考
- 《算法导论》第四版 第六部分（§20-25）
- 第20章 基本图算法（§20.1-20.5）
- 第21章 最小生成树（§21.1-21.2）
- 第22章 单源最短路径（§22.1-22.5）
- 第23章 全源最短路径（§23.1-23.3）
- 第24章 最大流（§24.1-24.3）
- 第25章 二分图匹配（§25.1-25.3）
