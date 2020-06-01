# Deep Learning with Python

## Chapter 1
* Kaggle竞赛两大主流方法(2016-2017年)
    * 结构化数据: 梯度提升机(gradient boosting machine) - XGBoost库
    * 图像分类等感知问题: Deep Learning - Keras库
* 深度学习爆发的算法层面的原因
    * 更好的激活函数
    * 更好的权重初始化方案
    * 更好的优化方案, 比如RMSProp和Adam
    * 其他有助于梯度传播的方法: batch normalization, residual connection, **深度可分离卷积**

## Chapter 2
### 2.1 初始神经网络
这一节展示了第一个Keras的例子
```python
# numpy中的dtype可以用字符串表示, 但是不推荐
train_images = train_images.astype('float32') / 255
# to_categorical 将整数label转换为one hot label
train_labels = to_categorical(train_labels)
```

### 2.2 神经网络的数据表示
* n维张量 = nD张量 = n轴张量 = n阶张量 (推荐)
* 维度既可以表示沿着某个轴上的元素个数(比如5D向量), 也可以表示张量中轴的个数(5D张量)
* 张量的三个关键属性:
    - 轴的个数 ndim
    - 形状 shape
    - 数据类型 dtype
* Numpy (以及大多数其他库) 中不存在字符串张量, 因为张量存储在预先分配的连续内存段中, 而字符串的长度是可变的, 无法用这种方式存储

## Chapter 3
### 3.1 神经网络剖析
* 层&模型
* 输入数据&目标
* 损失函数
* 优化器

#### 层 - 深度学习的基础组件
* 简单的向量数据(samples, feature): 全连接层(fully connected layer) / 密集连接层(densely connected layer)
* 序列数据(samples, timesteps, features): 循环层(recurrent layer) 比如Keras的LSTM层
* 图像数据(samples, height, width, color_depth): 二维卷积层 Keras的Conv2D

#### 模型 - 层构成的网络
模型是层构成的有向无环图, 常见的网络拓扑结构:
* 线性堆叠
* 双分支(two-branch)网络
* 多头(multihead)网络
* Inception模块

#### 损失函数&优化器
* 具有多个输出的网络可能具有多个损失函数, 但是梯度下降过程必须基于单个标量损失值, 需要将所有损失函数取平均, 变成一个标量值
* 二分类问题: 二元交叉熵(binary crossentropy)
* 多分类问题: 分类交叉熵(categorical crossentropy)
* 回归问题: 均方误差(mean-squared error)
* 序列学习问题: 联结主义时序分类(CTC, connectionist temporal classifcation)损失函数

### Keras简介
#### 重要特性
* 代码可以在CPU或GPU上无缝切换运行
* 用户友好API, 快速开发DL原型
* 内置支持卷及网络, 循环网络以及两者的任意组合
* 支持任意网络架构: 多输入或多输出模型, 层共享, 模型共享等等. 能够构建任意深度学习模型, 无论是生成式对抗网络还是神经图灵机

Keras是一个模型级的库, 不处理张量操作, 求微分等低层次的运算. 它依赖一个专门的, 高度优化的张量库来完成这些运算,
这个库就是Keras的后端引擎(backend engine), 有多种后端实现, 最常见的是Tensorflow

#### 典型的Keras工作流
1. 定义训练数据: 输入张量和目标张量
2. 定义层组成的模型, 将输入映射到目标
3. 配置学习过程(compile): 选择损失函数, 优化器和需要监控的指标
4. 调用模型的fit方法在训练数据上进行迭代

定义模型的两种方法, 一旦定义好了模型架构, 接下来的步骤是相同的
* Sequential类(仅用于层的线性堆叠)
* 函数式APT(functional API, 用于层构成的有向无环图, 可以构建任意形式的架构)

## Chapter 4
### 4.1 机器学习的四个分支
* 监督学习
* 无监督学习
    - 无监督学习是数据分析的必备技能, 在解决监督学习之前, 为了更好地了解数据集, 它通常是一个必要步骤.
    - 尝试掌握该必备技能!
* 自监督学习
    - 自编码器
    - 时序监督学习: 给定视频中过去的帧来预测下一帧, 文本中前面的词预测下一个词
    - 取决你关注的是学习机制还是应用场景, 自监督学习可以重新被解释为监督学习或无监督学习
* 强化学习

**P.S.**
* 多标签分类(multilabel classification) 每个输入样本都可以分配多个标签, 每个样本的标签个数通常是可变的.
* minibatch中的样本数通常取2的幂, 这样便于GPU上的内存分配
