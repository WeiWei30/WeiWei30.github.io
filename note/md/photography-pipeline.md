# Photography Pipeline

<img src="img/photography-pipeline/image-20220506204200680.png" alt="image-20220506204200680"/>

## image sensor

![image-20220506204413163](img/photography-pipeline/image-20220506204413163.png)

成像传感器由微透镜阵列、颜色滤镜、光电二极管和势井组成。

- CCD型：电荷耦合元件，基于CMOS，高端相机采用
- CMOS型：互补金属氧化物半导体，基于MOSFET，便宜

Color filter array多采用Bayer排列，2*2 阵列中绿色占两个，蓝色和红色各一个。因为人对绿光更敏感。

![image-20220506210122949](img/photography-pipeline/image-20220506210122949.png)

## AFE

![image-20220506205837341](img/photography-pipeline/image-20220506205837341.png)

相机中的模拟前端主要由模拟放大器、模数转换器以及LUT(look-up table)组成，将势井产生的模拟信号转化成原始数字马赛克图像(raw digtial mosaiced image)。其中analog amplifier将模拟值进行增益gain的数值放大(ISO设置)，再经过ADC将模拟信号转换为数字信号(输出的值为10-16bits)，最后LUT可以在一定的范围内修正传感器响应的非线性，修复一些损坏的像素。

## ISP

![image-20220506210742183](img/photography-pipeline/image-20220506210742183.png)

ISP(image signal reocessor)系统接收的raw digtial mosaiced image转化为最后的RGB图像。包括一下几个步骤：

### white balance

白平衡的作用就是平衡RGB颜色的权重，而不是采用R、G、B各自归一化。自动白平衡需要选取一个标准来作为校准，根据标准不同而分为以下两类：(两者算法？标准化？归一化？)

- 灰世界假设：校准平均颜色为灰色
- 白世界假设：校准最亮颜色为白色

### demosaice

![image-20220506213211909](img/photography-pipeline/image-20220506213211909.png)

通过对color filter array中的RGB分别**插值**去马赛克。(哪些插值方法？)

### denoise

噪声来源：

- shot noise/poisson noise：光子到达传感器的数量是一个随机过程，符合泊松分布
- dark-shot noise：传感器发热导致逸出电子从而产生的噪声，温度越高，噪声越大
- Read noise：AFE读取产生的噪声

### tune reproduction

即色调重建，gamma校正：
$$
L'=L^\gamma
$$
$\gamma$通常取2.2。