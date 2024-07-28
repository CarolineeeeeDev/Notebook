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

叉乘结果是正的说明后项向量在前项向量的左侧，叉乘结果是负的说明后项向量在前项向量的右侧；

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

**光栅化 = 绘制到屏幕上**

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

#### 低通滤波

在采样之前先做模糊

**傅里叶级数展开**

![image-20240526174006081](images\image-20240526174006081.png)

![image-20240526174022476](images\image-20240526174022476.png)

采样频率如果太慢，就会产生走样

**傅里叶变换**

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

#### MSAA

多重采样抗锯齿，用更多采样点进行反走样

把一个像素分为多个采样点，近似一个合理的覆盖率

![image-20240526222348031](images\image-20240526222348031.png)

![image-20240526222408481](images\image-20240526222408481.png)

通过MSAA可以得到抗锯齿效果，但是增大了计算量，不过很多样本得到了复用，计算量不会增加那么大

#### 其它抗锯齿方法

**SSAA**：先把低分辨率变为高分辨率处理（增加采样点），再变回低分辨率

 **==TAA==** 时间性抗锯齿：目前最主流的抗锯齿技术，复用上一帧每个像素的值继续产生作用，能够很好地缓解物体运动造成的闪烁。**抗锯齿效果极佳，但是会造成严重的画面模糊。**

**FXAA** 快速近似抗锯齿：图像的后期处理，检测图像的边缘并对其进行模糊处理。**抗锯齿效果较差，但是性能消耗极低。**

**SMAA**边缘抗锯齿技术：类似于FXAA，是一种基于图像的抗锯齿技术，它通过检测和平滑图像中的边缘来减少锯齿效应。

**TXAA**：TAA+MSAA

**FSR2**：超分辨率 Super resolution：是 **AMD**开发的从低分辨率到高分辨率的优化方法，它会根据之前帧的信息以及当前帧的低分辨率图像生成高分辨率图像。这种技术可以在保持较高帧率的情况下，显著提升图像的细节和清晰度。

**DLSS** ：是 **NVIDIA** 开发的一种图像重建技术，利用深度学习和 AI 算法来提升游戏的图像分辨率。

![image-20240529121230931](images\image-20240529121230931.png)

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

![image-20240528092057011](images\image-20240528092057011.png)

n：法线向量

v：观测方向

l：光照方向

表面属性：颜色、亮度（shininess）

shading不考虑其它物体的存在，也不考虑阴影，只考虑每个点自己，有局部性（local）

#### 漫反射 Diffuse Reflection

任一shading point周围单位面积接收到的能量和光照方向与法线方向之间的夹角的余弦成正比

cosΘ = l · n （l和n都为单位向量）

![image-20240528092018132](images\image-20240528092018132.png)

球壳离光源距离为1时，定义光强为I；则球壳离光源距离为r时，定义光强为I/r^2^（球壳面积*光强守恒）

==漫反射公式==

![image-20240528092033821](images\image-20240528092033821.png)

到达的能量➡接收的能量

点有颜色的原因：它吸收了一部分能量，反射出去的是没吸收的能量

漫反射与v完全没关系，从各个地方看到的都是一样的

#### 高光 Specular Term

高光反射是在观察方向接近镜面反射的方向，即法线向量接近半程向量方向

==高光反射公式==

![image-20240528122112098](images\image-20240528122112098.png)

用指数是降低容忍度，布林冯一般用100~200

![image-20240528122808183](images\image-20240528122808183.png)

#### 环境光 Ambient Term

==环境光反射公式==

![image-20240528123110854](images\image-20240528123110854.png)

总结：==布林冯反射模型公式==：对每个点应用该公式

![image-20240528123335765](images\image-20240528123335765.png)



### 着色频率

Flat Shading：对每个三角形求法线，计算出着色结果就是一个三角形的着色结果

Gouraud Shading：对每个顶点着色，三个顶点为一个三角形，每个三角形内部的颜色通过插值的方法计算

