# Games101

[TOC]

## 一、Review of Linear Algebra 线性代数

### 向量

单位向量：长度为一的向量

操作：向量求和--平行四边形法则，三角形法则 

![image-20240525163044249](images\image-20240525163044249.png)

#### 向量点乘：==判断同向反向、接近程度==

![image-20240525163147555](images\image-20240525163147555.png)

#### 点乘基本属性

![image-20240525163358612](images\image-20240525163358612.png)

#### 点乘坐标系运算

![image-20240525163456150](images\image-20240525163456150.png)

#### 向量投影

![image-20240525164037556](images\image-20240525164037556.png)

#### 向量叉乘：==判定左右、判定内外==

![image-20240525164828987](images\image-20240525164828987.png)

#### 叉乘基本属性（右手坐标系）：不满足交换律

![image-20240525164920751](images\image-20240525164920751.png)

#### 叉乘坐标系运算

![image-20240525165143590](images\image-20240525165143590.png)

叉乘结果是正的说明后项向量在前项向量的左侧，叉乘结果是正的说明后项向量在前项向量的右侧；

由此可以得到点在图形内还是在图形外

右手三维直角坐标系

![image-20240525170811243](images\image-20240525170811243.png)

### 矩阵

#### 矩阵乘积 

乘积的i行j列元素 = i行向量**点乘**j行向量

#### 矩阵乘积属性：不满足交换律

![image-20240525171839648](images\image-20240525171839648.png)

#### 矩阵的逆

![image-20240525211352122](images\image-20240525211352122.png)

向量的点乘和叉乘写成矩阵相乘的形式：

![image-20240525212435103](images\image-20240525212435103.png)

A*：伴随矩阵



## 二、Transformation 变换

### 1. 模型变换 Modeling Transformation

#### 缩放矩阵

![image-20240525214623109](images\image-20240525214623109.png)

#### 镜像矩阵

![image-20240525214701148](images\image-20240525214701148.png)

#### 切变矩阵

![image-20240525214730640](images\image-20240525214730640.png)

![image-20240525214722999](images\image-20240525214722999.png)

#### 旋转矩阵

![image-20240525215209689](images\image-20240525215209689.png)

θ为逆时针旋转的角度

线性变换：一个向量 = ==一个矩阵== * 另一个向量

#### 齐次坐标变换

引入齐次坐标的理由是平移变换

![image-20240525220021671](images\image-20240525220021671.png)

引入齐次变换后：

![image-20240525220414795](images\image-20240525220414795.png)

#### 平移变换

![image-20240525220447289](images\image-20240525220447289.png)

向量具有平移不变性

 ![image-20240525220953294](images\image-20240525220953294.png)

点+点 = 这两个点的中点

#### 仿射变换

（ = 先应用前述 线性变换，再应用平移变换）

![image-20240525221156933](images\image-20240525221156933.png)

#### 引入齐次坐标后的二维线性变换

![image-20240525221355006](images\image-20240525221355006.png)

逆变换矩阵的效果就是将原来的变换还原：M ➡ M^-1^

向量会==从右向左==逐个运用变换矩阵

三维空间引入齐次变换：

![image-20240525222821468](images\image-20240525222821468.png)

#### 三维变换矩阵

（先线性变换，再平移）

![image-20240525223027030](images\image-20240525223027030.png) 

正交矩阵：矩阵的逆等于它的转置（例如旋转矩阵）

![image-20240525224143273](images\image-20240525224143273.png)

#### 三维旋转矩阵

![image-20240525224207536](images\image-20240525224207536.png)

罗德里格斯旋转公式：绕任意过原点的轴旋转任意角度

绕任意轴：把旋转中心点平移到原点再进行操作，最后把所有东西再移回去

![image-20240526115941891](images\image-20240526115941891.png)

![image-20240526120643615](images\image-20240526120643615.png)

四元数的引入：旋转与旋转之间的插值

### 2. 视图变换 Viewing Transformation

视图变换：改变相机位置、方向

#### 初始相机定义

![image-20240526122454355](images\image-20240526122454355.png)

#### 相机标准位置

