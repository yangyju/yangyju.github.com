---
layout: post
title: "shortest-path-within-lingo"
---
本文介绍了最短路问题，并给出了一个用lingo解决该问题的一个范例代码。
本文内容引自(http://www.smatrix.org)的一份文档.

最短路问题：
给定由$N$个点$p_i$组成的集合$\{p_i\}$,其中$i=1,2,3,...,N.$该集合中任一点$p_i$到另一点 $p_j$的距离用 $c_{ij}$表示.如果 $p_i$到$p_j$没有弧连接,则规定$c_{ij}=+\infty$,又规定$c_{ij}=0,1 \leq i \leq N$,指定终点为$p_N$.求从$p_i$出发到$p_N$的最短路.

这里采用动态规划的方法,即用$p_i$表示状态,决策集合是$p_i$以外的点,选定一个点$p_j$以后,得到效益$c_{ij}$并转入新状态$p_j$,当状态是$p_N$时,过程停止.这是一个不定期多阶段决策过程。

定义$f(i)$是由$p_i$点出发到终点$p_N$的最短路，由最优化原理可得
$$
\left\{ \begin{array}{ll}
f(i)=\min_{j}\{c_{ij}+f(j)\} & \textrm{$i=1,2,3,\cdots ,N-1$}\\
f(i)=0 & \textrm{$i=N$}
\end{array} \right.
$$
这是一个函数方程，用Lingo解决的代码例程：

!最短路问题;
```Lingo
model:
data:
n=10;
enddata
sets:
cities/1..n/: F; !10 个城市;
roads(cities,cities)/
1,2 1,3
2,4 2,5 2,6
3,4 3,5 3,6
4,7 4,8
5,7 5,8 5,9
6,8 6,9
7,10
8,10
9,10
/: D, P;
endsets
data:
D=
6 5
3 6 9
7 5 11
9 1
8 7 5
4 10
5
7
9;
enddata
F(n)=0;
@for(cities(i) | i #lt# n:
F(i)=@min(roads(i,j): D(i,j)+F(j));
);
!显然,如果 P(i,j)=1,则点 i 到点 n 的最短路径的第一步是 i --> j,否则就不是。
由此,我们就可方便的确定出最短路径;
@for(roads(i,j):
P(i,j)=@if(F(i) #eq# D(i,j)+F(j),1,0)
);
end
```
