---
layout: mypost
title: 最大匹配问题-匈牙利算法
categories: [教程]
extMath: false
---

前不久在动态目标检测评测项目中用到了多目标匹配算法，其中需要涉及多个目标在两帧之间的最大匹配问题，其中就用到了匈牙利算法(Hungarian Algorithm)解决最大匹配问题，来找到两个集合内最多的匹配对。

匈牙利算法有多种实现方式，比如基于图论的方式等，本文主要讨论使用矩阵变换来实现的方法。

### 一个简单的例子

匈牙利算法的一个典型场景是任务分配。举个例子:

现在有三名工人张三，李四和王五以及三份工作扫地，浇花和擦窗户。每名工人做不同工作要求的工资是不同的, 如下表所示：

<table>
  <thead>
    <tr>
      <th style="text-align: center">&nbsp;</th>
      <th style="text-align: center">扫地</th>
      <th style="text-align: center">浇花</th>
      <th style="text-align: center">擦窗户</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align: center">张三</td>
      <td style="text-align: center">2</td>
      <td style="text-align: center">1</td>
      <td style="text-align: center">3</td>
    </tr>
    <tr>
      <td style="text-align: center">李四</td>
      <td style="text-align: center">3</td>
      <td style="text-align: center">3</td>
      <td style="text-align: center">4</td>
    </tr>
    <tr>
      <td style="text-align: center">王五</td>
      <td style="text-align: center">3</td>
      <td style="text-align: center">3</td>
      <td style="text-align: center">2</td>
    </tr>
  </tbody>
</table>

每名工人分配一份工作，问如何分配可以使得所付工资总和最少？

在上面这个例子中我们很容易观察出 `张三-浇花，李四-扫地，王五-擦窗户` 的成本最低。 但当工人数量和工作数量较大时， 寻找最优分配就变得不这么直观了。

### 匈牙利算法

我们发现这类分配问题可以用一个矩阵表示(称为效益矩阵)，记为`C`。
算法如下:

1. 效益矩阵初始化
   - 将矩阵`C`每行减去该行的最小元素, 得新矩阵`C'`；
   - 将矩阵`C'`每列减去该列的最小元素, 得新矩阵`C''`，以下操作对`C''`2进行；
2. 对当前效益矩阵求可行解
   - 从含零最少的行(或列)开始, 圈出矩阵中的一个 “0”, 并划去其所在的行和列；
   - 重复步骤 (2.1) 直至矩阵中所有的 “0” 均被划去或圈出为止；
   - 若已圈出`n`个 “0”, 它们即对应一最优解, 如不然转步骤3.
3. 求覆盖当前效益矩阵中所有 “0” 的最少条数直线
   - 对没有圈出 “0” 的行打`√`，对打`√`行上所有 “0” 所在的列打`√`，再对打`√`的列上所有有 “0” 被圈出的行打`√`，直至打不出`√`为止；
   - 将没有打`√`的行和打`√`的列划上直线，这些直线即为所求。
4. 调整效益矩阵
   - 找出没有被直线覆盖的所有元素中最小的数`c`；
   - 将打`√`的行上每个元素减去`c`，打`√`的列上每个元素加上`c`，得到新的效益矩阵。返回步骤2。

### 一个稍复杂的例子

TBA


