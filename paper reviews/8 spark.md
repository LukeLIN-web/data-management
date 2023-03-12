

| Reviewer **(R2)**                                            |
| ------------------------------------------------------------ |
| [**[Spark: Cluster Computing with Working Sets](http://people.csail.mit.edu/matei/papers/2010/hotcloud_spark.pdf).**](http://research.google.com/archive/mapreduce.html) |
| Matei Zaharia, Mosharaf Chowdhury, Michael J. Franklin, Scott Shenker, Ion Stoica |
| CS  341                                                      |

## Summary 

- The paper introduces the concept of Resilient Distributed Datasets (RDDs), a fundamental data abstraction that allows data to be stored in memory across a cluster of machines and processed in parallel.
- The paper describes the Spark programming model and its support for fault tolerance, data partitioning, and transformations and actions on RDDs.
- The paper demonstrates the performance benefits of Spark compared to Hadoop MapReduce for iterative algorithms.

## Advantage

1. Previous mapreduce tasks always need to load data from disk in iterative workloads. Spark first proposes a data model to optimize these workloads.
2. Spark can process iterative workloads much faster than Hadoop MapReduce, making it well-suited for machine learning and other applications that require repeated computations on large datasets.
3. Spark broadcast variables can be reused *across* parallel operations. It is better than Hadoop. Spark can outperform Hadoop by 10x in iterative machine learning workloads and can be used interactively to scan a 39 GB dataset with sub-second latency.
4. Spark is opensource.

## Drawback

1. The implementation of Spark is still at an early stage. 
2. Lack of discussion on fault tolerance: Although Spark provides fault tolerance mechanisms, the paper does not discuss how these mechanisms work in detail
3. Limited evaluation: The paper provides a limited evaluation of Spark's performance by comparing it to Hadoop MapReduce on a small set of benchmarks. 

## Justification

1. RDDs provide fault tolerance by allowing lost data to be reconstructed through lineage information captured in the RDD objects. 
2. The paper shows how engineers can use Spark for various applications, such as Text Search, Logistic Regression. It is first engine support multiple end-to-end big data applications. 
3. The authors do not explore the full range of use cases and workloads that Spark can handle. The experiments don't show the results of the very large datasets.
4. Spark can process distributed data in very large volumes and allows people to achieve real-time interactive analysis. Because it is built on RDDs and in-memory storage for intermediate data, it provides high support for real-time processing.
5. Users don't need to consider how to translate to 'map' and 'reduce' operations, as Spark provides interfaces with higher levels of abstraction so that it is easy to use and fast.



之前, 发现集群计算有巨大潜力, mapreduce 有挑战,很慢,  迭代的话要很多mapreduce

内存价格降下来了

没有实现对集群内存的抽象封装。这样对那些需要重复利用中间结果集的应用就很不友好.

Spark想解决一个问题，就是数据（在内存中）的[复用性](https://www.zhihu.com/search?q=复用性&search_source=Entity&hybrid_search_source=Entity&hybrid_search_extra={"sourceType"%3A"article"%2C"sourceId"%3A"438880210"})，作者发现在这种情况下MapReduce不是很高效.

迭代式任务：机器学习算法往往需要重复作用一个数据集去优化一个参数，每一次迭代都可以表示成MapReduce任务，都需要重新从磁盘加载数据。

迭代式分析：用户很自然地需要加载数据集到内存中，多次对数据集做[查询分析](https://www.zhihu.com/search?q=查询分析&search_source=Entity&hybrid_search_source=Entity&hybrid_search_extra={"sourceType"%3A"article"%2C"sourceId"%3A"438880210"})，但对于MapReduce任务而言，每次查询都是一次单独的MapReduce任务，需要重新从磁盘加载数据。

Spark Alpha-0.1 - Chao.G的文章 - 知乎 https://zhuanlan.zhihu.com/p/438880210

RDD:为什么你必须要理解弹性分布式数据集？ - Linf的文章 - 知乎 https://zhuanlan.zhihu.com/p/424165937

不用记住所有中间结果, 而是记下来所有转换, 每次都重算. 这也是deepspeed的想法. 