![image-20240526122853628](images\image-20240526122853628.png)

#### 相机旋转矩阵

![image-20240526123402740](images\image-20240526123402740.png)

模型要和相机一起变换

### 3. 投影变换 Projection Transformation

3D到2D

![image-20240526125236787](images\image-20240526125236787.png)

#### 正交投影 Orthographic Projection

映射到标准立方体：先把中心点平移到原点，再缩放

![image-20240526125617410](images\image-20240526125617410.png)

![image-20240526130050798](images\image-20240526130050798.png)

#### 透视投影 Perspective Projection

映射到立方体的变换矩阵：

![image-20240526133813949](images\image-20240526133813949.png)

## 三、Rasterization 光栅化 

定义视锥的长宽比（Aspect ratio）和可视角度（fovY）

![image-20240526161143876](images\image-20240526161143876.png)

![image-20240526161358648](images\image-20240526161358648.png)

光栅化 = 绘制到屏幕上

像素：一个像素是一个有着均匀颜色的小方块，是RGB的混合

像素的坐标：

![image-20240526162516167](images\image-20240526162516167.png)

视口变换矩阵：

![image-20240526162635441](images\image-20240526162635441.png)

三角形得到广泛应用的原因：三角形是最基础的多边形；任何多边形都能拆成三角形；三角形内部一定是平面的；三角形内外定义是清晰的

### 采样

给一个三角形，判断像素中心在不在三角形内：

![image-20240526164959012](images\image-20240526164959012.png)

### 光栅化

![image-20240526165253140](images\image-20240526165253140.png)

### AABB包围盒

![image-20240526165815393](images\image-20240526165815393.png)

### 走样

 走样：锯齿、摩尔纹、车轮效应

走样原因：信号变化太快，采样太慢

### 反走样

在采样之前先做模糊

### 傅里叶级数展开

![image-20240526174006081](images\image-20240526174006081.png)

![image-20240526174022476](images\image-20240526174022476.png)

采样频率如果太慢，就会产生走样

### 傅里叶变换

可以把某个函数/图像从时域Spatial Domain变到频域Frequency Domain（频谱）

低频多，高频少：

![image-20240526211715322](images\image-20240526211715322.png)

滤波：把某个特定的频段去掉。

下图为高通滤波，只有高频信号可以通过。

![image-20240526212013781](images\image-20240526212013781.png)

下图为低通滤波，只有低频信号可以通过。

![image-20240526212247555](images\image-20240526212247555.png)

带通滤波

![image-20240526212453386](images\image-20240526212453386.png)

滤波 = 平均 = 卷积

卷积示例：

![image-20240526212907587](images\image-20240526212907587.png)

时域上的卷积相当于频域上的乘积，时域上的乘积相当于频域上的卷积

每个像素取周围3*3的盒子（box filter）做点乘操作：模糊

![image-20240526213456238](images\image-20240526213456238.png)

如果盒子在时域上变大，那么对应在频域上会变小

时域上：采样 = 原始信号 * 冲击函数

在频域上：采样就是在重复原始信号的频谱

![image-20240526215752914](images\image-20240526215752914.png)

产生走样的原因：

采样的间隔会影响频谱的复制粘贴间隔，采样的不够快就会导致复制粘贴原频谱的间隔小 （混叠）

![image-20240526220424668](images\image-20240526220424668.png)

改善走样造成的问题的方法：增加采样频率（但是需要高分辨率）；反走样：

==先拿掉高频信号（模糊），再采样==

![image-20240526221239133](images\image-20240526221239133.png)

对于一个三角形：对每个覆盖到的像素求平均

![image-20240526221856984](images\image-20240526221856984.png)

### MSAA：用更多采样点进行反走样

把一个像素分为多个采样点，近似一个合理的覆盖率

![image-20240526222348031](images\image-20240526222348031.png)

![image-20240526222408481](images\image-20240526222408481.png)

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

![image-20240528092057011](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20240528092057011.png)

n：法线向量

v：观测方向

l：光照方向

表面属性：颜色、亮度（shininess）

