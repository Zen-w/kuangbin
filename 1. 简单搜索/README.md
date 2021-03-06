# 专题一、简单搜索

> 万物皆可搜 everything can be dfs/bfs...

## 深搜 dfs

多用于找到结果的种数，如 A-棋盘问题，写成回溯的形式比较直观；
注意需要剪枝，比如“当前情况用时”已经超过“当前最优用时”便可剪掉

### 优化

#### 记忆化搜索（类似于 DP）

#### 剪枝
TODO

## 广搜 bfs

通常用于找到“最短”之类的解，通常用“队列”来实现，且第一次找到的答案即为“最优答案”，因为此时向下搜索的“层数”最低嘛；
但因为需要存储的数据量指数增长（如果不剪枝的话），内存很容易爆掉...所以也需要大量剪枝，比如设 vis 数组或利用 STL 中 set 的 .count() 方法，判断当前的情况是否曾经出现过，若出现过则无需再推入队列。

### 考虑层数

可在节点 x 出队后，将其邻接点 x~i~ 入队时记录最后一个入队的节点 x~n~，当之后某时刻弹出的节点为 x~n~ 时，说明层数递增了

### 复杂度

* 邻接（链）表存储：O(N+E)   N 为每个节点，E 为每个节点所连接的共 2E 条边
* 邻接矩阵：O(N^2^)

### 优化

而对于数据量超大的情况，比如“八数码”类问题（如 HDU 1043、POJ 1077），直接 暴力广搜+STL 会超时或爆内存。所以，（以下参考 [八数码优化思想](http://www.cnblogs.com/goodness/archive/2010/05/04/1727141.html)，[八数码优化、附代码](https://www.cnblogs.com/zufezzt/p/5659276.html) 两篇文章，（文章内有笔误，注意））

* 对于超时问题，主要因为 STL 中 set 的查找仍旧耗时（logN），所以需要进行再度优化，比如改为通过哈希（Hash），仍用数组 vis 的 O(1) 复杂度来判断该情况是否曾出现过；

* 对于爆内存，一方面因为数据量太大，为了减少队列规模，可用“双向广搜”，即从开始和结果状态分别搜索，直接碰到相同的状态；另一方面，爆内存自然也与 STL 或数据结构的设计有关，优化方法比如：将起始状态到每个新状态的转换路径从存储状态的结构体中去掉，用结构体 { from, change } 数组来保存，即保存当前状态的上一状态 from 的下标，和转换到当前状态的改变量 change，最后输出结果时倒序输出即可。

* 如果需要再度优化，即使用“打表”，从“结果”出发，将所有可能到达的状态放入数组中，对于题目所给情况，直接查数组后输出结果，适用于多组测试的情况。

* 再再度优化，即使用 A*、简单估价函数、曼哈顿距离、堆优化、IDA* 等方法，我真的不会了...

### 流氓剪枝

对于深搜，可以在深度 deep 大于某一特定值时停止向下搜索；

对于广搜，可以 `if (rand() % 100 < 5)` 时不扩展当前状态，否则扩展