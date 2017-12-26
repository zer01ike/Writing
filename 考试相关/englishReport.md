abstract 
introduction  两人、一人写abstract和introduction前半部分、预计写3段

method 一人、预计写两段

results 一人、预计写两段

discussion&conclusion 一人、预计写三段

普林斯顿研究员在这篇论文中提出了中全新的神经网络合成工具 NeST，既训练神经网络权重又训练架构。受人脑学习机制的启发，NeST 先从一个种子神经网络架构（出生点）开始合成。它能让神经网络基于梯度信息（婴儿大脑）生成连接和神经元，以便于神经网络能快速适应手头问题。然后，基于量级信息（成人大脑），它修剪掉不重要的连接和神经元从而避免冗余。这使得 NeST 能够生成紧凑且准确的神经网络。

NeST 先从一种种子架构开始（图 1a）。种子架构一般是一种稀疏的、局部连接的神经网络。然后，它在两个连续阶段合成神经网络：(i) 基于梯度的成长阶段；(ii) 基于量级的修剪阶段。在成长阶段，架构空间中的梯度信息被用于渐渐成长出新的连接、神经元和映射图，从而得到想要的准确率。在修剪阶段，神经网络继承成长阶段合成的架构与权重，基于重要性逐次迭代去除冗余连接与神经元。最终，得到一个轻量神经网络模型后 NeST 停止，该模型既不损失准确率，也是相对全连接的模型。

Princeton researchers in this paper proposed a new neural network synthesis tool NeST, both training neural network weights and training architecture. Inspired by human brain learning mechanisms, NeST begins with the synthesis of a seed neural network architecture (birth point). It allows neural networks to generate connections and neurons based on gradient information (baby's brain) so that the neural network can quickly adapt to the problem at hand. Then, based on the magnitude information (adult brain), it prunes off unimportant connections and neurons to avoid redundancy. This allows NeST to generate a compact and accurate neural network.

NeST begins with a seed architecture (Figure 1a). The seed structure is generally a sparse, locally connected neural network. It then composes the neural network in two successive phases: (i) a gradient-based growth phase; (ii) a magnitude-based clipping phase. In the growth phase, gradient information in architectural space is used to grow new connections, neurons, and maps to get the desired accuracy. In the pruning phase, neural networks inherit the architecture and weight of the synthetic phase of the growth phase and iteratively remove redundant connections and neurons iteratively based on their importance. Finally, NeST stops after a light neural network model is obtained. The model does not lose the accuracy and is also a relatively fully connected model.

The researchers in Princeton give a new neural network synthesist tool NeST, it can both train nerual network weights and structure. It's begins with a seed neural network structure which is inspired by buman brain. It allows nerual networks to generate connections like a baby's brain. So that this structure can quickly adapt to the problem. Then it prunes off unimportant connections like a adult brain which allows NeST to generate a compact and accruate neural network.

The seed structure is generally a sparse,locally connected neural network. It then composes the neural network in two successive phases. one is gradient-based growth phase and the other is magnitude-based clipping pahse. In growth phase, it use gradient information to grow new connections,neurons and maps to get the desired accuracy. In pruning phase,it inherit the structure and weight of the synthetic phase. Finally, NeST stops after a light neural network model is obtained. The model does not lose the accuracy and is also a relatively fully connected model.   