<script type="text/javascript" src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.1/MathJax.js?config=TeX-AMS-MML_HTMLorMML"></script>

# Nearest Neighbor - 最近点对

--------

#### 问题

求出二维平面坐标系上$$ n $$个点中最近的两点距离。

#### 解法

显然这个问题不能通过遍历每个点，再遍历计算它和其他所有点之间的距离的方法，这个方法的时间复杂度为$$ O(n) $$。

正确的方法是分治法对该问题求解。

将$$ n $$个点作为一个区域$$ s $$，按照$$ x $$坐标从小到大，$$ y $$坐标从小到大排序。可以得到该区域$$ x $$坐标范围为$$ [ x_{min}, x_{max} ] $$，$$ y $$坐标范围为$$ [ y_{min}, y_{max} ] $$。

在区域$$ s $$中选取$$ x $$坐标最接近$$ \frac{x_{min} + x_{max}}{2} $$的顶点$$ p $$，用垂直于$$ x $$轴，$$ x $$坐标为$$ x_{p} $$的直线将该区域划分为左右两个子区域$$ left $$和$$ right $$。顶点$$ p $$不属于$$ left $$或$$ right $$任意区域。对两个子区域，类似的继续进行划分，直到区域中顶点的数量$$ n \le 3 $$。

当一个区域中顶点数量$$ n \le 3 $$时，可以直接求出这三个点中的最近两点距离$$ dist_{min} $$，但我们无法确定左右两个子区域中的最近两点距离（毕竟我们并不想暴力的遍历两个子区域中的所有顶点）。

考虑左右区域中所有顶点的$$ x $$坐标，若某点$$ a $$的$$ x $$坐标与点$$ p $$的$$ x $$坐标之差$$ x_{ap} \ge dist_{min} $$（对$$ y $$坐标同样适用，即$$ a $$的$$ y $$坐标与点$$ p $$的$$ y $$坐标之差$$ y_{ap} \ge dist_{min} $$），则显然该点与$$ p $$不是最近点对。对于坐标差值小于左右子区域各自最近距离的点$$ a $$，算出点$$ a $$与点$$ p $$之间距离$$ dist_{ap} $$与左右子区域的最近距离进行比较，得到该父区域实际的最近距离。

//以它为基准设置一条垂直x轴的中线将当前区间划分为两个所含顶点数量一样的子区间
//若子区间包含的顶点数量大于3个 则继续递归的设置垂直线将子区间进行划分
//若子区间包含的顶点数量小于等于3个 则计算子区间中顶点之间的距离并找出最短距离
//考虑这样的情况相邻的左区间left与右区间right由中点p所在的垂直线划分成两部分
//通过上面递归的方法分别求出左区间和右区间中距离最近的两组点对
//比较这两个点对可以确定一对最近点对
//但无法确定是否存在这样一对点 其中一个属于左区间 另一个属于右区间
//它们之间的距离比上述已求出的最近点对更近
//因此考虑左右区间中所有点到中点p的x坐标
//若一个点与点p的x坐标或y坐标之差大于等于已求出的最近距离 则可以跳过该点
//因为两点的单x坐标或y坐标已经大于最近距离 则其实际距离必然大于等于最近距离
//若一个点与点p的x坐标和y坐标之差都小于已求出的最近距离
//则计算这两点的距离与已知最近距离比较 并进行更新

判断两线段$$ l_{1} $$和$$ l_{2} $$是否相交。

--------

#### 源码

[NearestNeighbor.h](https://github.com/linrongbin16/Way-to-Algorithm/blob/master/src/AnalyticGeometry/ConvexHull/NearestNeighbor.h)

[NearestNeighbor.cpp](https://github.com/linrongbin16/Way-to-Algorithm/blob/master/src/AnalyticGeometry/ConvexHull/NearestNeighbor.cpp)

#### 测试

[NearestNeighborTest.cpp](https://github.com/linrongbin16/Way-to-Algorithm/blob/master/src/AnalyticGeometry/ConvexHull/NearestNeighborTest.cpp)
