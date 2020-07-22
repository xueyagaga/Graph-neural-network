# 数据

对于图卷积神经网络，尤其是交通领域的应用，输入数据一般是这样的结构。

![](.gitbook/assets/image%20%288%29.png)

其中64代表batchsize，6代表时间片长度，5代表图上顶点数目，要是在每个顶点上仅考虑一个观测值就是一维的数据，也有可能是多维的多种观测值或有向图上的数据。

![](.gitbook/assets/image%20%289%29.png)
