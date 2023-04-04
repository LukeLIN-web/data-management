

| Reviewer **(R2)**                                            |
| ------------------------------------------------------------ |
| HOGWILD!: A Lock-Free Approach to Parallelizing Stochastic Gradient Descent |
| 2011                                                         |
| CS  341                                                      |

## summary

1. Before this paper, several researchers used parallel SGD, but all required performance-destroying memory locking and synchronization.
2. Introduces a novel method for parallelizing SGD. Allows multiple processors to update the same model parameters in parallel.
3. Through theory and experiments, they demonstrate that Hogwild! Achieves near-linear speedup with respect to the number of processors on data that satisfies appropriate sparsity conditions.

## advantage

1. This paper presents the first method that demonstrates how to parallelize SGD without any locking mechanism.
2. This method also provides strong performance guarantees.
3. Memory efficiency: HOGWILD! It requires minimal memory overhead as it does not need to maintain multiple copies of the model parameters for each processor.

## drawback

1. It assumes that the hypergraph induced by f is isotropic and sparse. 
1. HOGWILD! may result in slightly lower model accuracy due to the lack of synchronization between processors
1. HOGWILD! may have slower convergence rates than traditional methods

## Justification

1. Each worker runs SGD on a different subset of the data simultaneously and performs fully asynchronous updates on the shared memory that stores the model parameters.
2. No locking may lead to access conflicts. By imposing certain restrictions on the sparsity of the model parameters, the access conflicts are actually very limited. This is the theoretical basis for the convergence of the Hogwild! algorithm.
3. Achieves scalability by allowing multiple processors to operate simultaneously on different subsets of the data without the need for expensive communication overhead or synchronization mechanisms.
4. This paper obtains the NIPS 2020 Test Of Time Award. 



维护一个全局的模型，每个任务都有一个本地的局部模型，通过同步本地与全局的模型来达到更新的目的，使得全局模型能够处理多个任务。

这是异步sgd中非常重要的一篇文章. 

本文针对稀疏问题提出了一种简单的策略，称为Hogwild：让每个工作人员在数据的不同子集上同时运行SGD，并在托管模型参数的共享内存中执行完全异步更新。通过理论和实验，他们证明了Hogwild满足适当稀疏性条件的数据上的处理器数量实现了近乎线性的加速。

### 背景

当时，一些研究人员提出了并行化SGD的方法，但是它们都需要跨不同工作进程的内存锁定和同步。

异步并行算法既可以在多机集群上开展，也可以在多核系统下通过多线程开展。当我们把ASGD算法应用在多线程环境中时，因为不再有参数服务器这一角色，算法的细节会发生一些变化。特别地，因为全局模型存储在共享内存中，所以当异步的模型更新发生时，我们需要讨论是否将内存加锁，以保证模型写入的一致性。

如果训练中每个分布计算单元都能得到最新参数，这种训练算法叫**模型一致性方法**（consistent model methods）。当放松同步的限制条件，则训练得到的是一个不一致的模型，比如Yahoo提出的分布式SGD 算法Hogwild，允许训练代理随意读取参数和更新梯度，覆盖现有进展。Hogwild已被证明可以收敛稀疏学习（sparse learning）问题，其中更新仅修改参数的子集，可用于一般的凸优化**convex** optimaztion和非凸优化问题。

Hogwild！算法为了提高训练过程中的数据吞吐量，选择了无锁的全局模型访问.



![](https://pic3.zhimg.com/v2-84acd7a9f4d4e90e9860577d24695782_b.jpg)



参数更新过程中，发生冲突了那算法还有效吗？回答是肯定的。详细的证明过程可以看Paper，这里只简单说一下。SGD计算过程是随机抽取样本进行计算更新参数的，随机的情况下其实参数更新冲突的概率就大大降低了，即便冲突了梯度也不完全是往差的方向发展，毕竟都是朝着梯度下降的方向更新的。

Hogwild!的第一作者Feng Niu首先实现了一个加锁的同步版本，去掉锁之后发现速度快了100x，分析发现，正常的一次梯度更新计算只要微秒级别甚至更少的时间，而[加锁](https://www.zhihu.com/search?q=加锁&search_source=Entity&hybrid_search_source=Entity&hybrid_search_extra={"sourceType"%3A"answer"%2C"sourceId"%3A"72373555"})带来的排队等待往往就在毫秒级别了，所以即使有冲突整个算法也加速了不少。

当采用不带锁的多线程的写入（即在更新wjw_jw_j的时候不用先获取对wjw_jw_j的访问权限），而这可能会导致导致**同步错误**的问题。比如在线程1加载全局参数之后，线程2还没等线程1存储全局参数更新后的值，就也对全局参数wjtw^t_jw^t_j进行加载，这样导致每个线程都会存储值  更新后的全局参数值，这样就导致其中一个线程的更新实际上在做“无用功”。直观的感觉是这应该会对学习的过程产生负面影响。分布式机器学习：异步SGD和Hogwild!算法（Pytorch） - 猎户座的文章 - 知乎 https://zhuanlan.zhihu.com/p/606063318

不过，当我们对模型访问的稀疏性（sparity）做一定的限定后，这种访问冲突实际上是非常有限的。这正是Hogwild！算法收敛性存在的理论依据。

假设我们要最小化的损失函数为，对于特定的训练样本集合，损失函数是由一系列稀疏子函数组合而来的：

也就是说，实际的学习过程中，每个训练样本涉及的参数组合eee只是全体参数集合中的一个很小的子集。



这个假设在大规模机器学习问题中一般都成立，大多模型的总体维度非常高，达到千万million或者billion上亿级别，但是真正取值为1的特征只有几十个左右







