

| Reviewer **(R2)**                                     |
| ----------------------------------------------------- |
| TensorFlow: A system for large-scale machine learning |
| M. Abadi et al osdi2016                               |
| CS  341                                               |

## summary

1. TensorFlow is an open-source software library for numerical computation and large-scale machine learning.
2. It is designed to be flexible and scalable, allowing developers to build and train various types of machine-learning models on a variety of platforms.
3. TensorFlow offers high-level APIs for building and training neural networks.

## advantage

1. TensorFlow can scale to handle large datasets and complex models.
2. TensorFlow can run on a variety of platforms.
3. TensorFlow provides high-level APIs for building and training neural networks.
4. TensorFlow Serving and TensorFlow Lite can be quickly deployed to cloud, server, mobile, and IoT devices.

## drawback

1. Compatibility issues: TensorFlow's rapid development pace can sometimes lead to compatibility issues
1. Steep learning curve: TensorFlow has a steep learning curve, especially for beginners. 
1. Lack of documentation: it can be challenging to navigate and may not always provide clear explanations or examples for specific use cases. 

## Justification

1. TensorFlow's dataflow representation subsumes existing work on parameter server systems. It offers a set of uniform abstractions that allow users to harness large-scale heterogeneous systems, both for production tasks and for experimenting with new approaches.
2. The requirement for compatibility with different versions of the CUDA library and the migration of function interfaces between different versions can lead to a significant amount of time spent setting up the environment when reproducing other people's code.
3. TensorFlow uses a single dataflow graph to represent all computation and state in a machine learning algorithm, including the individual mathematical operations, the parameters and their update rules, and the input pre-processing.



### pre

问题

1. before , they need use numpy to write NN.   You need has great fundation when you use regularization or dropout.   手写dropout - Jarvix的文章 - 知乎 https://zhuanlan.zhihu.com/p/72353349

通过深度神经网络得到的结果。能够极大地优于，早期的手工构建并且手工调试的模型。

它能把你写的代码转换成操作图。而真正运行的正是这种图。

顺便提一下，**在这些操作之间运行的数据叫做张量(Tensor)**。这也是名字的来源。TensorFlow 这个词由 Tensor 和 Flow 两个词组成，这两者是 TensorFlow 最基础的要素。Tensor 代表张量（也就是数据），它的表现形式是一个多维数组；而 Flow 意味着流动，代表着计算与映射，它用于定义操作中的数据流。

借助于TensorFlow的框架，你能够训练出这样的模型。含许多层，并且比早期的神经网络更复杂。

因为你的模型以图的形式展现出来，你可以推迟或者删除不必要的操作。甚至重用部分结果。你还可以很轻松地实现的一个过程叫做**反向传播**。如果你还记得的话，当我们基于所见的样本以及计算的误差，来更新模型中的连接强度。这整个过程就是反向传播。

最重要的是可以自动微分.  这些都是现在机器学习研究者最基本的知识. 但是在当时是非常惊人的突破. 

因为模型表现为操作图而不是代码，因此你不需要为此写额外的代码。只需直接自动地计算以及应用这些迭代更新。模型表现为图的另一个好处就是，在你的代码中，你可以用一行声明就表明:"我想这部分图在这里运行,我想另一部分图分布式运行在不同的机器群上"。

你甚至可以说"我想要这部分注重数学的图在GPU上运行,与此同时,数据输入部分的代码在CPU上运行"。

所以, 就很多工作, 比如融合算子.

来自于spark. 将数据保存在tensor里，将对数据的操作写成op，数据经过多个op的处理得到最后的结果，就像tensor在op里流动一样。 一样的思想. 

TensorFlow Serving是非常高性能的基础设施。你能够在自己的服务器上加载模型，用于低延时的推断请求

优势 : start early. Deploy tensorflow product. 

超算中 计算图优化,  

地方很小, 很多不同领域 交叉的聊天机会.  组和组差距很大, 你很少和别人聊天.
