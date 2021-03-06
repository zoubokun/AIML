# 第一次上课总结
## 基本概念
### 摘要
#### 本次学习中我们将学到神经网络的基本的训练和工作原理，后面接着是导数公式和反向传输公式，包括矩阵求导，主要目的是可以备查，在自己推导反向公式时可以参考，然后是反向传播和梯度下降，梯度下降是神经网络的基本学习方法，最后会学习损失函数的讲解，着重说明了神经网络中目前最常用的均方差损失方程和交叉熵损失方程
### 第1章 神经网络的基本工作原理
- 一个神经元可以有多个输入
- 一个神经元只能有一个输出，这个输出可以同时输入给多个神经元**
- 一个神经元的w的数量和输入的数量一致
- 一个神经元只有一个b
- w和b有人为的初始值，在训练过程中被不断修改
- 激活函数不是必须有的，亦即A可以等于Z
- 一层神经网络中的所有神经元的激活函数必须一致
### 步骤
假设我们有以下训练数据样本：

|Id|x1|x2|x3|Y|
|---|---|---|---|---|
|1|0.5|1.4|2.7|3|
|2|0.4|1.3|2.5|5|
|3|0.1|1.5|2.3|9|
|4|0.5|1.7|2.9|1|

其中，x1，x2，x3是每一个样本数据的三个特征值，Y是样本的真实结果值：

1. 随机初始化权重矩阵，可以根据高斯分布或者正态分布等来初始化。这一步可以叫做“蒙”，但不是瞎蒙。
2. 拿一个或一批数据作为输入，带入权重矩阵中计算，再通过激活函数传入下一层，最终得到预测值。在本例中，我们先用Id-1的数据输入到矩阵中，得到一个A值，假设A=5
3. 拿到Id-1样本的真实值Y=3
4. 计算损失，假设用均方差函数 $Loss = (A-Y)^2=(5-3)^2=4$
5. 根据一些神奇的数学公式（反向微分），把Loss=4这个值用大喇叭喊话，告诉在前面计算的步骤中，影响A=5这个值的每一个权重矩阵，然后对这些权重矩阵中的值做一个微小的修改（当然是向着好的方向修改，这一点可以用数学家的名誉来保证）
6. 用Id-2样本作为输入再次训练（goto 2）
7. 这样不断地迭代下去，直到以下一个或几个条件满足就停止训练：损失函数值非常小；迭代了指定的次数；计算机累吐血了......

训练完成后，我们会把这个神经网络中的结构和权重矩阵的值导出来，形成一个计算图（就是矩阵运算加上激活函数）模型，然后嵌入到任何可以识别/调用这个模型的应用程序中，根据输入的值进行运算，输出预测值。
### 神经网络的主要功能
- **回归/拟合 Regression/fitting**
- **分类 Classification**
### Deep Learning的训练过程简介
1. 使用自下上升非监督学习（就是从底层开始，一层一层的往顶层训练）

   采用无标签数据（有标签数据也可）分层训练各层参数，这一步可以看作是一个无监督训练过程，是和传统神经网络区别最大的部分（这个过程可以看作是feature learning过程）。
   具体的，先用无标签数据训练第一层，训练时先学习第一层的参数（这一层可以看作是得到一个使得输出和输入差别最小的三层神经网络的隐层），由于模型capacity的限制以及稀疏性约束，使得得到的模型能够学习到数据本身的结构，从而得到比输入更具有表示能力的特征；在学习得到第n-1层后，将n-1层的输出作为第n层的输入，训练第n层，由此分别得到各层的参数；

2. 自顶向下的监督学习（就是通过带标签的数据去训练，误差自顶向下传输，对网络进行微调）

   基于第一步得到的各层参数进一步fine-tune整个多层模型的参数，这一步是一个有监督训练过程；第一步类似神经网络的随机初始化初值过程，由于deep learning的第一步不是随机初始化，而是通过学习输入数据的结构得到的，因而这个初值更接近全局最优，从而能够取得更好的效果；所以deep learning效果好很大程度上归功于第一步的feature learning过程。
### 总结与心得体会
通过本节课的学习，我学习了什么是神经网络，了解了神经网络的基本工作原理，知道了神经元细胞的数学模型，了解了神经网络的训练过程和神经网络中的矩形运算，还有学习了神经网络的主要功能有回归拟合和分类，单层的神经网络能够模拟一条二维平面上的直线，从而可以完成线性分割任务。而理论证明，两层神经网络可以无限逼近任意连续函数。也通过生物学上的例子知道了为什么需要激活函数，我们希望我们的神经网络不仅仅可以学习和计算线性函数，而且还要比这复杂得多，通常我们把三层以上的网络称为深度神经网络。两层的神经网络虽然强大，但可能只能完成二维空间上的一些拟合与分类的事情。如果对于图片、语音、文字序列这些复杂的事情，就需要更复杂的网络来理解和处理。第一个方式是增加每一层中神经元的数量，但这是线性的，不够有效。另外一个方式是增加层的数量，每一层都处理不同的事情，这就是我们为什么需要深度神经网络和深度学习。也了解了Deep Learning的训练过程。本次学习我学到了很多，也为之后神经网络更加深度的学习打下了深厚的基础。