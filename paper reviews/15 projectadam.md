

| Reviewer **(R2)**                                            |
| ------------------------------------------------------------ |
| Project Adam: Building an Efficient and Scalable Deep Learning Training System |
| 2014                                                         |
| CS  341                                                      |

## summary

1. Project Adam is a research project aimed at creating an efficient and scalable deep-learning training system.
2. Describes the design and implementation of Adam, focusing on computation and communication optimizations and the use of asynchrony to improve system efficiency and scaling.
3. It has efficiency and scalability, using commodity server machines to train large deep neural network models.

## advantage

1. SOTA performance on difficult visual recognition tasks.
2. Significant improvement in efficiency and scalability compared to previous systems.
3. Asynchrony throughout the system to improve the performance and accuracy of trained models.

## drawback

1. The paper primarily focuses on image recognition tasks. 
1. It is not open source.
1. The datasets are limited. They don't evaluate this system on various datasets.

## Justification

1. The system uses a combination of CPU and GPU computing resources to accelerate the training of deep neural networks.
2. It used 30x fewer machines to train a giant 2 billion connection model to 2x higher accuracy in comparable time on the ImageNet 22,000 category image classification task than the system that previously held the record for this benchmark.
3. partitioning large models across machines to minimize memory bandwidth and cross-machine communication requirements, as well as restructuring the computation across machines to reduce communication requirements. 

大大省钱了. 

他们也是无锁写入, 不过要求 associative可结合的 and commutative 可交换的 weight updates , 而不是要求模型稀疏. 

3.2.4 , 把model 切分了, 再这样 workering sets for the model layers fit in the L3 cache.

他们发送了 activation 和error gradient ,而不是发送梯度更新.   减少了通讯流量. 

deepspeed就是起源于 project adam. 微软从那时候就开始布局机器学习, 2023年大丰收, copliot, ms365. new bing.





