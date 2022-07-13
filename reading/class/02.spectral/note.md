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





background



model

