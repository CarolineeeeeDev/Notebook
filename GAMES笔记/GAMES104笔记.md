# GAMES104

[TOC]

## 01.从入门到实践

### 什么是游戏引擎

1. Technology Foundation of Matrix 虚拟世界的技术基础
2. Productivity Tools of Creation 创造力和生产力的工具 -> 为艺术家和开发者创造工具
3. Art of Complexity 复杂性系统的艺术

### 学习顺序

基础构建Basic Elements、渲染Rendering、动画Animation、物理表达Physics、游戏规则Gameplay、特效系统Misc. Systems、工具体系Toolset、网络Online Gaming、前沿技术Advanced Technology（DOP, Job System, Lumen, Nanite）

参考书籍： Game Engine Architecture



## 02.引擎架构分层

从上到下：工具层Tool Layer，功能层Function Layer，资源层Resource Layer，核心层Core Layer， 平台层Platform Layer；还有第三方库

### 资源层

Offline Resource Importing ： Resource资源转换成Asset资产

数据关联

GUID唯一识别号

实时资产管理器 handle系统

核心:管理生命周期

gc垃圾回收很重要

延迟加载：玩到哪才加载

### 功能层

Tick概念->tick函数两大神兽：

tickLogic(float delta_time) 逻辑

tickRender(float delta_time) 渲染

多线程算法（*）多核架构是未来

### 核心层

数学库

一切为效率服务

SIMD，并行计算

做一套自己的数据结构，容器实现

内存管理：类似操作系统，内存池（*）

底层内存管理三条逻辑：1.尽可能将数据放在一起   2.数据尽可能按顺序访问   3.读写尽可能一次一批（多量）

一般代码要求非常高

### 平台层

掩盖掉平台差异度

RHI(Render Hardware Interface) ： 重新定义一次Graphics的API，把各个硬件的sdk的区别封装起来

### 工具层

以地图编辑器为中心形成的一系列编辑器，例如逻辑编辑器（蓝图）、材质编辑器、动画编辑器等

DCC：别人开发的资产生产工具，开发的资源通过一条管线（Asset Conditioning Pipeline，各种导入导出器）统一变成游戏资产



为什么引擎要分层：降低复杂度，封装；上层更灵活，容易根据改变需求来改变，而下层更稳定

### 总结

引擎是分层架构的，分为五层

越底层的代码越稳定，质量也要求越高；越上面的代码设计得越开放，比较灵活，能够适应不同的需求

游戏这个虚拟世界的核心是靠tick函数驱动的



## 03.如何构建游戏世界

动态游戏物体、静态游戏物体、环境（地形、天空、植被）、TriggerBox等 ： 统一都为GameObject（GO）

面向对象：property、behavior

问题：没有清晰的父子关系

解法：组件化代替继承

ComponentBase->Components->GameObjectBase

基于GameObject的Tick×  基于Component的Tick√

事件机制event：解耦合  可扩展的消息系统

游戏物体管理、场景管理（空间划分算法：画格子、四叉树、八叉树Octree，BVH, BSP, Scene Graph）

### 其它需要管理的复杂情况

父GO先tick，子GO后tick

pretick和posttick：解决时序性问题

Q&A

如果一个tick时间过长怎么办：把步长传进去，补偿位移等（掉帧？）/跳过一个tick（分帧？）；分帧处理策略

tick的时候，渲染线程和逻辑线程怎么同步：tickLogic会比tickRender早一些

如何debug：打印log

物理和动画相互影响的时候怎么处理：插值



## 04.游戏引擎中的渲染实践Rendering

游戏绘制中的挑战：所有绘制算法汇集在一起，所有算法要有高效率：深度适配当代硬件，帧率必须稳定，只能使用一部分CPU资源Profiling

### 游戏引擎中的绘制知识点（结合实际进化而来）

Rendering基础：GPU硬件

实战：光照模型，材质系统，Shader模型

特殊子系统：地形系统，天空系统，后处理系统

Pipeline：延迟渲染等

### 渲染基础

Rendering Pipeline：参考GAMES101，投影、光栅化、着色绘制、纹理sampling等

#### GPU显卡

SIMD

单指令多数据，指令级并行技术

SIMT





### 总结：

在游戏世界中，所有东西都可以抽象为一个GameObject

GameObject可以看成由很多Components组成

所有的component在tick更新

在component中，所有GameObject通过一套复杂的消息机制event system进行通信

场景管理需要高效的层次结构管理机制







