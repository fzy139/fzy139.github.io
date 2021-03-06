#### 模拟问题

* 设计数据模型--考虑边界的设计（-1？）

#### 枚举
* 本质是 把问题用一定数据结构描述，然后遍历
* 构建搜索树 
* 慢的原因是DFS 结果产生在叶节点 大
* 普遍但低效
* 通过枚举去反应问题的内在机制

```
Zero Sum
```

#### 贪心
只选择局部最优，只考虑当前的最优选择，不考虑对后面的影响

如果整体最优解可通过局部最优得到，可以使用贪心

#### 求解过程 
先进行排序

枚举+贪心

枚举用来去除干扰因素（影响后续选择的决策）
不影响的用贪心来解决。
用其他方法来刨除干扰项。

```
灯泡问题

```




```

打字员安排问题`
```
枚举划分 t>= max(ti)
二分法枚举时间，贪心检测是否找出贪心解（）







# DFS
贪心算法效率更高，减去所有 \
1.不断构建一个解决方案（增加深度），逻辑比较顺畅\
2.深度确定\
\
**剪枝是优化主要手段** \
走到分支的尽头，不满足就回溯 \
设置一个标志存储分支，存储量比广度优先小。

BFS是把待搜索节点放到队列，一次\
\
使用递归编程\
对应栈

**优化**\
重复计算判定 使用结果集(备忘录法)

```
四皇后问题 
Sum it up
```

每个数取与不取 作差计算距离
* 相同数的处理,在处理右子数时加入相同判断，传入上一个数，判断是否
* 也可以写两个函数 处理左子树和右子树

```
genetic code
```
后面判断过的前面不用判断了 只用判断加入后

**如何选择？**\
1.看是否要求结果不能重复\
DFS不好处理 重复判断\
* 只要找到答案 用DFS（更快）
* 找最短路径 (对比所有结果 ) BFS
  
2.深度确定 \
或者使用迭代加深 即某曾没有答案时继续加深度\

3.规模小时
DFS需要很多剪枝才能优化 但是往往剪枝比较难(处理过的减掉 但是不好发现)\





* BFS 通过状态存储来优化，可通过状态压缩进行优化
* DFS 只记录当前路径

```
//先序遍历
{
    根节点压栈;
    while(栈不为空)
    {
        弹栈，访问该节点;
        右子数压栈;
        左子树压栈;
    }

}
```

# 动态规划
解决多阶段决策问题的优化方法。\
最优性原理，最优策略的一部分也是最优的。\
每阶段的的最优建立在前一阶段的最优解上。
具有无后效性(马尔科夫性)

最短路
```
mmin(sk+fk)
```
串联系统效果
```
max(sk*fk)
```

识别阶段！
几元组描述很关键！描述不好没有最优子结构
获取转移转移方程
临时值后面还会处理
动态规划很灵活
正向推进和逆向

1、最短路问题 

枚举法
```
{
    int MaxSubSum(int a[])
    for i:n
    {
        if b>0 
            b+=a[i]
        else
            b=a[i]   //如果以上个结尾的最大和小于0，那么加上前面肯定会变小，所以直接舍掉前面的

        if b>sum sum=b;
    }
    return sum
    
}
```

### 设计要点
1.问题的状态表示

```
插花问题
有编号1-v的花和同样数量的花瓶，
插花时 编号小的花必须放在左边
（使状态简单，不用考虑小花的最大值出现在大花当前花瓶之后）
且每个花放在不同的花瓶有不同的美学值
找出所有组合的最大值


```

```
dp[i][k]=max{ dp[i-1][k-1]+a[i][k] 
              dp[i][k-1] 
}
```

#### 多路径的问题
在进入下一阶段前需初始化上一阶段的状态
不允许跟本阶段有关，只能和上一阶段有关

发现题目的无后效性

* 先考虑解除所有约束，看怎么做，然后根据不同约束去解决

**不能脱离枚举的一个基本规律**

阶段递进，根据上次的结果

```
放单词的问题
单词美观问题
空格最少最美观
```
```
买票问题
委托买票

```

状态阶段->选择->递推方程

# 图
点V
边E
权W
表示 邻接矩阵 权值为矩阵
邻接表

## 最小生成树
构建一个包含图中所有节点的树，且权值最小

## PRIM（贪心枚举）
1.V中任选一个作为根节点
2.从已选取的节点V'中找一个权最小的添加顶点进V‘
3.更新表

× 有重复搜索，使用动态规划进行阶段选择
加入一个数组 记录V'某顶点到其他顶点的最小权值，并且不断更新这个表

每一个阶段对前一个阶段进行总结，

Kruscal 从边入手
开始顶点时离散的，未连接的，然后对边进行排序进而添加边
反复添加 放弃（构成回路时）

## 最短路
### Dj
解决两点间最小距离
针对非负权值
类比prim
prim是寻找v’中所有点到某顶点的最小距离

用邻接表也是可以的

###

### Bellman-Ford
解决负权边
类比kruscal
dk[j] 从原点经k条边到j的最短路径
也就是说 相比dj考虑了环形（因为走环可能会遇到负权减小）

对比dj 针对已知点（固定最小的点 因为都是正权 每次找最小肯定是）

计算量大，比dj复杂

收敛问题（无限刷下限）
N次和N-1次不同，说明有负环
遇到负环，要提前停止

```
### Floyed 
Flyed 计算任意两点间最短距离
输出一个矩阵


for k //遍历所有点
    for i   
        for j
           d[i][j] = min(d[i][j],d[i][k]+d[k][j])



```

### 欧拉回路

一笔画问题

tiaojian  wuxiang oushu
            chu dengyu ru



项链问题
```
珠子作为边
颜色作为点
解决欧拉回路
```
```
转盘问题
转盘上n个0 1



```
有向图的强连通分量

koerajue
dfs解决


### 二分图
图中的顶点输入两个集合
并且一个边联通的两个点属于不同的集合

最小顶点的覆盖数就是最大匹配问题


#### 匹配边的集合


## 计算几何

基本问题 位置和方向 
基本运算 叉乘和点乘

叉积应用
cross(a.b.c)== 

求多边形面积
简单多边形面积 任何不相邻的两个点叉积得到


# 凸包问题
对于点集或多边形 包含他们的最小凸多边形
Graham-Scan 试探性凸包

# 网络流
### 三个性质
容量限制
反对称性
流量平衡（流入流出）
满足的称为合法流

最大流问题
定义网络流量f

$\sum_{v}^{f(u,v)}$
### 链
顶点的一个排序
前向弧 方向与链一致
### 弧
流量f\
c容量
### 割
一个节点，删去它则讲图G分成两个不相连部分S和T，记为（S,T）


## 残量网络

最大流就是满足性质的情况下求f的最大值

## 标号法寻求可改进路

## 最大流


# 群论

## 置换
## 循环
# 裸题列表
poj1273 最大流
DFS poj1321 3984
BFS 3984 3287 
最小生成树 1258 prim/kruscal
最短路 1847 Floyed Dj 
贪心 1700 1017
