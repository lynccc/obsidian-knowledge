---
tags: [数据结构, Python, Miller, DFS, 图]
aliases: [深度优先搜索Python, 骑士周游问题]
---

# 深度优先搜索 DFS（Python）

## 🗣️ 通俗讲解

> 想象走迷宫——你选择一条路一直往前走，走到死胡同再退回来试下一条路。DFS 就是这个策略：一条路走到黑，走不通再回溯。它用栈（或递归）来记住「退回到哪里」。

📖 **想看更深入的理论分析？** → [[深度优先搜索DFS]]（邓俊辉 C++ 版）

## 核心概念

DFS沿一条路径**尽可能深**地探索，遇到死路再**回溯**。使用**栈**（或递归调用栈）管理。

## 关键要点

### 骑士周游问题（Knight's Tour）

马从棋盘某格出发，按L形走法访问每个格子恰好一次。

**建图**：每个格子为顶点，马的合法走法为边。

```python
def knight_tour(n, path, u, limit):
    u.setColor('gray')
    path.append(u)
    if n < limit:
        nbr_list = list(u.get_connections())
        i = 0
        done = False
        while i < len(nbr_list) and not done:
            if nbr_list[i].getColor() == 'white':
                done = knight_tour(n + 1, path, nbr_list[i], limit)
            i += 1
        if not done:  # 回溯
            path.pop()
            u.setColor('white')
    else:
        done = True
    return done
```

### Warnsdorff 优化

优先访问**邻居数最少**的未访问顶点（贪心策略），大幅减少搜索空间：

```python
def order_by_avail(n):
    res_list = []
    for v in n.get_connections():
        if v.getColor() == 'white':
            c = 0
            for w in v.get_connections():
                if w.getColor() == 'white':
                    c += 1
            res_list.append((c, v))
    res_list.sort(key=lambda x: x[0])
    return [y[1] for y in res_list]
```

### 通用DFS实现

```python
def dfs(g):
    for aVertex in g:
        aVertex.setColor('white')
        aVertex.set_pred(-1)
    for aVertex in g:
        if aVertex.getColor() == 'white':
            dfsvisit(g, aVertex)

def dfsvisit(g, start_vertex):
    start_vertex.setColor('gray')
    for next_vertex in start_vertex.get_connections():
        if next_vertex.getColor() == 'white':
            next_vertex.set_pred(start_vertex)
            dfsvisit(g, next_vertex)
    start_vertex.setColor('black')
```

### DFS时间戳

每个顶点记录**发现时间**和**结束时间**，用于后续算法（拓扑排序、强连通分量）。

- 时间：O(V + E)
- 空间：O(V)（递归栈深度）

## 与其他概念的联系

- ← [[深度优先搜索DFS]]：邓俊辉版理论
- ← [[图的实现Python]]：基于Graph/Vertex类
- → [[拓扑排序Python]]：基于DFS完成时间
- → [[BFS-Python]]：对比——BFS找最短路径，DFS探索连通性

## 参考
- 《Python数据结构与算法分析》第2版 §7.5