> 求顶点法线：顶点相邻面的法线加权求平均
>
> ![image-20240528145020574](images\image-20240528145020574.png)

Phong Shading：对每个像素着色

每条法线都是**单位向量**



### 图形渲染管线（Real-time Rendering）

![image-20240528145639170](images\image-20240528145639170.png)

shader：每个像素都会执行一次的程序

vertex shader：顶点着色器

fragment/pixel shader：片段/像素着色器

GPU的并行度很高

### 纹理映射

uv

![image-20240528160227099](images\image-20240528160227099.png)



### 重心坐标

重心坐标是为了插值

对于三角形内的点坐标：

![image-20240528161334631](images\image-20240528161334631.png)

通过面积比得到重心：

![image-20240528161659238](images\image-20240528161659238.png)

![image-20240528162453430](images\image-20240528162453430.png)

做插值处理：

![image-20240528163813586](images\image-20240528163813586.png)

但是重心坐标在投影下会变化，所以三维空间中的属性建议==在三维空间中做插值==，再对应到二维结果上去

纹理映射实现伪代码：

texel：纹理元素

![image-20240528165216690](images\image-20240528165216690.png)

纹理分辨率太低的解决方法：

![image-20240528170432888](images\image-20240528170432888.png)

Nearest：把小数部分四舍五入成为整数

Bilinear：==双线性插值==，找到相邻的4个整数点，进行两段lerp插值

![image-20240528171001677](images\image-20240528171001677.png)

Bicubic：与Bilinear类似，是找到相邻的16个整数点，进行三段lerp插值

纹理分辨率太高（纹理太大）会产生走样问题：

原因：远处一个像素覆盖多个纹素

![image-20240528172419517](images\image-20240528172419517.png)

解决方法：避免采样

使用范围查询，快速得出平均值

MipMap：快、不准、正方形的范围查询

存储量是原来的4/3

一张图片中有很多图片，每一张图片的分辨率是递减的，渲染器在调用它们时会根据距离自动切换

像素对应的纹理区域近似：

![image-20240528190121426](images\image-20240528190121426.png)

通过这个区域计算出它在第几层会变成一个像素大小

三线性插值：两次查询，一次插值

![image-20240528190831017](images\image-20240528190831017.png)

MipMap问题：Overblur

解决方法：

引入各向异性过滤Anisotropic Filtering

1. Ripmaps and summed area tables 预先计算在x、y两个方向的压缩图，允许查到矩形区域

![image-20240528191529090](images\image-20240528191529090.png)

2. 引入EWA过滤，将不规则图形拆成很多椭圆，多次查询

   ![image-20240528191822009](images\image-20240528191822009.png)

### 纹理的应用

#### 环境贴图

将环境光记录在球体上再展开会扭曲

![image-20240529151512679](images\image-20240529151512679.png)

解决办法 Cube Map：存在立方体上变成六张纹理图，但是需要额外的计算

![image-20240529151654397](images\image-20240529151654397.png)

#### 凹凸贴图、法线贴图

用纹理图定义一个点的相对高度、法线信息，没有改变几何信息

有关法线信息的二维计算：

![image-20240529152908029](images\image-20240529152908029.png)



![image-20240529153025982](images\image-20240529153025982.png)

有关法线信息的三维计算：

![image-20240529154651335](images\image-20240529154651335.png)

### 位移贴图

相比于凹凸贴图，位移贴图是真的移动了顶点的位置

![image-20240529155340504](images\image-20240529155340504.png)

DirectX提供了动态曲面细分，根据需要细分模型

纹理还可以：定义三维程序噪声、存一些计算好的信息（AO信息）、体积渲染



## 五、Geometry 几何

### 几何表示方法

#### 隐式几何 Implicit Representations of Geometry

满足一定特定关系的点都在一个平面上 **f(x,y,z) = 0**

判定一个点是否在平面上还是平面内或外很容易（函数大于等于小于0），但找出所有在平面上的点很难

**表示方法：**

