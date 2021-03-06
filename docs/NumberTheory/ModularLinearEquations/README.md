<script type="text/javascript" src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.1/MathJax.js?config=TeX-AMS-MML_HTMLorMML"></script>

# Modular Linear Equations - 模线性方程组

--------

#### 问题

给定$$ n $$组除数$$ m_{i} $$和余数$$ r_{i} $$（$$ 0 \leq i \lt n $$），求一个非负整数$$ x $$满足：

$$
x \bmod m_{i} = r_{i}
$$

或者写作：

$$
\begin{cases}
x \bmod m_{0} = r_{0}  \\
x \bmod m_{1} = r_{1}  \\
x \bmod m_{2} = r_{2}  \\
\cdots              \\
x \bmod m_{n-1} = r_{n-1}
\end{cases}
$$

即求解模线性方程组。

#### 解法

将取模运算转化为乘法运算，存在$$ n $$组整数$$ k_{i} $$满足所有等式：

$$
\begin{cases}
x = k_{0} \times m_{0} + r_{0}  \\
x = k_{1} \times m_{1} + r_{1}  \\
x = k_{2} \times m_{2} + r_{2}  \\
\cdots              \\
x = k_{n-1} \times m_{n-1} + r_{n-1}
\end{cases}
$$

将前两行联立，可得：

$$
k_{0} \times m_{0} + r_{0} = k_{1} \times m_{1} + r_{1}
$$

变换等式可得：

$$
k_{0} \times m_{0} - k_{1} \times m_{1} = r_{1} - r_{0}
$$

上面等式中$$ k_{0}, k_{1} $$是求解$$ x $$的未知数，联想到Extended Euclid中的等式$$ a \times x + b \times y = gcd(a, b) $$，类似的对于任意两除数和余数都有：

$$ 
\begin{matrix}
x \bmod m_{i} = r_{i}      & \rightarrow & x = k_{i} \times m_{i} + r_{i}  \\
x \bmod m_{i+1} = r_{i+1}  & \rightarrow & x = k_{i+1} \times m_{i+1} + r_{i+1}
\end{matrix}
$$

通过Extended Euclid算法算出满足等式的$$ k_{i}, k_{i+1} $$，从而求出$$ x_{i} $$（注意$$ x_{i} $$只能满足第$$ i $$行和第$$ i + 1 $$行两行等式，但不一定满足其他行等式）。$$ n $$组除数和余数上可以求出$$ n - 1 $$个解：$$ [x_{0}, x_{1}, \dots, x_{n-2}] $$，最终的解为$$ x = lcm\{ x_{0}, x_{1}, \dots, x_{n-2} \} $$，显然这样的$$ x $$对所有除数和余数都满足$$ x \bmod m_{i} = r_{i} $$。

该算法的时间复杂度为$$ O((log_2 n) \cdot n) $$。

--------

#### 源码

[ModularLinearEquations.h](https://github.com/linrongbin16/Way-to-Algorithm/blob/master/src/NumberTheory/ModularLinearEquations.h)

[ModularLinearEquations.cpp](https://github.com/linrongbin16/Way-to-Algorithm/blob/master/src/NumberTheory/ModularLinearEquations.cpp)

#### 测试

[ModularLinearEquationsTest.cpp](https://github.com/linrongbin16/Way-to-Algorithm/blob/master/src/NumberTheory/ModularLinearEquationsTest.cpp)
