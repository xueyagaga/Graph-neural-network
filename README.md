# Graph-neural-network
图神经网络从入门到精通

## 阅读指南

1. 在线观看请使用Chrome浏览器，并安装插件：[MathJax Plugin for Github(需科学上网)](https://chrome.google.com/webstore/detail/mathjax-plugin-for-github/ioemnmodlmafdkllaclgeombjnmnbima)， 插件[Github地址](https://github.com/orsharir/github-mathjax)
2. 或下载内容到本地，使用markdown相关软件打开，如：[Typora](https://typora.io/)

## 文章列表

- <a href = "#基本概念与常用符号">基本概念与常用符号</a>
  - <a href = "#图">图</a>
  - <a href = "#顶点的度">顶点的度</a>
  - <a href = "#图的表现形式">图的表现形式</a>
    - <a href = "#邻接矩阵">邻接矩阵</a>
    - <a href = "#度矩阵">度矩阵</a>
    - <a href = "#拉普拉斯矩阵">拉普拉斯矩阵</a>
  - <a href = "#其他相关概念">其他相关概念</a>
- <a href = "#循环图神经网络RecGNNs">循环图神经网络RecGNNs</a>
- <a href = "#卷积图神经网络ConvGNNs">卷积图神经网络ConvGNNs</a>
- <a href = "#图自编码器GAEs">图自编码器GAEs</a>
- <a href = "#时空图神经网络STGNNs">时空图神经网络STGNNs</a>
- <a href = "#图神经网络的输出">图神经网络的输出</a>
- <a href = "# 图神经网络训练框架">图神经网络训练框架</a>
- <a href = "#易混淆概念">易混淆概念</a>
  - <a href = "#图神经网络与图嵌入">图神经网络与图嵌入</a>
- <a href = "#参考文献">参考文献</a>

## [基本概念与常用符号](#content)

### [图](#content)

<div align = "center"><image src="https://github.com/Knowledge-Precipitation-Tribe/Graph-neural-network/blob/master/images/graph.png" width = "300" height = "160" alt="axis" align=center /></div>

图是一种数据结构，由顶点集$V$和边集$E$组成,表示为$G=(V,E)$，其中$v_{i} \in V$代表每个顶点，$e_{i j}=\left(v_{i}, v_{j}\right) \in E$代表表每条边，图分为两种：

- 有向图：每条边都带有方向
- 无向图：每条边都不带有方向，上图就是一个无向图

### [顶点的度](#content)

与顶点$V$相关的边的条数称为顶点$V$的度。

### [图的表现形式](#content)

#### [邻接矩阵](#content)

邻接矩阵是表示顶点之间相邻关系的矩阵。设$G=(V,E)$是具有$n$个顶点的图，顶点序号依次为$0,1,...,n-1$,则$G$的邻接矩阵是具有如下定义的$n$阶方阵$A$：

- $A[i][j]=1$表示顶点$i$与顶点$j$邻接，即$i$与$j$之间存在边
- $A[i][j]=0$表示顶点$i$与顶点$j$不邻接，即$i$与$j$之间没有边

<div align = "center"><image src="https://github.com/Knowledge-Precipitation-Tribe/Graph-neural-network/blob/master/images/adjMatrix.png" width = "300" height = "200" alt="axis" align=center /></div>

#### [度矩阵](#content)

度矩阵其中包含的信息为的每一个顶点的度数，度矩阵$D$:

<div align = "center"><image src="https://github.com/Knowledge-Precipitation-Tribe/Graph-neural-network/blob/master/images/degreeMatrix.png" width = "300" height = "200" alt="axis" align=center /></div>

#### [拉普拉斯矩阵](#content)

给定一个有$n$个顶点的图$G=(V,E)$，其拉普拉斯矩阵被定义为$L=D-A$，$D$其中为图的度矩阵，$A$为图的邻接矩阵，拉普拉斯矩阵$L$:

<div align = "center"><image src="https://github.com/Knowledge-Precipitation-Tribe/Graph-neural-network/blob/master/images/laplaMatrix.png" width = "300" height = "200" alt="axis" align=center /></div>

### [其他相关概念](#content)

<img><img src="https://cdn.mathpix.com/snip/images/7GxH8KCmCtUy_O3IUoVb65iuSZmRCF3LDnDKQDrNV7E.original.fullsize.png" />

## [循环图神经网络RecGNNs](#contents)

循环图神经网络（RecGNNs）旨在学习具有递归神经体系结构的节点表示。他们假设图中的一个节点不断与其邻居交换信息/消息，直到达到稳定的平衡为止。

## [卷积图神经网络ConvGNNs](#contents)

卷积图神经网络（ConvGNNs）概括了从网格数据到图数据的卷积操作。主要思想是通过汇总节点自身的特征$\mathbf{X}_{v}$和邻居的特征$\mathbf{X}_{u}$来生成节点$v$的表示形式，其中$u \in N(v)$。与RecGNN不同，ConvGNN堆叠多个图卷积层以提取高级节点表示。ConvGNN在建立许多其他复杂的GNN模型中起着核心作用。

## [图自编码器GAEs](#contents)

图自动编码器（GAE）是无监督的学习框架，可将节点/图编码到潜在的矢量空间中，并从编码信息中重建图数据。GAEs用于学习网络嵌入和图生成分布。对于网络嵌入，GAEs主要通过重建图结构信息（例如图邻接矩阵）来学习潜在节点表示。对于图生成，某些方法逐步生成图的节点和边，而其他方法则直接输出图。

## [时空图神经网络STGNNs](#content)

时空图是属性图，其中节点输入随时间动态变化。时空图的定义为：$G^{(t)}=\left(\mathbf{V}, \mathbf{E}, \mathbf{X}^{(t)}\right)$其中$\mathbf{X}^{(t)} \in \mathbf{R}^{n \times d}$。时空图神经网络（STGNNs）旨在从时空图学习隐藏模式，这种模式在各种应用中变得越来越重要，例如交通速度预测，驾驶员操纵预期和人类行为识别。STGNNs的关键思想是同时考虑空间依赖性和时间依赖性。当前许多方法将图卷积与RNNs或CNNs集成在一起以捕获空间依赖性，从而对时间依赖性进行建模。

## [图神经网络的输出](#content)

使用图结构和节点内容信息作为输入，GNNs的输出可以通过以下机制之一专注于不同的图分析任务：

- Node-level：节点级的输出与节点回归和分类任务有关。RecGNN和ConvGNN可以通过信息传播/图卷积来提取高级的节点表示。使用多感知器或softmax层作为输出层，GNNs能够以端到端的方式执行节点级别的任务。
- Edge-level：边级别输出与边级别分类和链接预测任务有关。将来自GNNs的两个节点的隐藏表示作为输入，可以利用相似度函数或神经网络来预测边的标签/连接强度。
- Graph-level：图级别的输出与图分类任务有关。为了获得图级别的紧凑表示，GNNs通常与pooling和readout操作结合使用。

## [图神经网络训练框架](#content)



## [易混淆概念](#content)

### [图神经网络与图嵌入](#content)

#### 图嵌入

将网络中的节点表示为低维向量表示，同时保留网络拓扑结构和节点内容信息，将获得的嵌入向量用于分类，聚类等问题中。

#### 图神经网络

将获得的嵌入向量用于分类，聚类等问题中

#### 两者主要区别

GNN是一组为解决各种任务而设计的神经网络模型，GNN是一组为解决各种任务而设计的神经网络模型。<br>

图嵌入是针对同一种任务的各种方法，图嵌入也包含非深度学习的方法，例如矩阵分解以及随机游走等。

## [参考文献](#content)

[1] THUNLP: [GNNpapers](https://github.com/thunlp/GNNPapers)

[2] [A Comprehensive Survey on Graph Neural Networks](https://arxiv.org/pdf/1901.00596.pdf)

