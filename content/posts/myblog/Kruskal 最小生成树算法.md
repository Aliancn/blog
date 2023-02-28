---

title: "Kruskal"
summary: "Kruskal算法的证明和实现"
date: 2023-01-15
weight: 
tags: ["Kruskal"]
author: "CHuSeng"
draft: false
isCJKLanguage: true
---

# Kruskal 最小生成树算法

### 生成树与最小生成树

树与图的差别在于，树不包含环，而图可以包含环

生成树就是指在图中找一棵白喊所有节点的树，即是包含所有节点的**无环连通子图**

对于加权图而言，最小生成树就是在所有生成树中，**权重和最小**的那棵生成树



### Kruskal算法

### 步骤

1. 将所有的边按升序排列

2. 从权值最小的边开始，如果这条边连接的两个节点不在同一连通分量，则

   将这条边添加到树中，并使两点处于同意连通分量

3. 重复3，直至图中的所有节点都在树上，即同一连通分量中

### 证明

1. 以上步骤保证连接的点处于不同连通分量，不存在环，因此构成的是树

2. 在步骤三中，每条边在选取的当时，都是连接两个不同的连通分量的权值最小的边

3. 要证明这条边属于最小生成树，用反证法：如果这条边A不在最小生成树上，但是两

   边的连通分量一定要连接，那么存在另一种连法，另一种连法中的边B和边A可以形成

   环，而B一定是比A大的，所以将B用A替换掉，图依旧保持连通，但是总权值变小了。

   也就是说，选这条边的总权值是最小的。

4. 如果最终不能将所有点归于同一连通分量，则没有生成树

> 以上证明参考[wiki](https://zh.wikipedia.org/zh-hans/%E5%85%8B%E9%B2%81%E6%96%AF%E5%85%8B%E5%B0%94%E6%BC%94%E7%AE%97%E6%B3%95#%E8%AF%81%E6%98%8E)

### 伪码

```
KRUSKAL-FUNCTION(G, w)
1    F := 空集合
2    for each 图 G 中的顶点 v
3        do 将 v 加入森林 F
4    所有的边(u, v) ∈ E依权重 w 递增排序
5    for each 边(u, v) ∈ E
6        do if u 和 v 不在同一棵子树
7            then F := F ∪ {(u, v)}
8                将 u 和 v 所在的子树合并
```

### c++实现

```c++
#include <bits/stdc++.h>

struct DSU {
    std::vector<int> fa, sz;
    DSU(int n = 0) : fa(n), sz(n, 1) {
        std::iota(fa.begin(), fa.end(), 0);
    }
    int Find(int x) { // 路径压缩
        while (x != fa[x])
            x = fa[x] = fa[fa[x]];
        return x;
    }
    bool Merge(int x, int y) { // 按秩合并
        x = Find(x), y = Find(y);
        if (x == y) return false; // 处于同一连通分量
        if (sz[x] > sz[y]) std::swap(x, y);
        fa[x] = y;
        sz[y] += sz[x];
        return true;
    }
}; // 并查集

int main() {
    int n, m; // 点数，边数
    std::cin >> n >> m;
    std::vector<std::tuple<int, int, int>> edge(m);
    // 边集，三元组分别表示边权和边的两个端点
    for (auto &[w, u, v] : edge)
        std::cin >> u >> v >> w;
    std::sort(edge.begin(), edge.end()); // 按边权升序排序
    DSU dsu(n); // 初始化并查集
    long long result = 0; // 最小生成树边权和
    for (auto &[w, u, v] : edge)
        if (dsu.Merge(u, v)) result += w;
        // 合并两个连通分量并统计答案
    std::cout << result << std::endl;
    return 0;
}
```

