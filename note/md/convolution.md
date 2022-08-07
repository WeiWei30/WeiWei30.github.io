# 傅里叶光的一些数学基础

[toc]

## 卷积的定义和计算

$$
C(u)=f(x)*g(x)=\int f(x)g(u-x)\ \text{d} x
$$

两种理解：

1. $g(x)$不作镜面对称处理

   
   $$
   C(u)=\sum_i f(i)g(u-i)
   $$
   $f(i)$倍的$g(u)$向右移动$i$个单位，最后全部累加起来。则**$C(u)$的值是两个函数关于$x=u/2$对称轴所有对称点函数值乘积的叠加。**

2. $g(x)$作镜面对称处理

   取$h(x)=g(-x)$，则卷积变互相关：
   $$
   C(u)=f(x)\star h(x)=\int f(x)h(x-u)\ \text{d}x
   $$
   可以看作$h(x)$不断在$f(x)$上滑动，向右滑动$+u$个单位后两者乘积的积分即$C(u)$的值。

## 卷积的交换律

$$
\begin{split}
C(u) & = f(x)*g(x) \\
& = \int_{-\infty}^{+\infty} f(x)g(u-x)\ \text{d}x\\
& \xlongequal{x'=u-x}-\int_{+\infty}^{-\infty} f(u-x')g(x')\ \text{d}x'\\
& = \int_{-\infty}^{+\infty}g(x')f(u-x')\ \text{d}x'\\
& =g(x)*f(x)
\end{split}
$$

(p.s. 积分上下限反号的同时，$\text{d}x'$也提供一个负号)

## 线性系统中的卷积

[ref](https://www.zhihu.com/question/22298352)

假设有一个线性空不变系统$L$，对$\delta(x-x_0,y-y_0)$冲激的响应为$h(x-x_0,y-y_0)$
$$
f(x_0,y_0)=\iint f(x,y)\delta(x-x_0,y-y_0)\ \text{d}x\text{d}y
$$
则：
$$
\begin{split}
f(x,y)&=\iint f(\alpha,\beta)\delta(\alpha-x,\beta-y)\ \text{d}\alpha\text{d}\beta\\
&=\iint f(\alpha,\beta)\delta(x-\alpha,y-\beta)\ \text{d}\alpha\text{d}\beta
\end{split}
$$
对于该信号，线性系统的输出为：
$$
\begin{split}
g(x,y)&=L[f(x,y)]=L\left[\iint f(\alpha,\beta)\delta(x-\alpha,y-\beta)\ \text{d}\alpha\text{d}\beta\right]\\
&=\iint f(\alpha,\beta)L[\delta(x-\alpha,y-\beta)]\ \text{d}\alpha\text{d}\beta\\
&=\iint f(\alpha,\beta)h(x-\alpha,y-\beta)\ \text{d}\alpha\text{d}\beta\\
&=f(x,y)*h(x,y)
\end{split}
$$
**对于这种某一时刻的输入与之后一段时间的输出都有关系的线性系统，可以用卷积来描述输入与输出的关系。**即某一信号的输出，等于该信号与脉冲函数输出信号的卷积。譬如成像系统，点光源输入时，会产生艾里斑，即某一个空间点的输入，能够影响相邻空间的输出，因此对一个物体成的像，就是该物体与点扩散函数的卷积。

因此，从上面的分析可知，若想要卷积有其物理意义，必须存在一个抽象的线性系统，且该线性系统存在某些平移不变量，且某维输入会影响该维度一个范围内的输出(当然这条不满足也行，譬如点扩散函数是仍是$\delta$函数时、或某时刻的输入只影响该时刻的输出)。

## 傅里叶变换

傅里叶变换：
$$
F(u)=\int_{-\infty}^{+\infty} f(x)e^{-i2\pi ux}\ \text{d}t
$$
逆傅里叶变换：
$$
f(x)=\int_{-\infty}^{+\infty}F(u)e^{i2\pi ux}\ \text{d}t
$$
### 帕塞瓦尔(Parseval)定理

Parseval定理公式为：
$$
<f(x),g(x)>=<F(f_x),G(f_x)>
$$
其中$F,G$为$f,g$的傅里叶变换。即频域空间的内积不变。

当$g=f$时：
$$
\|f(x)\|^2=\|F(f_x)\|^2
$$
表示空域总能量与频域总能量相等。

#### 傅里叶变换是幺正算符

若$G(f_x)=F[g(x)]$，那么：
$$
F^*[g(x)]=G^*(f_x)
$$
且：
$$
F^{-1}[g(x)]=G(-f_x)=G^*(f_x)
$$
因此，傅里叶变换操作是幺正算符。

#### 帕塞瓦尔定理证明

$$
\begin{split}
\int f(x)g(x)\ \text{d}x &= \int g(x)\int F(f_x)e^{j2\pi f_xx}\ \text{d}f_x\ \text{d}x\\
&=\int F(f_x)\int g(x)e^{j2\pi f_xx}\ \text{d}x\ \text{d}f_x\\
&=\int F(f_x) G(-f_x)\ \text{d}f_x\\
&=\int F(f_x)G^*(f_x)\ \text{d}f_x
\end{split}
$$



## 卷积定理证明

$$
\begin{split}
F[f_1(t)*f_2(t)]&=\int_{-\infty}^{+\infty}\left ( \int_{-\infty}^{+\infty}f_1(\tau)f_2(t-\tau)\ \text{d}\tau \right ) e^{-i\omega t}\ \text{d}t\\
& =\int_{-\infty}^{+\infty}f_1(\tau)\left ( \int_{-\infty}^{+\infty}f_2(t-
\tau)e^{-i\omega t}\ \text{d}t\right )\ \text{d}\tau\\
& =\int_{-\infty}^{+\infty}f_1(\tau)F_2(\omega)e^{-i\omega\tau}\ \text{d}\tau\\
& =F_2(\omega)\int_{-\infty}^{+\infty}f_1(\tau)e^{-i\omega\tau}\ \text{d}\tau\\
& = F_2(\omega)F_1(\omega)
\end{split}
$$

## 线性系统的本征值方程

假设时不变线性系统$L$的脉冲响应函数为$g(t)$，根据前面的推导，信号$f(t)$经过线性系统后的输出为$L[f(t)]=f(t)*g(t)$，当输入$f(t)=e^{i\omega t}$时：
$$
\begin{split}
L[f_\omega(t)]&=\int g(\tau)f_\omega(t-\tau)\ \text{d}\tau\\
&=\int g(\tau)e^{i\omega(t-\tau)}\ \text{d}\tau\\
&=e^{i\omega t}\int g(\tau)e^{-i\omega \tau}\ \text{d}\tau\\
&=\lambda_\omega f_\omega(t)
\end{split}
$$
即$\lambda_\omega$和$f_\omega(t)$分别是操作$L$的一组本征值和本征函数，即谐波经过时不变线性系统后波形不变，只是放大了$\lambda_\omega$倍，且$\lambda_\omega$是脉冲响应中频率为$\omega$的谐波的振幅。**从这里可以看出卷积定理在线性系统中的物理意义，即输出信号的频谱($F[L(f(t))]=F[f(t)*g(t)]$)等于输入信号频谱与脉冲函数频谱的乘积**。

## 采样：模拟到数字

### 采样定理

以空间采样为例，假设采样间隔是$\Delta x$，第$m$个采样点是$x_m=m\Delta x$，采样后的信号为：
$$
f_s(x)=f(x)\times\sum_{m=-\infty}^{+\infty}\delta(x-m\Delta x)
$$
采样信号的频谱为：
$$
\begin{split}
F'(u)&=F\left[f(x)\times\sum_{m=-\infty}^{+\infty}\delta(x-m\Delta x) \right]\\
&=F(u)*F\left[\sum_{m=-\infty}^{+\infty}\delta(x-m\Delta x) \right]\\
&=\frac{1}{\Delta x}F(u)* \sum_{m=-\infty}^{+\infty}\delta(u-\frac{m}{\Delta x})\\
&=\frac{1}{\Delta x}\sum_{m=-\infty}^{+\infty}F(u)* \delta(u-\frac{m}{\Delta x})\\
&=\frac{1}{\Delta x}\sum_{m=-\infty}^{+\infty}F\left(u-\frac{m}{\Delta x}\right)
\end{split}
$$
[注
$$
f(x)\times\delta(x-x_0)&=&f(x_0)\\
f(x)*\delta(x-x_0)&=&f(x-x_0)
$$
即==**采样信号的频谱为对原信号频谱平移($\cdots,-\frac{1}{\Delta x},0,\frac{1}{\Delta x},\cdots$)后的叠加**==，又频谱关于$u=0$对称，所以采样信号的频谱是周期函数，周期为$\frac{1}{2\Delta x}$。假设原信号的带宽为$u_0$，若频谱函数周期$\frac{1}{2\Delta x}<u_0$，那采样信号频谱的每个周期就会相互重叠，产生aliasing。因此：
$$
\frac{1}{\Delta x}>2u_0
$$
即奈奎斯特采样定理，保证采样的频率大于信号最大频率的两倍。

### sinc插值

由于采样后信号频谱的周期性，我们只取其中一个周期来对原始数据进行重建。故待重建的采样信号频谱为：
$$
F(u)=\text{rect}\left(\frac{u}{\Delta x^{-1}}\right)\times F'(u)
$$
其中$\text{rect}\left(\frac{u}{\Delta x^{-1}}\right)$为宽度为$\Delta u=\Delta x^{-1}$的矩形函数，来表示取中心那个周期。下面对$F(u)$进行重建，利用卷积定理：
$$
\begin{split}
f_r(x)&=F^{-1}[F(u)]=F^{-1}\left[\text{rect}\left(\frac{u}{\Delta x^{-1}}\right)\right]*f_s(x)\\
&=\frac{1}{\Delta x}\sum_{m=-\infty}^{+\infty}f(m\Delta x)\text{sinc}\left(\frac{x-m\Delta x}{\Delta x}\right)
\end{split}
$$
可以证明，经过sinc插值重建出来的信号与原始信号完全相同，即$f(x)=f_r(x)$。

