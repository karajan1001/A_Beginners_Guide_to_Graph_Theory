# 第二章 Walks, Paths and Cycles

## 2.1 Basic Ideas

- 游走(walk): 有限数量的顶点和边的序列,比如顶点$x_i$和边$a_i$ 组成的序列,其中边$a_i$的终点为点$x_i$
$$x_0 =(a_0)=> x_1 =(a_1)=> x_2 =(a_2)=> x_3 =(a_3)=> x_4 ... =(a_n)=> x_n  $$
这个游走叫 $x_0x_n-walk$ 其长度为游走经过的边数。

- 简单游走(simple walk): 没有重复边的游走。

- 路径(path): 没有重复顶点的游走。

- 封闭游走(closed walk): 又叫环(circuits)$x_0 = x_n $的$x_0x_n-walk$

##### 理论2.1 如果图G中有一个条游走可以从顶点y到顶点z。那么图中就有一条路径从y到z。

证明方法就是不断去掉环，因为游走有限，所以总会有一天，游走不包含重复顶点，得到一条路径。

- 相连(connected): 两个顶点之间有一条路径，则称他们相连。相连的顶点一定在图的同一个连通分量(component)中。

- 距离(distance): $D(x, y)$两个顶点之间最短的路径的长度。

##### 理论 2.2 一个二部图当且仅当它没有奇数长度的环时成立
证明，设有UV两个部分，沿着奇数长度环，一个点在U一个在V最后可以得到矛盾。
从x出发，距离为奇数的一部分，距离为偶数的一部分，如果某部分两点相连，则可以得出必定有奇数长度环。

- 树(tree): 无环图又叫树，多个无环图叫森林(forests)

## 2.2 Radius, Diameter and Eccentricity 
- 离心率(Eccentricity): $\epsilon(x) = Max(D(x,y))$某个点的离心率等于图中最大的距离。

- 半径(Radius): $D(G)$图中所有点中最小的离心率。

- 直径(Diameter): $R(G)$图中所有点中最小的离心率。

- 中心(center): $C(G)$图中所有$\epsilon(x) = R(G)$的点 $x$。

##### 理论 2.3. 任何图满足 $$R(G) \leq D(G) \leq 2R(G)$$

- 内周长(girth):$g(G)$是图中最小的环的长度。

- 外周长(circumference):$c(G)$是图中最大的环的长度。

##### 理论 2.4. 如果G是个有环图，则 $$g(G) \leq 2D(G) + 1$$

证明反证法: 如果有$g(G) > leq2D(G) + 2$ 则要么有更小的环，要么有更大的半径。

## 2.3 Weighted Distance

- 权重(weight): $w(x, y)$，权重不光可以赋予边也可以赋予顶点。

- 权重距离(weighted distance): $W(x, y)$, 权重和最小的路径。

##### 理论 2.5. 如果G是一个权重图，则其权重距离满足以下个性质
##### $$ W(x, y) = 0 当且仅当 x = y $$ 
##### $$ W(x, y) = W(y, x) $$
##### $$ W(x, y) + W(y, z) \geq W(x, z), 对所有顶点 x, y, z 成立 $$

- 最短路径(shortest path): 可以用Dijkstra的算法求得。

##### Dijkstra算法

问题： 求s到x的最短距离。
- s0 设为 s, 距离设为0
- s1 设为 s 的邻居中边权重最小的距离设为, s 到 s1 之间距离。
- sn 设为 与 s0,s1...sn-1直接连接的顶点的邻居中，到相应顶点si边权重加上到顶点si的距离最小的，其距离设为 si的举例加上sisn的边权重。
- 直到得到s,x停下。

反向计算时可以通过前一顶点的距离与到当前节点的变长反推出来。

## 2.4 Euler Walks

- 欧拉游走(Euler Walk): 一个可以正好不重复的走遍每条边的游走。

##### 理论 2.6. 如果一个连通图没有一个节点拥有奇数的度, 那么可以找到一个从任意点开始任意点结束的欧拉游走. 如果它有两个奇数度的节点，那么它有一条从一个奇数点开始另一个奇数点结束的欧拉游走。

证明：从任意节点A开始找一条回到A的简单游走。剩下图再找一条回到起点的简单游走，然后将这些游走拼合起来:
$$ABCDA + CEFGC = ABCEFGCDA $$。
有奇数节点则，先从奇数节点开始到奇数节点结束。

- 封闭欧拉游走(Closed Euler walk): 回到起点的欧拉游走。增加边使得图拥有封闭欧拉游走的方法叫欧拉化(Eulerization),需要增加的最小边数叫做欧拉化数(eu)。

## 2.5 哈密顿环

- 哈密顿环(Hamilton cycle): 一个经过所有顶点的环。包含这样的环的图叫做哈密顿的

- 哈密顿路径(Hamilton path): 一条经过所有顶点的路径

##### 定理2.7： 对于一个顶点大于3的图G，如果对任意不相连的顶点x,y，都有$d(x) + d(y) \geq v$ 则图G是哈密顿的。

证明：找到一个无哈密顿环最多条边的图，里面顶点pq不相连。则连接pq后图G+pq是哈密顿图，设哈密顿环为$p,x_1,x_2,x_3, ... x_v-2,q$。对于任意点$x_i$，只可能和p,q中一个相连否则$p,x_1,x_2...,x_{i-1}, q, x_{v-2} ... x_i$是一个哈密顿环。所以可以得到$d(p) + d(q) \leq v -1$

##### 推论2.8: 如果Ｇ是一个顶点大于３的图，而且每个顶点度大于等于$\frac v 2$则Ｇ是哈密顿的。

> 推论，一个哈密顿的图中度比k小的顶点数量不超过k，当k满足$1\leq k \leq \frac{v-1} 2$　时。

判断是否含有哈密顿环的一个可能方法是找到多组不相连的顶点，它们每个只能有两条边在哈密顿环中。如果最后剩余的边数少于顶点书数则不可能含有哈密顿环。

##### 定理2.9 一个二部图$G_{m,n}只有当$m=n$时才有哈密顿环，同理，只有当$m - n = 1或者-1$才有哈密顿路径

证明: $x_1,x_2,x_3...x_v$　可以分成两组$x_1,x_3,x_5,...x_v-1$,$x_2,x_4,x_6...x_v$只有两者相等才可能有哈密顿环。

## 2.6 旅行商人问题
> 旅行商人问题: (Traveling Sales Problem)寻找代价最少的哈密顿环的问题。
> 指数级计算复杂度。

> - 方法1 最近邻，任选一个点开始，然后不断寻找没有走过的点中最近的那个。

> - 方法2 排序边，先将边排序，然后选择不会导致任何一个顶点度超过2的最短的边。