shading不考虑其它物体的存在，也不考虑阴影，只考虑每个点自己，有局部性（local）

#### 漫反射 Diffuse Reflection

任一shading point周围单位面积接收到的能量和光照方向与法线方向之间的夹角的余弦成正比

cosΘ = l · n （l和n都为单位向量）

![image-20240528092018132](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20240528092018132.png)

球壳离光源距离为1时，定义光强为I；则球壳离光源距离为r时，定义光强为I/r^2^（球壳面积*光强守恒）

==漫反射公式==

![image-20240528092033821](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20240528092033821.png)

到达的能量➡接收的能量

点有颜色的原因：它吸收了一部分能量，反射出去的是没吸收的能量

漫反射与v完全没关系，从各个地方看到的都是一样的

#### 高光 Specular Term

高光反射是在观察方向接近镜面反射的方向，即法线向量接近半程向量方向

==高光反射公式==

![image-20240528122112098](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20240528122112098.png)

用指数是降低容忍度，布林冯一般用100~200

![image-20240528122808183](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20240528122808183.png)

#### 环境光 Ambient Term

==环境光反射公式==

![image-20240528123110854](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20240528123110854.png)

总结：==布林冯反射模型公式==：对每个点应用该公式

![image-20240528123335765](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20240528123335765.png)



### 着色频率

Flat Shading：对每个三角形求法线，计算出着色结果就是一个三角形的着色结果

Gouraud Shading：对每个顶点着色，三个顶点为一个三角形，每个三角形内部的颜色通过插值的方法计算

> 求顶点法线：顶点相邻面的法线加权求平均
>
> ![image-20240528145020574](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20240528145020574.png)

Phong Shading：对每个像素着色

每条法线都是**单位向量**



### 图形渲染管线（Real-time Rendering）

![image-20240528145639170](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20240528145639170.png)

shader：每个像素都会执行一次的程序

vertex shader：顶点着色器

fragment/pixel shader：片段/像素着色器

GPU的并行度很高

### 纹理映射

uv

![image-20240528160227099](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20240528160227099.png)



### 重心坐标

重心坐标是为了插值

对于三角形内的点坐标：

![image-20240528161334631](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20240528161334631.png)

通过面积比得到重心：

![image-20240528161659238](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20240528161659238.png)

![image-20240528162453430](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20240528162453430.png)

做插值处理：

![image-20240528163813586](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20240528163813586.png)

但是重心坐标在投影下会变化，所以三维空间中的属性建议==在三维空间中做插值==，再对应到二维结果上去

纹理映射实现伪代码：

texel：纹理元素

![image-20240528165216690](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20240528165216690.png)

纹理分辨率太低的解决方法：

![image-20240528170432888](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20240528170432888.png)

Nearest：把小数部分四舍五入成为整数

Bilinear：==双线性插值==，找到相邻的4个整数点，进行两段lerp插值

![image-20240528171001677](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20240528171001677.png)

Bicubic：与Bilinear类似，是找到相邻的16个整数点，进行三段lerp插值

纹理分辨率太高（纹理太大）会产生走样问题：

原因：远处一个像素覆盖多个纹素

![image-20240528172419517](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20240528172419517.png)

解决方法：避免采样

使用范围查询，快速得出平均值

MipMap：快、不准、正方形的范围查询

存储量是原来的4/3

一张图片中有很多图片，每一张图片的分辨率是递减的，渲染器在调用它们时会根据距离自动切换

像素对应的纹理区域近似：

![image-20240528190121426](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20240528190121426.png)

通过这个区域计算出它在第几层会变成一个像素大小

三线性插值：两次查询，一次插值

![image-20240528190831017](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20240528190831017.png)

MipMap问题：Overblur

解决方法：

引入各向异性过滤Anisotropic Filtering

1. Ripmaps and summed area tables 预先计算在x、y两个方向的压缩图，允许查到矩形区域

![image-20240528191529090](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20240528191529090.png)

2. 引入EWA过滤，将不规则图形拆成很多椭圆，多次查询

   ![image-20240528191822009](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20240528191822009.png)

## 五、Geometry 几何

