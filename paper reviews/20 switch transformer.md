

| Reviewer **(R2)**                                            |
| ------------------------------------------------------------ |
| Switch Transformers: Scaling to Trillion Parameter Models with Simple and Efficient Sparsity |
| William Fedus  Google JMLR'22                                |
| CS  341                                                      |

## summary

1. This paper simplify the MoE routing algorithm and design intuitive improved models with reduced communication and computational costs.
1. Successful distillation of sparse pre-trained and specialized fine-tuned models into small dense models
1. Further reduction of training communication and improved training performance are achieved through data parallelism, model parallelism, and expert parallelism.

## advantage

1.  Switch Transformers outperform both carefully tuned dense models and MoE Transformers on a speed-quality basis.
1.  The Switch Transformer has a smaller computational footprint than the MoE counterpart.
1.  Switch Transformer architecture not only excels in the domain of supercomputers, but is beneficial even with only a few computational cores.

## drawback

1. Switch Transformer approach to be more unstable when used with low precision number formats
1. It use too complex parallelism so that it is not worthwhile for small dataset.
1.  the implementation of the sparsity patterns in the attention mechanism can be challenging

## Justification

1. The simplified routing algorithm presented in the Switch Transformer approach is called a Switch layer. Unlike traditional Mixture of Experts (MoE) models that route to multiple experts, the Switch layer routes to only a single expert. This simplification preserves model quality, reduces routing computation, and performs better. 
1. Expert, Model and Data Parallelism. When combining both model and expert-parallelism, we will have all-to-all communica- tion costs from routing the tokens to the correct experts along with the internal all-reduce communications from the model parallelism
1. An increase in the scale of neural language models achieved by efficiently combining data, model, and expert-parallelism to create models with up to a trillion parameters. These models improve the pre-training speed of a strongly tuned T5-XXL baseline by 4x.

替换了dense FFN, 用 sparse switch FFN. 

侧重switch部分.  pipeline 并行是怎么做的? 

只执行一部分model.



演讲.

## **动机**

现在的模型越来越大，训练样本越来越多，每个样本都需要经过模型的全部计算，这就导致了训练成本的[平方级](https://www.zhihu.com/search?q=平方级&search_source=Entity&hybrid_search_source=Entity&hybrid_search_extra={"sourceType"%3A"article"%2C"sourceId"%3A"335024684"})增长。

怎么降低成本? 

MOE, Mixture-Of-Experts的缩写 1991 Hinto write the paper.   idea: different experts.   hardware limit, data is small. 

ICLR  2017 : Jeff dean, 优点: 

moe 将大模型拆分成多个小模型，对于一个样本来说，无需经过所有的小模型去计算，而只是激活一部分小模型进行计算，这样就节省了计算资源.  

那么如何决定一个样本去经过哪些小模型呢？这就引入了一个[稀疏门机制](https://www.zhihu.com/search?q=稀疏门机制&search_source=Entity&hybrid_search_source=Entity&hybrid_search_extra={"sourceType"%3A"article"%2C"sourceId"%3A"335024684"})，即样本输入给这个门，得到要激活的小模型索引，同时包含n个[expert网络](https://www.zhihu.com/search?q=expert网络&search_source=Entity&hybrid_search_source=Entity&hybrid_search_extra={"sourceType"%3A"article"%2C"sourceId"%3A"335024684"})，这n个expert网络一般是同结构的。

这个门需要确保稀疏性，这样比较快 Sparsely-Gated: 不是所有expert都会起作用，而是极少数的expert会被使用来进行推理。这种稀疏性，也使得我们可以使用海量的experts来把模型容量做的超级大。

token-level：前面那个文章，是 sample-level 的，即不同的样本，使用不同的experts，但是这篇则是 token-level 的，一个句子中不同的token使用不同的experts。

这篇:  它是在T5模型的基础上加入了MoE设计，并在C4数据集上预训练。  Swith Transformer 的主要亮点在于——简化了MoE的[routing算法](https://www.zhihu.com/search?q=routing算法&search_source=Entity&hybrid_search_source=Entity&hybrid_search_extra={"sourceType"%3A"answer"%2C"sourceId"%3A"2577969736"})，从而大大提高了计算效率。

优点 1 : 不需要[稀疏算子](https://www.zhihu.com/search?q=稀疏算子&search_source=Entity&hybrid_search_source=Entity&hybrid_search_extra={"sourceType"%3A"answer"%2C"sourceId"%3A"1676632982"})，可以更好的适应当前的稠密硬件 [GPT-3](https://www.zhihu.com/search?q=GPT-3&search_source=Entity&hybrid_search_source=Entity&hybrid_search_extra={"sourceType"%3A"answer"%2C"sourceId"%3A"1676632982"})里所使用的sparse attention，还需要用到稀疏算子，这些稀疏算子往往限制稠密硬件的算力发挥.

figure 2 

Swith Transformer 在论文中提到其设计的指导原则是——**尽可能地把Transformer模型的参数量做大！**（同时以一种简单高效的实现方式）

跟其他MoE模型的一个显著不同就是，**Switch Transformer 的 gating network 每次只 route 到 1 个 expert**，而其他的模型都是至少2个。这样就是最稀疏的MoE了，因此单单从[MoE layer](https://www.zhihu.com/search?q=MoE layer&search_source=Entity&hybrid_search_source=Entity&hybrid_search_extra={"sourceType"%3A"answer"%2C"sourceId"%3A"2577969736"})的计算效率上讲是最高的了。

下图展示了在同样的计算开销下，增大 experts 个数带来的性能提升：figure 4 



Combining expert, model and data parallelism

不同颜色, split data.  

data并行, 每个核独立forward  backward. 

model 并行, 每个核保存所有的数据,有unique的weight. 通信代价非常高. 所有core都要通信. 

model and data并行:   4个核平分全局weight,  

expert and data , 所有核平分全局data.each core has its own expert .  只需要shard the E dimension instead of the n-dimension 

**Expert, Model and Data Parallelism** :   4个核平分一个 weight,  有4个不同的weight matrix. 

Expert并行实际上就是一种算子间的并行，[experts](https://www.zhihu.com/search?q=experts&search_source=Entity&hybrid_search_source=Entity&hybrid_search_extra={"sourceType"%3A"answer"%2C"sourceId"%3A"1676632982"})在计算图上是个多并行子图分支，每个分支是一个FFN结构。在FFN内部，再进一步进行算子级的模型并行。



## **难点**

听起来这个方法其实还是很直接的，那么为什么之前没有人做呢？主要因为以下几点：

- 现在的设备，比如GPU，比较擅长做运算，不擅长做分支。
- 大批量是训练模型的必须，但是这种方式下会导致每个小模型的样本数较少，无法训练得到好的模型
- 网络通信是瓶颈。
- 为了控制稀疏性，可能需要在loss上去做些改进，确保模型质量和小模型上的负载均衡
- 模型容量对大数据集比较重要，现有的工作都是在类似cifar10之类的数据上做的，很难有好效果。

It is common to mix both model and data parallelism for large scale models, which was done in the largest T5 models (Raffel et al., 2019; Xue et al., 2020) and in GPT-3 (Brown et al., 2020)



互联网很重要, 数据处理很重要. 爬虫技术很重要. 

camel, 大模型, fine tune. 被ICLR拒绝了. 

