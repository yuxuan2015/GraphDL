# GraphDL

图深度学习是当前深度学习领域最热门的方向之一，图神经网络（GNN）不仅在理论上有所创新，在工业界中也真实的应用。本文介绍Github上热门的图神经网络源码及框架，方便研究人员和工程师上手图深度学习。

近两年来，图卷积、图注意力网络等图神经网络在学术界、工业界都有广泛的应用。虽然大多数图神经网络理论包含复杂的公式推导，但最终产出的网络结构（公式）缺一般比较简单，但这并不意味着图神经网络的实现会很简单。

导致图神经网络实现复杂的原因主要有以下几个：

以图卷积网络为例，它的原版依赖完整邻接矩阵和全部节点作为输入，对内存、显存和计算效率都造成了限制。好在目前有一些理论如FaskGCN可以通过mini-batch等方式来进行数据切分从而解决这个问题。
虽然利用稀疏矩阵可以一定程度上缓解上述问题，但依然不能处理大规模的数据。另外，由于多层网络结构的复杂，一般在实现时要同时实现稀疏版和非稀疏版的组件。
对图结构数据的预处理比较麻烦。例如在处理异构网络时，有时需要对每种类型的节点进行独立地编号、为每种关系独立建立子图等，才能将图数据转换为深度学习模型可用的数值化数据，并且任何一个细节可能都会影响算法的效率（如邻节点列表的数据结构使用list和set会导致不同的采样效率和查询效率）。
需要一些基于图的额外操作，例如Random Walk、有类型约束的Random Walk（Meta-path）等，由于图结构的复杂性，这些操作在单机上的实现都比较费力，更不用说在大规模分布式上。


图深度学习研究者和工业界在Github上开源了一些优秀的图神经网络的实现其框架，都从一定程度上去解决了上述的问题，非常值得我们借鉴。下面我们列出一些优秀的Github仓库：

1 DeepWalk / LINE

链接：

DeepWalk: https://github.com/phanein/deepwalk

LINE: https://github.com/tangjianpku/LINE

简介：

虽然DeepWalk和LINE属于网络表示学习中的算法，与现在端到端的图神经网络有一定的区别，但目前一些图神经网络应用（如社交网络、引用网络节点分类）依然使用DeepWalk/LINE来作为预训练算法，无监督地为节点获得初始特征表示。另外，DeepWalk项目中的Random Walk也可以被直接拿来用作图神经网络的数据采样操作。

2 图卷积网络GCN TensorFlow/PyTorch版

链接：

TensorFlow版本: https://github.com/tkipf/gcn

PyTorch版本: https://github.com/tkipf/pygcn

Keras版本：https://github.com/tkipf/keras-gcn

简介：

GCN论文作者提供的源码，该源码提供了大量关于稀疏矩阵的代码。例如如何构建稀疏的变换矩阵（这部分代码被其他许多项目复用）、如何将稀疏CSR矩阵变换为TensorFlow/PyTorch的稀疏Tensor，以及如何构建兼容稀疏和非稀疏的全连接层等，几乎是图神经网络必读的源码之一了。

3 快速图卷积网络FastGCN TensorFlow版

链接：

https://github.com/matenure/FastGCN

简介：

FastGCN作者提供的源码，基于采样的方式构建mini-match来训练GCN，解决了GCN不能处理大规模数据的问题。

4 图注意力网络GAT TensorFlow版

链接：

https://github.com/PetarV-/GAT

简介：

GAT论文作者提供的源码。源码中关于mask的实现、以及稀疏版GAT的实现值得借鉴。

5 Mini-batch版图注意力网络DeepInf

链接：

https://github.com/xptree/DeepInf

简介：

DeepInf论文其实是GAT的一个应用，但其基于Random Walk采样子图构建mini-batch的方法解决了GAT在大规模网络上应用的问题。

6 DeepMind开源的图神经网络框架Graph Nets

链接：

https://github.com/deepmind/graph_nets

简介：

基于TensorFlow和Sonnet。上面的项目更侧重于节点特征的计算，而graph_nets同时包含节点和边的计算，可用于一些高级任务，如最短路径、物理场景模拟等。

7 工业级分布式图神经网络框架Euler

链接：

https://github.com/alibaba/euler

简介：

Euler是阿里巴巴开源的大规模分布式的图学习框架，配合TensorFlow或者阿里开源的XDL等深度学习工具，它支持用户在数十亿点数百亿边的复杂异构图上进行模型训练。

GCN的应用

1 文本分类

https://github.com/yao8839836/text_gcn

2 relation

https://github.com/tkipf/relational-gcn
