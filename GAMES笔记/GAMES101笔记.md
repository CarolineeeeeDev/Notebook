# Games101

[TOC]

## 一、Review of Linear Algebra 线性代数

### 向量

单位向量：长度为一的向量

操作：向量求和--平行四边形法则，三角形法则 

![image-20240525163044249](C:\Users\LilSc\AppData\Roaming\Typora\typora-user-images\image-20240525163044249.png)

#### 向量点乘：==判断同向反向、接近程度==

![image-20240525163147555](C:\Users\LilSc\AppData\Roaming\Typora\typora-user-images\image-20240525163147555.png)

#### 点乘基本属性

![image-20240525163358612](C:\Users\LilSc\AppData\Roaming\Typora\typora-user-images\image-20240525163358612.png)

#### 点乘坐标系运算

![image-20240525163456150](C:\Users\LilSc\AppData\Roaming\Typora\typora-user-images\image-20240525163456150.png)

#### 向量投影

![image-20240525164037556](C:\Users\LilSc\AppData\Roaming\Typora\typora-user-images\image-20240525164037556.png)

#### 向量叉乘：==判定左右、判定内外==

![image-20240525164828987](C:\Users\LilSc\AppData\Roaming\Typora\typora-user-images\image-20240525164828987.png)

#### 叉乘基本属性（右手坐标系）：不满足交换律

![image-20240525164920751](C:\Users\LilSc\AppData\Roaming\Typora\typora-user-images\image-20240525164920751.png)

#### 叉乘坐标系运算

![image-20240525165143590](C:\Users\LilSc\AppData\Roaming\Typora\typora-user-images\image-20240525165143590.png)

叉乘结果是正的说明后项向量在前项向量的左侧，叉乘结果是正的说明后项向量在前项向量的右侧；

由此可以得到点在图形内还是在图形外

右手三维直角坐标系

![image-20240525170811243](C:\Users\LilSc\AppData\Roaming\Typora\typora-user-images\image-20240525170811243.png)

### 矩阵

#### 矩阵乘积 

乘积的i行j列元素 = i行向量**点乘**j行向量

#### 矩阵乘积属性：不满足交换律

![image-20240525171839648](C:\Users\LilSc\AppData\Roaming\Typora\typora-user-images\image-20240525171839648.png)

#### 矩阵的逆

![image-20240525211352122](C:\Users\LilSc\AppData\Roaming\Typora\typora-user-images\image-20240525211352122.png)

向量的点乘和叉乘写成矩阵相乘的形式：

![image-20240525212435103](C:\Users\LilSc\AppData\Roaming\Typora\typora-user-images\image-20240525212435103.png)

A*：伴随矩阵



## 二、Transformation 变换

### 1. 模型变换 Modeling Transformation

#### 缩放矩阵

![image-20240525214623109](C:\Users\LilSc\AppData\Roaming\Typora\typora-user-images\image-20240525214623109.png)

#### 镜像矩阵

![image-20240525214701148](C:\Users\LilSc\AppData\Roaming\Typora\typora-user-images\image-20240525214701148.png)

#### 切变矩阵

![image-20240525214730640](C:\Users\LilSc\AppData\Roaming\Typora\typora-user-images\image-20240525214730640.png)

![image-20240525214722999](C:\Users\LilSc\AppData\Roaming\Typora\typora-user-images\image-20240525214722999.png)

#### 旋转矩阵

![image-20240525215209689](C:\Users\LilSc\AppData\Roaming\Typora\typora-user-images\image-20240525215209689.png)

θ为逆时针旋转的角度

线性变换：一个向量 = ==一个矩阵== * 另一个向量

#### 齐次坐标变换

引入齐次坐标的理由是平移变换

![image-20240525220021671](C:\Users\LilSc\AppData\Roaming\Typora\typora-user-images\image-20240525220021671.png)

引入齐次变换后：

![image-20240525220414795](C:\Users\LilSc\AppData\Roaming\Typora\typora-user-images\image-20240525220414795.png)

#### 平移变换

![image-20240525220447289](C:\Users\LilSc\AppData\Roaming\Typora\typora-user-images\image-20240525220447289.png)

向量具有平移不变性

 ![image-20240525220953294](C:\Users\LilSc\AppData\Roaming\Typora\typora-user-images\image-20240525220953294.png)

点+点 = 这两个点的中点

#### 仿射变换

（ = 先应用前述 线性变换，再应用平移变换）

![image-20240525221156933](C:\Users\LilSc\AppData\Roaming\Typora\typora-user-images\image-20240525221156933.png)

#### 引入齐次坐标后的二维线性变换

