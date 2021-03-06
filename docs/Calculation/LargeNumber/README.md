<script type="text/javascript" src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.1/MathJax.js?config=TeX-AMS-MML_HTMLorMML"></script>

# LargeNumber - 大数字

--------

#### 问题

计算两个整数$$ a $$和$$ b $$的加减乘除，这些数字非常大到无法用内置的$$ int64 $$、$$ float64 $$存储。

#### 解法

将每个数字分为符号、整数区两个部分，模拟加减乘除的运算过程得到结果。设$$ a $$有$$ n_{a} $$位，$$ b $$有$$ n_{b} $$位。将$$ 0 $$视作与正数符号相同。

#### 取反

如果$$ a = 0 $$，$$ a $$的负值为它自己，如果$$ a \ne 0 $$，$$ a $$的负值为$$ -a $$。

#### 加法

加法$$ a + b $$有以下情况：

$$ (1) $$ 相同符号的$$ a, b $$相加可以把整数部分直接相加，符号与$$ a, b $$的符号相同；

$$ (2) $$ 不同符号的加法$$ a + b $$可以转化为$$ a + b = a - (-b) $$，比如$$ 12 + (-4) \rightarrow 12 - 4 $$，$$ (-1) + 8 \rightarrow (-1) - (-8) $$，然后交给减法器处理；

对于相同符号的加法$$ c = a + b $$，设$$ a[0], b[0] $$为数字的最低位（个位），用下标$$ i $$从最低位到最高位开始遍历$$ a, b $$的每一位（$$ i = 0 \rightarrow max(n_{a}, n_{b}) + 1 $$）。初始时设$$ c $$的每一位都为$$ 0 $$。则有：

$$

\begin{matrix}
c[i+1] = c[i+1] + ( c[i] + a[i] + b[i] ) \div 10    \\
c[i] = ( c[i] + a[i] + b[i] ) % 10
\end{matrix}

$$

下图演示$$ 12583 + 9127 = 21710 $$的过程：

![LargeNumber1.svg](../res/LargeNumber1.svg)

#### 减法

减法$$ a - b $$有以下情况：

$$ (1) $$ 两正整数相减$$ a - b $$且$$ 0 \leq b \leq a $$，可以把直接相减，符号为负；

$$ (2) $$ 符号不同减法$$ a - b $$可以转化$$ a - b = a + (-b) $$，比如$$ 12 - (-4) \rightarrow 12 + 4 $$，$$ -12 - 4 \rightarrow (-12) + (-4) $$，然后交给加法器处理；

$$ (3) $$ 两正整数相减$$ a - b $$且$$ 0 \leq a \lt b $$，可以转化为$$ a - b = -(b - a) $$，比如$$ 3 - 7 \rightarrow - (7 - 3) $$，$$ 12 - 37 \rightarrow -(37 - 12) $$；

$$ (4) $$ 两负整数相减$$ a - b $$且$$ a \lt b \lt 0 $$，可以转化为$$ a - b = -((-a) - (-b)) $$，比如$$ (-17) - (-9) \rightarrow -(17 - 9) $$，$$ (-82) - (-37) \rightarrow -(82 - 37) $$；

$$ (5) $$ 两负整数相减$$ a - b $$且$$ b \lt a \lt 0 $$，可以转化为$$ a - b = (-b) - (-a) $$，比如$$ (-9) - (-17) \rightarrow 9 - 17 $$，$$ (-37) - (-82) \rightarrow 82 - 37 $$；

对于两正整数$$ 0 \leq b \leq a $$的减法$$ c = a - b $$，设$$ a[0], b[0] $$为数字的最低位（个位），用下标$$ i $$从最低位到最高位开始遍历$$ a, b $$的每一位（$$ i = 0 \rightarrow max(n_{a}, n_{b}) + 1 $$）。初始时设$$ c $$的每一位都为$$ 0 $$。则有：

$$

c[i] =
\begin{cases}
c[i] + a[i] - b[i]                              &   a[i] \ge b[i] \\
c[i] + a[i] + 10 - b[i], a[i+1] = a[i+1] - 1    &   a[i] \lt b[i]
\end{cases}

$$

下图演示$$ 12583 - 9127 = 4456 $$的过程：

![LargeNumber2.svg](../res/LargeNumber2.svg)

#### 乘法

乘法$$ a \times b $$把整数部分直接相乘。若两数字符号相同其结果的符号为正，若两数字符号不同其结果的符号为负。

对于乘法$$ c = a \times b $$，设$$ a[0], b[0] $$为数字的最低位（个位），用下标$$ i, j $$从最低位到最高位开始分别遍历$$ a, b $$的每一位（$$ i, j = 0 \rightarrow max(n_{a}, n_{b}) + 1 $$）。$$ i, j $$的关系是两层循环，当$$ i = max(n_{a}, n_{b}) + 1 $$时$$ j $$加1。初始时设$$ c $$的每一位都为$$ 0 $$。则有：

$$

\begin{matrix}
c[j + i+1] = c[j + i+1] + ( c[j + i] + a[i] \times b[j] ) \div 10  \\
c[j + i] = ( c[j + i] + a[i] \times b[j] ) % 10
\end{matrix}

$$

下图演示$$ 12583 \times 9127 = 114845041 $$的过程：

![LargeNumber3.svg](../res/LargeNumber3.svg)

#### 除法

除法$$ a \div b $$有些麻烦，我们会在后面补上。

--------

#### 源码

[LargeNumber.h](https://github.com/linrongbin16/Way-to-Algorithm/blob/master/src/Calculation/LargeNumber.h)

[LargeNumber.h](https://github.com/linrongbin16/Way-to-Algorithm/blob/master/src/Calculation/LargeNumber.cpp)

#### 测试

[LargeNumberTest.h](https://github.com/linrongbin16/Way-to-Algorithm/blob/master/src/Calculation/LargeNumberTest.cpp)
