introduction

谱域图卷积

根据图谱理论和卷积定理，将数据由空域转换到谱域做处理。

问题1：如何对空间中的数据做卷积？

根据卷积定理，两信号在空域(时域)的卷积的傅里叶变换等于这两个信号在频域中的傅里叶变换的乘积
$$
\mathcal{F}[f_1(t)*f_2(t)]=F_1(w)·F_2(w)
$$
$\mathcal{F}$为傅里叶变换，$f(t)$为空域信号，$F(w)$为经过傅里叶变换后的频域信号

通过以下公式计算两个空域信号的卷积
$$
f_1(t)*f_2(t)=\mathcal{F}^{-1}[F_1(w)·F_2(w)]
$$
$f_1(t)$为空域输入信号，$f_2(t)$为空域卷积核，$\mathcal{F}^{-1}$为傅里叶反变换

问题2：如何定义图上的傅里叶变换？

傅里叶变换

decomposing frequencies from sound

a pure sound has certain beats per second. meaning if you measure the air pressure as a function of time, it would oscilate up and down, making 440 oscillations each second.

when two pure sound played at once, at any point in time, this pressure difference is the sum of what would be for each of those notes individually.

a microphone recording any sound just picks up on the air pressure at different time. it only see the final sum. can we decompose it into the pure frequencies that make it up?

the general strategy is to build a machine that treats signals with a given frequency differently from how it treat other signals.

we wrap the signal around a circle. the choice of winding frequency determines what the wound-up graph looks like.

we keep track of the center of mass for different winding frequency. the plot of the winding frequency vs. center of mass would only have a spike at the signal frequency. we can extract the signal frequency from this plot too. this machine is like a almost-Fourier transform.

if we take a random sound and throw it into this machine, it would have more then one spike. if you take two signals, and then apply this "almost Fourier transform" to each of them individually, and then add up the results, what you get is the same as if you first added up the signals, and then applied this "almost Fourier transform". so we can extract pure signals from it.

we think of the center of mess as a complex number. take a function describing a signal intensity vs. time, call it $g(t)$, if you multiply $g(t)$ by $e^{-2\pi ift}$, it can will represent the intensity vs. frequency. $g(t)e^{-2\pi ift}$ encapsulate the whole idea of winding a graph around a circle with a variable frequency $f$. 

now we need to track its center of mass. we sample N points from the signal. $mass = \frac{1}{N} \sum_{k=1}^{N} g(t_k)e^{-2\pi ift_k}=\frac{1}{t_2-t_1}\int_{t1}^{t2} g(t)e^{2e\pi ift}dt$

the actural fourier transform, means you scale the mess up by $t_2-t_1$
$$
\hat{g}(f)=\int_{t1}^{t2} g(t)e^{2e\pi ift}dt
$$
Laplacian Matrix
拉普拉斯矩阵=度矩阵-邻接矩阵

拉普拉斯矩阵是对称半正定矩阵

- n阶对称矩阵一定有n个线性无关的特征向量
- 对称矩阵的不同特征值对应的特征向量相互正交
- 实对称矩阵的特征向量一定是实向量
- 半正定矩阵的特征值一定非负

拉普拉斯矩阵的谱分解(特征分解)，将矩阵分解为特征值核特征向量表示的矩阵之积的方法
$$
L = U \Lambda U^{-1} = U
{\begin{bmatrix}
\lambda _1  &  & \\
  & \ddots  & \\
  &  & \lambda _n
\end{bmatrix}}
U^{-1} \\ 
U = (\vec{u_1}, \vec{u_2}, \cdots,\vec{u_n}) \\
\vec{u_i}\in \mathbb{R}^n, i=1,2,\cdots,n
$$
拉普拉斯矩阵的n个特征向量是线性无关且相互正交的，可以组成n维空间中的一组标准正交基。
$$
UU^T=I, L=U\Lambda U^{-1}=U\Lambda U^T
$$
拉普拉斯矩阵是图上的一种拉普拉斯算子