1. 代数平面（**隐式**）：用函数式定义几何

2. ==CSG== (Constructive Solid Geometry) (**隐式**) ： 用数学运算定义几何

3. 距离函数（**隐式**）：描述一个点到这个表面的最近距离，可正可负。可以进行blend操作（SDF : signed distance function）

![image-20240530190627380](images\image-20240530190627380.png)

4. 水平集（**隐式**）：类似于距离函数，区别是把距离写在格子上。等于0的地方就是物体表面。

5. 分型（**隐式**）：自相似

优点：表述很容易；查询点在里外较简单；容易做光线和表面求交点；对简单集合能给出确切描述；容易描述拓扑结构

缺点：很难描述复杂几何

#### 显式几何 Explicit Representations of Geometry

通过参数映射的方法定义一个平面：**(u,v) <--->(x,y,z)**

点在平面里面还是外面很难看出

**表示方法：**

1. 点云（**显式**）：密集的点表示几何，变成不同的面
2. 多边形面（**显式**）：应用非常广泛，用三角形四边形等描述复杂的物体

常用文件格式：

![image-20240530192816933](images\image-20240530192816933.png)

### 曲线和曲面

#### 曲线

##### 贝塞尔曲线

用一系列的控制点定义曲线

找到时间t上的点连成曲线：

![image-20240530193445580](images\image-20240530193445580.png)

![image-20240530193637748](images\image-20240530193637748.png)

代数表示方法（线性插值）：（这里的2不是平方，是次数）

![image-20240530193949157](images\image-20240530193949157.png)

![image-20240530194147518](images\image-20240530194147518.png)

![image-20240530194437677](images\image-20240530194437677.png)

规定：

1. t=0时一定在起点，t=1时一定在终点；
2. 如果想对贝塞尔曲线做**仿射变换**，则只需要对控制点做仿射变换，但是对投影不是这样
3. 画出来的贝塞尔曲线一定得在所有控制点形成的**凸包**（最小凸多边形）内

##### 逐段（Piecewise）贝塞尔曲线

每次用较少的控制点定义一段贝塞尔曲线，然后把这些贝塞尔曲线连起来

曲线连续：

1. 前一条终点 = 后一条起点

2. 保证连起来的曲线是光滑的：前一条最后一段和后一条第一段导数相同，即：

   ![image-20240530200821270](images\image-20240530200821270.png)

##### 其他

样条：满足一定连续性，是一个可控的曲线

B-样条：奇函数样条，是对贝塞尔曲线的扩展，具有局部性（有一定影响范围）

#### 曲面

原理：在两个方向上分别应用贝塞尔曲线

![image-20240530202118209](images\image-20240530202118209.png)

因此需要一个二维的控制的东西：

![image-20240530202444433](images\image-20240530202444433.png)

![image-20240530202456009](images\image-20240530202456009.png)

### 网格处理

几何处理：网格细分、网格简化、网格正规化

#### 网格细分

upsampling

##### 1. loop subdivision

只适用于全三角形网格

两步操作：三角形数量增多、调整三角形位置（区分新、旧顶点）

更新**新的顶点**的位置：

![image-20240531094200358](images\image-20240531094200358.png)

更新**旧的顶点**的位置：

![image-20240531094145135](images\image-20240531094145135.png)

##### 2. catmull-clark subdivision

对于网格的一般情况，不只是三角形

定义：四边形面、非四边形面、奇异点（度不为4的点）

做法：为每条边和每个面加上中点，连接所有的中点

#### 网格简化

downsampling

二次误差度量：新的点是到原来各个面的距离平方和最小的点

![image-20240531161959604](images\image-20240531161959604.png)

按照二次误差度量**由小到大**做贪缩：优先队列/堆

#### 网格正规化

### 阴影图 Shadow Mapping

只能做硬阴影，会产生走样现象

核心思想：如果点不在阴影里=可以从摄像机看到这个点，且光源也能看到这个点

第一步操作：从光源看向场景，做一遍光栅化

