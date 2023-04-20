

| Reviewer **(R2)**                                            |
| ------------------------------------------------------------ |
| Scaling Distributed Machine Learning with In-Network Aggregation |
| nsdi2021                                                     |
| CS  341                                                      |

## summary

1. Distributed ML and DL commonly use all-reduce operations to exchange gradients. It is possible to use a programmable switch to perform all-reduce, similar to a parameter server. This centralized approach allows the switches to handle data exchange.
2. There are many hardware limitations on switches, such as limited memory space, and programmable switches only have a few megabytes of memory. To address this, *streams* aggregation has been proposed, aggregating a block of a tensor, typically only a few kilobytes, each time.
3. Results in faster training times and improved efficiency for a number of real-world benchmark models.

## advantage

1. The paper presents a new communication primitive called SwitchML that accelerates distributed parallel training by reducing the volume of exchanged data.
2. In-network aggregation is consistently superior to ring all-reduce performance.
3. The existing quantization methods have been used to reduce communication overhead. It achieves the minimum possible latency and the minimum communication cost.

## drawback

1. Programmable switches are not commonly used machines and need to be purchased separately.
1. Data sparsity is not utilized, which is addressed in the subsequent omni-reduce paper.
1. Programmable switches cannot support floating point computation. So it needs quantization, resulting in the precision loss. Therefore, they can only be used in machine learning. However, if programmable switches can handle floating-point numbers, quantization will not be necessary, and they can be further used in more fields.

## Justification

1. In this approach, workers send their model updates over the network, where an aggregation primitive in the network sums the updates and distributes only the resulting value.
2. Switches cannot process floating-point numbers, so they have developed their own quantization methods. They can represent floating-point numbers using integers.
3. SwitchML uses a combined switch-host architecture to partition computation between end-hosts and switches carefully. The switch performs integer aggregation, while end-hosts manage reliability and perform more complex computations.





什么是allreduce





![](https://pic4.zhimg.com/80/v2-91128397dc6575d5e2751fbe012a0023_1440w.webp)





每一轮的训练迭代都需要所有卡都将数据同步完做一次Reduce才算结束。如果卡数比较少的情况下，其实影响不大，但是如果并行的卡很多的时候，就涉及到计算快的卡需要去等待计算慢的卡的情况，造成计算资源的浪费。

每次迭代所有的计算GPU卡多需要针对全部的模型参数跟Reduce卡进行通信，如果参数的数据量大的时候，那么这种通信开销也是非常庞大，而且这种开销会随着卡数的增加而线性增长。



什么是ring allreduce ?

![](https://pic4.zhimg.com/80/v2-d725a864c17515b0677e37877693d84b_1440w.webp)



![](https://pic2.zhimg.com/80/v2-dd33b0b67b71eaa0bbf60ae3a8241e5d_1440w.webp)

因为每张卡上面的网络结构是固定的，所以里面的参数结构相同。每次通信的过程中，只将参数send到右手边的卡，然后从左手边的卡receive数据。经过不断地迭代，就会实现整个参数的同步，也就是reduce。

怎么做all reduce.

allreduce, MPI  , gloo 是在CPU上操作,  nccl是在GPU上操作. 

gpu- > cpu mem - >  cpu mem- > remote  GPU -> computation.

1. switch ML, 分布式ML,  DL常用allreduce,   可以用可编程交换机 programable Switch做allreduce, 做的parameter server一样. 集中的就是交换机在处理数据. 
2. 交换机上有很多硬件的限制.   有限的内存空间, 只有几M, 提出了流aggregation. 每次都是aggregate 一个block ,tensor 的一部分, 一个block 几个KB.  
3. 交换机处理不了浮点数 , 搞了自己的量化方法. 可以用int 表示float浮点数. 

总带宽变大了. 比ring allreduce更大.  



“1. 可编程不是常用的机器.需要单独购买.  1. 没有利用数据稀疏性. 在后面的omni reduce 中. 1. 可编程交换机导致了量化, 所以有精度损失. 所以只能用在机器学习上. 但是如果可编程交换机可以处理浮点数, 量化就不是必须的.  就可以进一步用在HPC领域. ”

Variations on this primitive have been proposed, over the years, for specialized supercomputer networks [2, 26] and InfiniBand [32]. We demonstrate that it is possible to re- alize in-network aggregation in an Ethernet network and benefit ML applications.