![image-20240525221355006](C:\Users\LilSc\AppData\Roaming\Typora\typora-user-images\image-20240525221355006.png)

逆变换矩阵的效果就是将原来的变换还原：M ➡ M^-1^

向量会==从右向左==逐个运用变换矩阵

三维空间引入齐次变换：

![image-20240525222821468](C:\Users\LilSc\AppData\Roaming\Typora\typora-user-images\image-20240525222821468.png)

#### 三维变换矩阵

（先线性变换，再平移）

![image-20240525223027030](C:\Users\LilSc\AppData\Roaming\Typora\typora-user-images\image-20240525223027030.png) 

正交矩阵：矩阵的逆等于它的转置（例如旋转矩阵）

![image-20240525224143273](C:\Users\LilSc\AppData\Roaming\Typora\typora-user-images\image-20240525224143273.png)

#### 三维旋转矩阵

![image-20240525224207536](C:\Users\LilSc\AppData\Roaming\Typora\typora-user-images\image-20240525224207536.png)

罗德里格斯旋转公式：绕任意过原点的轴旋转任意角度

绕任意轴：把旋转中心点平移到原点再进行操作，最后把所有东西再移回去

![image-20240526115941891](C:\Users\LilSc\AppData\Roaming\Typora\typora-user-images\image-20240526115941891.png)

![image-20240526120643615](C:\Users\LilSc\AppData\Roaming\Typora\typora-user-images\image-20240526120643615.png)

四元数的引入：旋转与旋转之间的插值

### 2. 视图变换 Viewing Transformation

视图变换：改变相机位置、方向

#### 初始相机定义

![image-20240526122454355](C:\Users\LilSc\AppData\Roaming\Typora\typora-user-images\image-20240526122454355.png)

#### 相机标准位置

![image-20240526122853628](C:\Users\LilSc\AppData\Roaming\Typora\typora-user-images\image-20240526122853628.png)

#### 相机旋转矩阵

![image-20240526123402740](C:\Users\LilSc\AppData\Roaming\Typora\typora-user-images\image-20240526123402740.png)

模型要和相机一起变换

### 3. 投影变换 Projection Transformation

3D到2D

![image-20240526125236787](C:\Users\LilSc\AppData\Roaming\Typora\typora-user-images\image-20240526125236787.png)

#### 正交投影 Orthographic Projection

映射到标准立方体：先把中心点平移到原点，再缩放

![image-20240526125617410](C:\Users\LilSc\AppData\Roaming\Typora\typora-user-images\image-20240526125617410.png)

![image-20240526130050798](C:\Users\LilSc\AppData\Roaming\Typora\typora-user-images\image-20240526130050798.png)

#### 透视投影 Perspective Projection

映射到立方体的变换矩阵：

![image-20240526133813949](C:\Users\LilSc\AppData\Roaming\Typora\typora-user-images\image-20240526133813949.png)

## 三、Rasterization 光栅化 

定义视锥的长宽比（Aspect ratio）和可视角度（fovY）

![image-20240526161143876](C:\Users\LilSc\AppData\Roaming\Typora\typora-user-images\image-20240526161143876.png)

![image-20240526161358648](C:\Users\LilSc\AppData\Roaming\Typora\typora-user-images\image-20240526161358648.png)

光栅化 = 绘制到屏幕上

像素：一个像素是一个有着均匀颜色的小方块，是RGB的混合

像素的坐标：

![image-20240526162516167](C:\Users\LilSc\AppData\Roaming\Typora\typora-user-images\image-20240526162516167.png)

视口变换矩阵：

![image-20240526162635441](C:\Users\LilSc\AppData\Roaming\Typora\typora-user-images\image-20240526162635441.png)

三角形得到广泛应用的原因：三角形是最基础的多边形；任何多边形都能拆成三角形；三角形内部一定是平面的；三角形内外定义是清晰的

### 采样

给一个三角形，判断像素中心在不在三角形内：

![image-20240526164959012](C:\Users\LilSc\AppData\Roaming\Typora\typora-user-images\image-20240526164959012.png)

### 光栅化

![image-20240526165253140](C:\Users\LilSc\AppData\Roaming\Typora\typora-user-images\image-20240526165253140.png)

### AABB包围盒

![image-20240526165815393](C:\Users\LilSc\AppData\Roaming\Typora\typora-user-images\image-20240526165815393.png)

### 走样

 走样：锯齿、摩尔纹、车轮效应

走样原因：信号变化太快，采样太慢

### 反走样

在采样之前先做模糊

### 傅里叶级数展开

![image-20240526174006081](C:\Users\LilSc\AppData\Roaming\Typora\typora-user-images\image-20240526174006081.png)