![image-20240601204659060](C:\Users\LilSc\AppData\Roaming\Typora\typora-user-images\image-20240601204659060.png)

第二步操作：从眼睛出发再次看向场景，并投影回光源，判断实际到光源的距离是否与之前记录的深度一致

![image-20240601204642940](C:\Users\LilSc\AppData\Roaming\Typora\typora-user-images\image-20240601204642940.png)

![image-20240601204720748](C:\Users\LilSc\AppData\Roaming\Typora\typora-user-images\image-20240601204720748.png)

点光源是不会产生软阴影的，软阴影的产生一定是因为光源有一定的大小

![image-20240601211347179](C:\Users\LilSc\AppData\Roaming\Typora\typora-user-images\image-20240601211347179.png)

## 六、光线追踪

光栅化不能很好地表示全局效果：

![image-20240601212441310](C:\Users\LilSc\AppData\Roaming\Typora\typora-user-images\image-20240601212441310.png)

光线追踪很准确，但是非常慢

光栅化：实时；光线追踪：离线

### 最基础的光线追踪算法

![image-20240601213606713](C:\Users\LilSc\AppData\Roaming\Typora\typora-user-images\image-20240601213606713.png)

算某个点的着色

只弹射一次：

![image-20240601220504854](C:\Users\LilSc\AppData\Roaming\Typora\typora-user-images\image-20240601220504854.png)

多次弹射（Whitted Ray Tracing）：

![image-20240601221438178](C:\Users\LilSc\AppData\Roaming\Typora\typora-user-images\image-20240601221438178.png)

### 求光线和物体表面的交点

光线上任意一个点的定义r(t)

求光线和球的交点：

![image-20240601222916228](C:\Users\LilSc\AppData\Roaming\Typora\typora-user-images\image-20240601222916228.png)

![image-20240601223012201](C:\Users\LilSc\AppData\Roaming\Typora\typora-user-images\image-20240601223012201.png)

让光线到多边形内的一点和多边形交点一定是奇数，光线到多边形外的一点和多边形交点一定是偶数；

推广到3D也是可行的

![image-20240601225509095](C:\Users\LilSc\AppData\Roaming\Typora\typora-user-images\image-20240601225509095.png)

如何求光线和三角形的交点：

 分解为：光线和平面求交点+判断交点在不在三角形内这两个步骤

平面可以定义为： 一个（法线）方向和一个平面上的点

![image-20240602134517446](C:\Users\LilSc\AppData\Roaming\Typora\typora-user-images\image-20240602134517446.png)

求交点：

![image-20240602134541270](C:\Users\LilSc\AppData\Roaming\Typora\typora-user-images\image-20240602134541270.png)

MT算法：一次解出光线与平面的交点在不在三角形内--用重心坐标表示三角形内的点

用克拉默法则求解

![image-20240602135142315](C:\Users\LilSc\AppData\Roaming\Typora\typora-user-images\image-20240602135142315.png)

如何让光线和三角形面求交点**加速**：

包围盒/包围体积：常用AABB包围盒

![image-20240602140255479](C:\Users\LilSc\AppData\Roaming\Typora\typora-user-images\image-20240602140255479.png)

对于2D情况（3D情况也一样）：最后结果是求**交集**

![image-20240602142359137](C:\Users\LilSc\AppData\Roaming\Typora\typora-user-images\image-20240602142359137.png)

对于3D情况：只有当进入所有pair时候才算进入，只要退出了其中一个pair就算退出

![image-20240602142750847](C:\Users\LilSc\AppData\Roaming\Typora\typora-user-images\image-20240602142750847.png)

如果离开盒子的时间小于0：盒子在光线背后，不可能有交点

如果离开的时间大于0而进入的时间时间小于0：光线的起点在盒子里

总结：当且仅当**进入时间小于离开时间**且**离开时间非负**的情况下，光线与包围盒有交点

#### 格子解法

光线和盒子求交点会快一些（直线的光栅化）

