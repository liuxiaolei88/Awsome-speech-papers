


























Tzirakis, Panagiotis, Anurag Kumar, and Jacob Donley. "**Multi-channel speech enhancement using graph neural networks**." _ICASSP 2021-2021 IEEE International Conference on Acoustics, Speech and Signal Processing (ICASSP)_. IEEE, 2021.

ABS & Intro
将每个音频通道视为位于非欧几里德空间，具体而言，是图中的节点。这种形式使我们能够应用图神经网络（GNN）来找到不同通道（节点）之间的空间相关性。我们利用图卷积网络（GCN）将它们纳入U-Net架构的嵌入空间中。

![[../img/Pasted image 20230823144750.png]]

Method
输入首先通过编码器网络，试图从输入中学习更高级的特征（第3.1节）。然后，使用这些音频通道的特征表示构建一个图，通过其节点和边捕获多通道信息。在这一点上，我们使用图卷积网络（GCNs）（第3.3节）来聚合来自每个麦克风的信息。图中每个节点的输出表示被作为解码器的输入，解码器然后将信号转换回其原始维度。最后，计算解码器输出的加权和，将其与参考麦克风的STFT（时频变换）进行（复数）乘法运算，以计算出干净的STFT

构建无向图 G = (V, E)，其中 V 表示图的节点集合，vi 表示图的节点（即麦克风）。E 表示图中两个节点（vi, vj）之间的边。图由邻接矩阵 A表示，D 表示度矩阵。我们考虑加权邻接矩阵，其中 A 的条目对应于图中两个节点（vi, vj）之间的加权边。直观地说，每个权重表示图中两个节点的特征向量之间的相似性。邻接矩阵 A 的这些权重，在训练过程中被学习得到。对于两个节点 vi 和 vj，首先将它们的表示 f_vi 和 f_vj 连接起来，形成 [f_vi || f_vi]，然后将它们通过非线性函数 F([f_vi || f_vj]), 通过将每个节点的权重归一化为总和为一来构建邻接矩阵。过gcn。
![[Pasted image 20230823151119.png]]

 notes
 GCN 在增强的baseline Google引用共28篇

---

Time-Domain Speech Separation Networks With Graph Encoding Auxiliary

---
Hao, Minghui, Jingjing Yu, and Luyao Zhang. "**Spatial-temporal graph convolution network for multichannel speech enhancement**." _ICASSP 2022-2022 IEEE International Conference on Acoustics, Speech and Signal Processing (ICASSP)_. IEEE, 2022.

Abs&Intro
  
与分布式麦克风位置有关的空间依赖性对于多通道语音增强任务至关重要。由于缺乏准确的阵列位置和多通道嘈杂信号的复杂时空关系，这仍然具有挑战性。本文提出了一个由级联时空（ST）模块与通道融合组成的时空图卷积网络，用于处理这个问题。在没有阵列和声学场景的任何先验信息的情况下，设计了一个具有可学习的邻接矩阵的图卷积块，用于捕捉成对通道之间的空间依赖性。然后，将其与时频卷积块嵌入为ST模块，以融合用于目标语音估计的多维相关特征。此外，还提出了一种基于语音可懂度指数（SII）的新型加权损失函数，用于在网络训练期间更多地关注人类理解的重要频带。
![[../img/Pasted image 20230823161512.png]]

Method：

overview：
提出的框架主要由多个级联的时空（ST）模块和一个通道融合模块组成，其中ST模块提取 𝑿 的空间和时频信息。ST模块中的GCN块用于提取与不同麦克风位置相关的多通道信号之间的空间依赖性。然后，通道融合模块将多维相关特征自适应地组合起来，以重建语音成分。

GCN部分
与分布式麦克风位置相关的目标语音成分的空间依赖性可以根据接收到的多通道信号的幅度和相位差来估计。
定义了一个无向图 𝑮 = (𝑽, 𝑬)，其中 𝑽 表示阵列中的麦克风集合，𝑬 是表示成对麦克风接收到的信号之间相关关系的图边集合。这些关系可以由邻接矩阵 𝑨 ∈ ℝ，C×C来表征，其中 𝑨_𝑖,𝑗 表示从第 𝑗 个到第 𝑖 个麦克风的相关权重

CNN部分

多通道融合
每个麦克风通道中恢复的语音频谱的特征权重矩阵语音

损失函数
根据人耳理解的频率形成权重 对loss 加权

---
[需要精读]Chen, Yijiang, Chengdong Liang, and Xiao-Lei Zhang. "**Spatial-temporal Graph Based Multi-channel Speaker Verification With Ad-hoc Microphone Arrays**." _arXiv preprint arXiv:2307.01386_ (2023).

ABS&Intro
本文提出了一种基于时空图卷积网络（GCN）的空间时域方法，用于具有即席麦克风阵列的多通道说话者验证。该方法包括特征聚合块和通道选择块，两者都构建在图结构之上。特征聚合块通过空间时域GCN在不同的时间和通道之间融合说话者特征。基于图的通道选择块排除可能对系统产生负面影响的噪声通道。
当麦克风远离说话者时，录制的语音信号不仅严重衰减，还会受到背景噪声、混响和其他干扰声源的干扰。最终，远场条件下说话者验证系统的性能会急剧下降。
为了降低极端困难远场问题的发生概率，将多个分布式设备组合成一个临时麦克风阵列成为一种新型有效方法，其中临时麦克风阵列中的每个设备，称为临时节点，包含单个麦克风或传统的固定麦克风阵列。与固定阵列相比，基于深度学习的临时麦克风阵列处理的一个关键优势是，它能够通过通道重新加权和选择利用空间距离信息。
提出了一种基于图卷积网络（GCN）的端到端多通道说话者验证框架，以充分挖掘时空信息。该框架包括基于图的时空多通道特征聚合块和基于图的通道选择块。前者通过聚合其相邻帧和通道的时空信息，学习增强每个通道帧的说话者特征，后者则舍弃强噪声通道以进一步提高性能
Method
第一阶段训练的目标是训练一个帧级特征提取器。具体而言，我们首先使用大量单通道语音数据训练一个标准的说话者验证系统，如图1所示。然后，我们保留帧级特征提取器，并丢弃系统的所有其他部分。
第二阶段
时空数据XCT的每个帧重新构造为静态图的节点，并将其邻接矩阵ACT定义为布尔矩阵，其中元素ACT[i, j] = 0表示第i个节点与第j个节点没有直接连接，为了滤除对说话者验证系统产生负面影响的通道，我们进一步设计了一个基于图的通道选择算法

---
Nguyen, Huu Binh, et al. "Multi-Channel Speech Enhancement using a Minimum Variance Distortionless Response Beamformer based on Graph Convolutional Network." _International Journal of Advanced Computer Science and Applications_ 13.10 (2022).