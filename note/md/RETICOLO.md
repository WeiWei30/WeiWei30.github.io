[toc]

# RETICOLO

## res1.m

**aa = res1(wavelength,period,textures,nn,k_parallel,parm)**

为每一层texture求解state variable本征值方程。texture不包括上下半无限层，只包含中间器件层，对每个中间器件层单独求解特征向量和特征值，得到线性组合形成的通解。

**输入**

- wavelength：工作波长。不限制单位，在程序中统一一种即可。

- period：周期。周期重复方向为x方向。

- texture：层结构定义。

  *example*

  ```matlab
  textures = cell(1, 2);  % 两层结构
  textures{1} = {1.5};  % 周期内折射率均为1.5
  textures{2} = {[-5, -3, 1, 6], [2, 1.3, 1.5, 3]}  % 第一个向量为空间坐标截断处，第二个向量为各截段的折射率。最后一个截段的折射率等于第一个截段的折射率
  ```

- nn：截取的谐波数。nn越大，结果越准确。

- k_parallel：入射波波矢(以真空中波矢归一化)

  $k_{\rm parallel} = n_{\rm inc}*\sin{\theta}=k^{\rm inc}_x/(2\pi/\lambda)$

  *注*：k_parallel不区分从top入射还是bottom入射。程序计算时，两种结果都会被计算。

- parm：定义偏振方向

  ` para = res0(-1)` TM模，电场沿x方向偏振

  `para = res0(1)` TE模，电场沿y方向偏振

## res2.m

**result = res2(aa, profile)**

计算各层、各级衍射波。接受`res1.m`的计算结果，根据==边界条件==确定各衍射级次权重量及其他未确定量。

**输入**

- aa：`res1.m`计算结果

- profile：定义各层堆叠效果，形成layerstack。

  *example*

  ```matlab
  profile = {[50, 50, 5, 20, 80, 50], [1, 3, 4, 5, 6, 2]};  % 定义各层的厚度(第一个向量)和排列方式(第二个向量)。排列方式按从上往下排列，第一层为top层，最后一层为bottom层
  ```

**输出**

`result.inc_top`, `result.inc_top_reflected`, `result.inc_top_transmitted`;

`result.inc_bottom`,`result.inc_bottom_reflected`,`result.inc_bottom_transmitted`.

## energy

Poynting vector

${\rm P} = {\rm E}\times{\rm H^*}$

${\rm Power} = \frac{1}{2} \int_{\rm Surface}{\rm Re(P)}\cdot {\rm ds}$

${\rm Normalized\ Power = \frac{Power}{Source\ Power}}$

## diffraction order $m$ v.s. diffraction angle $\theta_m$

$k_x^{\rm inc}+mk_x = \frac{2\pi}{\lambda}n_{\rm top/bottom}\sin{\theta_m}$

Efficiency -> far-field relative intensity