![image-20240526174022476](C:\Users\LilSc\AppData\Roaming\Typora\typora-user-images\image-20240526174022476.png)

采样频率如果太慢，就会产生走样

### 傅里叶变换

可以把某个函数/图像从时域Spatial Domain变到频域Frequency Domain（频谱）

低频多，高频少：

![image-20240526211715322](C:\Users\LilSc\AppData\Roaming\Typora\typora-user-images\image-20240526211715322.png)

滤波：把某个特定的频段去掉。

下图为高通滤波，只有高频信号可以通过。

![image-20240526212013781](C:\Users\LilSc\AppData\Roaming\Typora\typora-user-images\image-20240526212013781.png)

下图为低通滤波，只有低频信号可以通过。

![image-20240526212247555](C:\Users\LilSc\AppData\Roaming\Typora\typora-user-images\image-20240526212247555.png)

带通滤波

![image-20240526212453386](C:\Users\LilSc\AppData\Roaming\Typora\typora-user-images\image-20240526212453386.png)

滤波 = 平均 = 卷积

卷积示例：

![image-20240526212907587](C:\Users\LilSc\AppData\Roaming\Typora\typora-user-images\image-20240526212907587.png)

时域上的卷积相当于频域上的乘积，时域上的乘积相当于频域上的卷积

每个像素取周围3*3的盒子（box filter）做点乘操作：模糊

![image-20240526213456238](C:\Users\LilSc\AppData\Roaming\Typora\typora-user-images\image-20240526213456238.png)

如果盒子在时域上变大，那么对应在频域上会变小

时域上：采样 = 原始信号 * 冲击函数

在频域上：采样就是在重复原始信号的频谱

![image-20240526215752914](C:\Users\LilSc\AppData\Roaming\Typora\typora-user-images\image-20240526215752914.png)

产生走样的原因：

采样的间隔会影响频谱的复制粘贴间隔，采样的不够快就会导致复制粘贴原频谱的间隔小 （混叠）

![image-20240526220424668](C:\Users\LilSc\AppData\Roaming\Typora\typora-user-images\image-20240526220424668.png)

改善走样造成的问题的方法：增加采样频率（但是需要高分辨率）；反走样：

==先拿掉高频信号（模糊），再采样==

![image-20240526221239133](C:\Users\LilSc\AppData\Roaming\Typora\typora-user-images\image-20240526221239133.png)

对于一个三角形：对每个覆盖到的像素求平均

![image-20240526221856984](C:\Users\LilSc\AppData\Roaming\Typora\typora-user-images\image-20240526221856984.png)

### MSAA：用更多采样点进行反走样

把一个像素分为多个采样点，近似一个合理的覆盖率

![image-20240526222348031](C:\Users\LilSc\AppData\Roaming\Typora\typora-user-images\image-20240526222348031.png)

![image-20240526222408481](C:\Users\LilSc\AppData\Roaming\Typora\typora-user-images\image-20240526222408481.png)

通过MSAA可以得到抗锯齿效果，但是增大了计算量，不过很多样本得到了复用，计算量不会增加那么大

其它抗锯齿方法：

==FXAA== 快速近似抗锯齿：图像的后期处理；

 ==TAA== 时间性抗锯齿：复用上一帧每个像素的值继续产生作用；

==TXAA==：TAA+MSAA

超分辨率 Super resolution：

从低分辨率到高分辨率的优化方法

常用方法：==DLSS== 深度学习



## 四、 Shading 着色

Z-Buffer 深度缓存

对每个像素/采样点记录最浅深度（离我们最近的距离）为浮点型

时间复杂度为O(n)，和顺序无关

> 顺序：MVP变换，Viewport，Rasterization，Shading

着色：对不同物体应用不同材质的过程

### 布林冯模型  Blinn-Phong反射模型

最基础的着色模型

高光、漫反射、环境光

shading point

n：法线向量

v：观测方向

l：光照方向

表面属性：颜色、亮度（shininess）

shading不考虑其它物体的存在，也不考虑阴影，只考虑每个点自己，有局部性（local）

#### 漫反射 Diffuse Reflection

任一shading point周围单位面积接收到的能量和光照方向与法线方向之间的夹角的余弦成正比

cosΘ = l · n （l和n都为单位向量）

球壳离光源距离为1时，定义光强为I；则球壳离光源距离为r时，定义光强为I/r^2^（球壳面积*光强守恒）

==漫反射公式==

到达的能量➡接收的能量

点有颜色的原因：它吸收了一部分能量，反射出去的是没吸收的能量

漫反射与v完全没关系，从各个地方看到的都是一样的