拉普拉斯算子$\bigtriangleup$定义为梯度gradient的散度divergence
$$
\bigtriangleup f = div(grad(f)) = \bigtriangledown \cdot (\bigtriangledown f)
$$
对于n维欧几里得空间，我们可以人为拉普拉斯算子是一个二阶微分算子。即在各个维度求二阶导数后求和。
$$
\bigtriangleup f = \sum_i \frac{\partial^2 f}{\partial x_i^2}
$$
在图上的拉普拉斯算子定义如下：
$$
\bigtriangleup f_i=\sum_{(i,j)\in\varepsilon}(f_i-f_j)
$$
其中$f=(f_1,f_2,\cdots,f_n)$，代表n个节点上每个节点的信号。

当边有权重时：
$$
\bigtriangleup f_i=\sum_{(i,j)\in\varepsilon}W_{ij}(f_i-f_j)=\sum_{j=1}^{n}W_{ij}(f_i-f_j)=D_{ii}f_i-\sum_{j=1}^nW_{ij}f_j
$$
对于n个节点有：
$$
\bigtriangleup f=g_\theta
=\begin{pmatrix} \bigtriangleup f_1\\ \vdots\\ \bigtriangleup f_n\\ \end{pmatrix}
=\begin{pmatrix}D_{11}f_1-\sum_{j=1}^nW_{1j}f_j\\\vdots\\D_{nn}f_n-\sum_{j=1}^nW_{nj}f_j\\ \end{pmatrix}
=\begin{pmatrix} D_{11}&&\\&\ddots&\\&&D_{nn} \end{pmatrix}f-Wf
=Df-Wf=Lf
$$
所以，拉普拉斯矩阵是图上的一种拉普拉斯算子

图傅里叶变换

傅里叶反变换的本质是把任意一个函数表示成若干正交基函数的线性组合

对于图上的节点信号 $x\in\mathbb R^n$，我们希望找到一组正交基，将其表达为这组正交基的线性组合

因此使用拉普拉斯矩阵的特征向量作为图傅里叶变换的基函数

使用拉普拉斯的特征向量作为基函数，则节点信号可以表示为：
$$
x=\hat{x}(\lambda_1)\vec{u_1}+\cdots+\hat{x}(\lambda_n)\vec{u_n}=U\hat x
$$
傅里叶变换与图傅里叶变换对比

|      |                     经典傅里叶变换                     |                 图傅里叶变换                  |
| :--: | :----------------------------------------------------: | :-------------------------------------------: |
| 公式 | $\hat x(w)=\sum_{k=1}^{n} x(k)e^{-\frac{2\pi}{n} iwk}$ | $\hat x(\lambda_l)=\sum_{k=1}^n x(k){u_l}(k)$ |
|  基  |               $e^{-\frac{2\pi}{n} iwk}$                |                  ${u_l}(k)$                   |
| 频率 |                          $w$                           |                  $\lambda_l$                  |
| 振幅 |                      $\hat x(w)$                       |              $\hat x(\lambda_l)$              |

经典傅里叶变换的基函数是拉普拉斯算子的本征函数(eigenfunction)，而拉普拉斯矩阵就是图上的拉普拉斯算子，所以图傅里叶变换的基函数即为图拉普拉斯矩阵的特征向量(eigenvector)。

特征基向量的性质

- 拉普拉斯矩阵的特征值担任了和频率类似的位置
- 拉普拉斯矩阵的特征向量担任了基函数的位置，特征值小的特征向量比较平滑，特征值大的特征向量变化比较剧烈，对应于低频基函数和高频基函数。

总结

依靠图傅里叶变换，可以将图上的节点信号$x$，从空间域转换到频域。

图卷积定义：
$$
x*_Gg=U(U^Tx\odot U^Tg)
$$
作为卷积核的$g$，我们不关心其在空间域上的表示，只关心其频率域上的表示，令$g_\theta=diag(U^Tg)$，
$$
x*_Gg_\theta=U(U^Tx\odot U^Tg)=Ug_\theta U^Tx
$$




model



SCNN
$$
x_{k+1,j}=h(U\sum_{i=1}^{C}F_{j,i}U^Tx_{k,i})
$$
其中，j表示卷积核，i表示输入channel，k表示层，h为激活函数。



ChebNet

解决计算复杂度大的问题，采用Chebyshev多项式代替谱域的卷积核



GCN

仅考虑一阶chebyshev多项式，每个卷积核只有一个参数





















