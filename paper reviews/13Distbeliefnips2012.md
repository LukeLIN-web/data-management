

| Reviewer **(R2)**                     |
| ------------------------------------- |
| Large Scale Distributed Deep Networks |
| 2012                                  |
| CS  341                               |

## summary

1. The authors propose a scalable approach to distributed training called DistBelief.
2. Designed and implemented two novel methods: *Downpour SGD*, an asynchronous stochastic gradient descent procedure. *Sandblaster L-BFGS*, a distributed implementation of L-BFGS that uses both data and model parallelism
3. The experiments reveal several surprising results about large-scale nonconvex optimization. 

## advantage

1. Train a deep network 30x larger than previously reported in the literature.
2. The underlying algorithms apply to any gradient-based machine learning algorithm. This paper found a critical Distributed DNN training architecture.
3.  Achieves SOTA performance on ImageNet.

## drawback

1. Communication overhead: The communication overhead of exchanging gradients between machines can be high, which may reduce the system's overall performance. 
2. Resource requirements: The approach requires a large number of machines and a high-speed network to achieve good performance, which can be costly and may not be feasible for small labs.
3. It doesn't have enough consideration for fault tolerance. So in the future, researchers propose different ways to improve it.

## Justification

1. Downpour SGD, divide the training data into a number of subsets, and run a copy of the model on each of these subsets. The models communicate updates through a centralized parameter server, which keeps the current state of all parameters for the model, sharded across many machines. 
2. Sandblaster L-BFGS, a distributed implementation of L-BFGS, can be competitive with SGD. Its more efficient use of network bandwidth enables it to scale to a more significant number of concurrent cores for training a single model.
3. Parameter server architecture has a scalability bottleneck at the parameter server machine. So the following papers propose ring-all reduce to solve it.
4. DistBelief led to further training framework Tensorflow.

现在大部分时候, 用同步通讯, 用dedicated GPU而不是 几千个CPU训练. 

Sandblaster L-BFGS 没有收敛保证. 

训练加速的图, 很误导人, x用log, y用了线性, 实际上他是严重非线性的 , 但是他画起来就像linear一样. 花了128倍的钱, 只有15x不到的加速.  

在当时都还只有一个GPU训练, 没有GPU并行. 没有torch也没有tensorflow. 没有这么多cuda 代码.

Mapreduce不适合迭代操作.  没有保存state, io太多了.

