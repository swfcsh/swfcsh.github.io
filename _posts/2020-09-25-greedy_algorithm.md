---
layout: mypost
title: 贪心算法
categories: [教程]
extMath: false
---

##### 贪心算法（Greedy Algorithm) 简介
所谓贪心算法是指，在对问题求解时，总是做出在当前看来是最好的选择。也就是说，不从整体最优上加以考虑，它所做出的仅是在某种意义上的局部最优解。也就是说在每一步中，选择目前最优的策略，而不考虑全局是不是最优的。

##### 贪心算法的前提
1、 原问题复杂度过高
2、 求全局最优解的数学模型难以建立
3、 求全局最优解的计算量过大；
4、 没有太大必要一定要求出全局最优解，“比较优”就可以。

贪心算法没有固定的算法框架，算法设计的关键是贪心策略的选择。必须注意的是，贪心算法不是对所有问题都能得到整体最优解，选择的贪心策略必须具备无后效性，即某个状态以后的过程不会影响以前的状态，只与当前状态有关。所以对所采用的贪心策略一定要仔细分析其是否满足无后效性。


##### 例题1-用最少数量的箭引爆气球

有一些球形气球贴在一堵用 XY 平面表示的墙面上。墙面上的气球记录在整数数组 `points` ，其中`points[i] = [xstart, xend]` 表示水平直径在 `xstart` 和 `xend`之间的气球。你不知道气球的确切 y 坐标。

一支弓箭可以沿着 x 轴从不同点 完全垂直 地射出。在坐标 x 处射出一支箭，若有一个气球的直径的开始和结束坐标为 `xstart`，`xend`， 且满足  `xstart ≤ x ≤ xend`，则该气球会被 引爆 。可以射出的弓箭的数量 没有限制 。 弓箭一旦被射出之后，可以无限地前进。

给你一个数组 points ，返回引爆所有气球所必须射出的 最小 弓箭数 。

 
示例 1：
```
输入：points = [[10,16],[2,8],[1,6],[7,12]]
输出：2
解释：气球可以用2支箭来爆破:
-在x = 6处射出箭，击破气球[2,8]和[1,6]。
-在x = 11处发射箭，击破气球[10,16]和[7,12]。
```

示例 2：
```
输入：points = [[1,2],[3,4],[5,6],[7,8]]
输出：4
解释：每个气球需要射出一支箭，总共需要4支箭。
```

示例 3：
```
输入：points = [[1,2],[2,3],[3,4],[4,5]]
输出：2
解释：气球可以用2支箭来爆破:
- 在x = 2处发射箭，击破气球[1,2]和[2,3]。
- 在x = 4处射出箭，击破气球[3,4]和[4,5]。
 ```

```python
class Solution:
    def findMinArrowShots(self, points: List[List[int]]) -> int:
        points.sort(key=lambda x: x[1])
        arrows = 1
        mini = points[0][1]
        for i in range(1, len(points)):
            if not points[i][0] <= mini <= points[i][1]:
                mini = points[i][1]
                arrows += 1

        return arrows
```


##### 例题2-两地调度

公司计划面试 `2n` 人。给你一个数组 `costs` ，其中 `costs[i] = [aCosti, bCosti]` 。第 `i` 人飞往 `a` 市的费用为 `aCosti` ，飞往 `b` 市的费用为 `bCosti` 。

返回将每个人都飞到 `a` 、`b` 中某座城市的最低费用，要求每个城市都有 `n` 人抵达。

 

示例 1：
```
输入：costs = [[10,20],[30,200],[400,50],[30,20]]
输出：110
解释：
第一个人去 a 市，费用为 10。
第二个人去 a 市，费用为 30。
第三个人去 b 市，费用为 50。
第四个人去 b 市，费用为 20。

最低总费用为 10 + 30 + 50 + 20 = 110，每个城市都有一半的人在面试。
```

示例 2：
```
输入：costs = [[259,770],[448,54],[926,667],[184,139],[840,118],[577,469]]
输出：1859
```

示例 3：
```
输入：costs = [[515,563],[451,713],[537,709],[343,819],[855,779],[457,60],[650,359],[631,42]]
输出：3086
```

```python
class Solution:
    def twoCitySchedCost(self, costs: List[List[int]]) -> int:
        # If all the people travels to the cityA then total cost:
        totalA = 0
        for costA, _ in costs:
            totalA += costA

        # If all the people wish to travel to cityB instead of cityA then the difference in cost would be:
        difference = [costB - costA for costA, costB in costs]

        """
            Since in both the cities the number of people travelling should be equal and their total cost should be minimum,
            So if we move half of the people from cityA to cityB having minimum difference among all the people then the total cost would be the minimum.
        """
        # Total cost of people travelling to cityB instead of cityA having minimum difference:
        totalB = sum(sorted(difference)[:len(costs) // 2])

        # Total cost of travelling for both the cities
        return totalA + totalB

```