![image-20240602150031226](C:\Users\LilSc\AppData\Roaming\Typora\typora-user-images\image-20240602150031226.png)

#### 空间划分

八叉树、KD树、BSP树

![image-20240602152540854](C:\Users\LilSc\AppData\Roaming\Typora\typora-user-images\image-20240602152540854.png)

#####  KD树

只需要在叶子节点存储要处理的 形状

![image-20240602154329837](C:\Users\LilSc\AppData\Roaming\Typora\typora-user-images\image-20240602154329837.png)

![image-20240602155114124](C:\Users\LilSc\AppData\Roaming\Typora\typora-user-images\image-20240602155114124.png)

#### ==物体划分--BVH树==

 一个物体只可能出现在一个格子里

![image-20240602155535987](C:\Users\LilSc\AppData\Roaming\Typora\typora-user-images\image-20240602155535987.png)

 划分的方法：沿着最长轴划分/找中间的（第n/2个）物体划分--快速选择算法O(n)时间复杂度

BVH也是叶子节点存实际的物体

算法伪代码：

![image-20240602160433830](C:\Users\LilSc\AppData\Roaming\Typora\typora-user-images\image-20240602160433830.png)

### 辐射度量学

 辐射度量学定义了精准物理量--比whitted风格更高级

光的空间属性：辐射通量Radiant flux、辐射强度Intensity、辐射照度Irradiance、辐射亮度Radiance

Flux的定义：

![image-20240602162715399](C:\Users\LilSc\AppData\Roaming\Typora\typora-user-images\image-20240602162715399.png)

![image-20240602162732014](C:\Users\LilSc\AppData\Roaming\Typora\typora-user-images\image-20240602162732014.png)

Intensity、Irradiance、Radiance的定义：

![image-20240602162913131](C:\Users\LilSc\AppData\Roaming\Typora\typora-user-images\image-20240602162913131.png)

==Intensity：单位立体角上的辐射通量==

![image-20240602163743226](C:\Users\LilSc\AppData\Roaming\Typora\typora-user-images\image-20240602163743226.png)

立体角：球面对应的面积除以半径的平方

![image-20240602164144167](C:\Users\LilSc\AppData\Roaming\Typora\typora-user-images\image-20240602164144167.png)

![image-20240602163950816](C:\Users\LilSc\AppData\Roaming\Typora\typora-user-images\image-20240602163950816.png)

对于各向同性（均匀分布）点光源：立体角为4Π

![image-20240602164736765](C:\Users\LilSc\AppData\Roaming\Typora\typora-user-images\image-20240602164736765.png)

 

==Irradiance：单位面积上的辐射通量==

![image-20240602170152451](C:\Users\LilSc\AppData\Roaming\Typora\typora-user-images\image-20240602170152451.png)

Intensity其实没有变，Irradiance在衰减

![image-20240602170530739](C:\Users\LilSc\AppData\Roaming\Typora\typora-user-images\image-20240602170530739.png)

==Radiance：在单位面积且单位立体角的辐射通量==

![image-20240602170847791](C:\Users\LilSc\AppData\Roaming\Typora\typora-user-images\image-20240602170847791.png)



![image-20240602171033313](D:\Dev\Github\Notebook\刷题\剑指offer\image-20240602171033313.png)

BRDF：双向反射分布函数

从一个方向进来打到某物体后往不同方向上反射的能量分布

定义：任何一个出射方向上radiance的微分除以一个入射点上irradiance的微分

![image-20240602191816951](C:\Users\LilSc\AppData\Roaming\Typora\typora-user-images\image-20240602191816951.png)

用一个方程描述所有的光线传播：

![image-20240602193823796](C:\Users\LilSc\AppData\Roaming\Typora\typora-user-images\image-20240602193823796.png)

![image-20240602194330810](C:\Users\LilSc\AppData\Roaming\Typora\typora-user-images\image-20240602194330810.png)

![image-20240602194356942](C:\Users\LilSc\AppData\Roaming\Typora\typora-user-images\image-20240602194356942.png)
